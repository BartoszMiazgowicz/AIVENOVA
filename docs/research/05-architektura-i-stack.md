# 05 - Architektura techniczna i stack (stan na 2026-11-13)

Metoda: 22 zapytania WebSearch plus dokumentacja pierwszej strony przez MCP (wyszukiwarka docs Vercel i Supabase). WebFetch był zablokowany, a wspólny limit WebSearch wyczerpał się w trakcie pracy. Dlatego Sentry, PostHog, Typesense/Meilisearch, next-intl, Expo, Modal, Cloudflare Containers i dostawcy moderacji NIE zostały sprawdzone na żywo i mają tag [niepewne]. Tagi: [zweryfikowane] = jest źródło z dzisiejszego odczytu, [wnioskowanie] = mój wniosek, [niepewne] = źródła sprzeczne, wtórne albo tylko moja wiedza sprzed połowy 2026.

## TL;DR

- **Stack bazowy trzyma się kont, które już są:** Next.js 16.4 + React 19 na Vercel Pro (Fluid Compute, region `fra1`) oraz Supabase Pro w regionie UE (Postgres, Auth, Realtime, pg_cron, pgmq). [wnioskowanie]
- **Media poza Supabase Storage:** Cloudflare R2 (0 USD za egress). Przy 10k MAU różnica to ok. 65 USD kontra 210-510 USD miesięcznie. [wnioskowanie na cenach zweryfikowanych]
- **Zadania generacji:** źródłem prawdy jest maszyna stanów w Postgres; wykonawcą Vercel Workflow (`"use workflow"`, `createWebhook`, `sleep`), a niezależnym bezpiecznikiem sweeper w pg_cron. Orkiestrator za interfejsem, zamiennik: Trigger.dev. [wnioskowanie]
- **Vercel AI Gateway obsługuje dziś obraz i wideo** (Veo, Kling, Wan, Seedance) z webhookiem i pollingiem, bez marży; AI SDK 7 ma stabilne `generateImage` i `generateSpeech`, a `experimental_generateVideo` wciąż eksperymentalne. [zweryfikowane]
- **ffmpeg nie w Supabase Edge Functions** (2 s CPU, brak sharp/libvips) i niechętnie w funkcjach Vercel; rekomendacja: sharp w funkcji dla obrazów, Vercel Sandbox dla wideo. [zweryfikowane + wnioskowanie]
- **Infrastruktura to ok. 2-4% kosztu inferencji:** ok. 80-190 USD/mies. przy 1k MAU i 570-1250 USD przy 10k MAU (przy założeniu średnio 0,15 USD inferencji na generację). Architekturę optymalizować pod niezawodność rozliczeń i śledzenie kosztu generacji, nie pod grosze na hostingu. [wnioskowanie]

## 1. Zweryfikowany stan platform

### 1.1 Next.js, React, AI SDK

| Temat | Stan | Tag |
|---|---|---|
| Wersja | Linia stabilna **16.4** (6-7.10.2026), łatka 16.4.4 z 10.11.2026 zawiera poprawki bezpieczeństwa (optymalizacja obrazów, ciasteczka w Edge runtime). Next.js 17 nie wyszedł. Źródła różnią się numerem łatki (16.4.3 kontra 16.4.4). ([blog][next164], [releasebot][releasebot], [versionlog][versionlog]) | [zweryfikowane] |
| 16.4 | Funkcje React 19.3, lazy compilation, mniejszy output Turbopack. Cache Components będą domyślne w Next 17, a `create-next-app` włącza je już teraz. ([blog][next164]) | [zweryfikowane] |
| 16.0 | `proxy.ts` zastępuje `middleware.ts` i działa na Node.js; cache jest jawny (`"use cache"` + PPR); Turbopack domyślny w dev i build; React 19.2. ([blog][next16]) | [zweryfikowane] |
| AI SDK | **AI SDK 7**: Node 22+, tylko ESM, `generateImage` i `generateSpeech`/`transcribe` stabilne, `experimental_generateVideo` z providerami fal, Google, Vertex, Replicate; zmiany nazw (`system` na `instructions`). ([blog][aisdk7], [docs][aisdk-docs]) | [zweryfikowane] |

### 1.2 Vercel

| Element | Fakty | Tag |
|---|---|---|
| Fluid Compute | Domyślne dla nowych projektów od 23.04.2025. Max duration: Hobby 300 s; Pro/Enterprise domyślnie 300 s, max 800 s (GA), 1800 s w becie dla Node/Bun/Python, w docs opisane dla funkcji poza App Routerem. ([fluid][v-fluid], [duration][v-duration]) Dla route handlerów Next.js zakładać 800 s. | [zweryfikowane], ostatnie zdanie [wnioskowanie] |
| Limity | Bundle funkcji 250 MB po rozpakowaniu ([docs][v-limits]). Region domyślny `iad1`, trzeba ustawić ręcznie ([docs][v-ts]). Limit 4,5 MB na body żądania: nie potwierdzony dziś. | [zweryfikowane]; body [niepewne] |
| Cennik | Pro 20 USD/mies. z kredytem 20 USD; Active CPU od 0,128 USD/h, pamięć od 0,0106 USD/GB-h (źródła wtórne, [przegląd][usagepricing]). Flat Rate CDN (GA 09.2026): w Pro 1 TB i 1M żądań, wyższe progi 20/100/300 USD ([changelog][v-flatcdn]). | [zweryfikowane wtórnie] |
| Workflow | `"use workflow"`, `"use step"`, `sleep`, `defineHook`, `createWebhook`; pakiet `workflow` 5.x; istnieje `@workflow/world-postgres` (przenośność). 50k zdarzeń/mies. w cenie, potem 0,02 USD/1k; 0,50 USD/GB zapisu i GB-mies. retencji; max 10k kroków i 25k zdarzeń na run. ([docs][v-wf], [cennik][v-wf-price]) Status GA nie potwierdzony. | [zweryfikowane]; status [niepewne] |
| Queues | **Beta na wszystkich planach.** Retencja 60 s-7 dni (domyślnie 24 h), opóźnienie do 7 dni, visibility timeout do 60 min, klucz idempotencji, dostarczanie at-least-once ([docs][v-queues], [API][v-queues-api]). Cena od 0,60 USD/1M operacji, naliczanie w porcjach 4 KiB ([źródło wtórne][usagepricing]). | [zweryfikowane]; cena wtórnie |
| Cron | Cron Jobs oznaczone jako legacy, migracja do **Schedules** (`schedules` w `vercel.json`: strefa czasowa, jitter, cel: funkcja, ścieżka lub topic kolejki). ([docs][v-sched]) | [zweryfikowane] |
| Blob | 0,023 USD/GB-mies., transfer 0,05 USD/GB, operacje 0,40 i 5,00 USD/1M; prywatne i publiczne w tej samej cenie; cache do 512 MB na obiekt. ([cennik][v-blob]) | [zweryfikowane] |
| Sandbox | Active CPU 0,128 USD/vCPU-h, pamięć 0,0212 USD/GB-h, do 8 vCPU/16 GB; `apt-get install` przez sudo; polityka sieci `deny-all`; trwałe sandboxy ze snapshotami. Hobby: sesja do 45 min, 10 równolegle ([docs][v-sbx-harbor]). Max sesja Pro: źródła podają 5 h albo 24 h. ([docs][v-sbx], [firewall][v-sbx-fw], [cennik wtórny][sbx-price]) | [zweryfikowane]; limit Pro [niepewne] |
| AI Gateway | Obraz: `generateImage`, `/v1/images/generations` (GPT Image 2, Flux, Recraft, Grok Imagine). Wideo: `experimental_generateVideo` z opcjami `webhook` i `poll`; żądanie startowe do 300 KiB, więc referencje jako URL. Ceny dostawcy bez marży; budżety na klucz API; raport kosztów `GET /v1/report` od Pro. Wideo w becie dla planów płatnych. ([wideo][v-gw-video], [obraz][v-gw-image], [Veo][v-gw-veo], [budżety][v-gw-budget]) | [zweryfikowane] |
| BotID, Firewall | BotID Basic za darmo; Deep Analysis 1 USD/1000 wywołań `checkBotId()`, tylko Pro+. WAF rate limiting na wszystkich planach: Hobby 1 reguła, Pro 40 reguł i 0,50 USD/1M przepuszczonych żądań; ruch zablokowany nie jest naliczany. `checkRateLimit(id, { rateLimitKey })` z `@vercel/firewall`. ([BotID][v-botid], [WAF][v-waf], [SDK][v-waf-sdk]) | [zweryfikowane] |

### 1.3 Supabase

| Element | Fakty | Tag |
|---|---|---|
| Plany | Free: 2 projekty, 500 MB bazy, 1 GB plików, 5+5 GB egress, **pauza po 7 dniach niskiej aktywności**. Pro 25 USD/mies. za organizację: 100k MAU, 8 GB dysku, 100 GB plików, 250 GB egress uncached + 250 GB cached, 10 USD kredytu compute, brak pauzowania, Spend Cap domyślnie włączony. Od 05-06.2026 Supabase wdraża VAT tam, gdzie jest zarejestrowany; NIP UE w ustawieniach pozwala na reverse charge. ([billing][s-billing], [FAQ][s-faq], [pauzowanie][s-freepause]) | [zweryfikowane] |
| Projekt wstrzymany | Dane zostają; przywrócenie jednym kliknięciem przez 90 dni, potem tylko pobranie backupu i plików ([docs][s-pause]). Status `INACTIVE` w API oznacza projekt wstrzymany: API i baza nie odpowiadają do czasu przywrócenia. Pod produkcję założyć projekt w regionie UE na planie Pro. | [zweryfikowane]; od `INACTIVE` [wnioskowanie] |
| Storage | Plik do 50 MB (Free) lub 500 GB (Pro); TUS w kawałkach 6 MB; signed upload URL; protokół S3. Nadwyżki: 0,0213 USD/GB-mies., egress 0,09 (uncached) i 0,03 (cached) USD/GB. Transformacje obrazów: 5 USD za 1000 obrazów źródłowych ponad 100, max 25 MB i 50 MP. ([limity][s-filelimits], [TUS][s-tus], [egress][s-egress], [transformacje][s-img]) | [zweryfikowane] |
| Realtime | Pro: 500 połączeń i 500 msg/s; bez Spend Cap 10 000 i 2 500. W cenie 5M wiadomości i 500 peak connections, potem 2,50 USD/1M i 10 USD/1000. Broadcast from Database i autoryzacja kanałów: public beta. ([limity][s-rt], [statusy][s-features]) | [zweryfikowane] |
| Edge Functions | 256 MB, 150 s (Free) / 400 s (płatne) wall clock, **2 s CPU na żądanie**, bez sharp/libvips. ([limity][s-fn]) | [zweryfikowane] |
| Auth | OAuth, magic link, SAML, CAPTCHA w GA; anonymous sign-ins z konwersją na konto stałe; **passkeys eksperymentalne** (supabase-js 2.105+, opt-in; zmiana RP ID unieważnia wszystkie passkeys). Przykłady w docs używają już kluczy publishable/secret. ([passkeys][s-passkeys], [anon][s-anon], [statusy][s-features]) | [zweryfikowane] |
| Queues, Cron, Branching | pgmq (visibility timeout, archiwum), pg_cron z interwałem sekundowym, pg_net do wywołań HTTP ([queues][s-queues], [wzorzec][s-embed]). Branching w becie: od 0,01344 USD/h za gałąź Micro, poza Spend Cap. ([branching][s-branch]) | [zweryfikowane] |

### 1.4 Alternatywy dla trwałych zadań w tle

| Narzędzie | Cennik | Uwagi | Tag |
|---|---|---|---|
| Inngest | Free 50k wykonań/mies., ok. 5 równoległych; Pro ok. 99 USD za 1M (część źródeł: 75) ([przegląd][inngest]) | Dojrzałe klucze współbieżności, kolejny dostawca | [niepewne] |
| Trigger.dev | Free 5 USD kredytu, Hobby 10 USD, Pro 50 USD/mies.; compute od 0,0000169 USD/s (micro) do 0,00068 USD/s (large-2x) + 0,000025 USD za run; 20/50/200+ równoległych ([limity][trigger], [przegląd][trigger-price]) | Własne maszyny bez limitu czasu, nadaje się też do ffmpeg | [zweryfikowane wtórnie] |
| Upstash QStash / Workflow | 1 USD za 100k wiadomości lub kroków; 1000 dziennie za darmo ([QStash][qstash], [Workflow][upwf]) | Najtańsze, oparte o HTTP | [zweryfikowane] |
| Cloudflare Queues / Workflows | Queues 0,40 USD/1M operacji; Workflows: rozliczanie per krok od 08.2026 (500k w cenie, 0,80 USD/100k) ([cennik][cf-workers]) | Sens tylko przy logice w Workers | [niepewne] |

## 2. Trudne części: opcje i rekomendacje

### (a) Potok generacji

Stany: `queued → submitted → processing → ingesting → succeeded | failed | expired | canceled`.

1. **Submit** (route handler): walidacja schematem modelu, potem jedna transakcja RPC: limit równoległych zadań planu, blokada kredytów w ledgerze, insert `generations` z `idempotency_key` (unikalny per workspace) i `deadline_at`.
2. **Workflow**: krok `submitToProvider` zapisuje `provider_request_id`; następnie wyścig `createWebhook()` z `sleep(timeout)`. Po timeoucie polling statusu z backoffem.
3. **Webhook dostawcy**: weryfikacja podpisu, deduplikacja w `webhook_events (provider, request_id, event)`, szybkie 200.
4. **Ingest**: strumieniowe pobranie wyniku (URL-e dostawców wygasają) do R2 pod kluczem `outputs/{workspace}/{generation}/{n}.{ext}`; upsert `assets`.
5. **Post-processing**: miniatury, blurhash, poster, znak wodny (punkt c).
6. **Settle**: wpis `settle` albo `release` z unikalnością `(generation_id, kind)`; zmiana stanu przez `UPDATE ... WHERE status IN (...)`.
7. **Notyfikacja**: trigger na `generations` wysyła Broadcast na prywatny kanał `user:{id}`; klient ma fallback w postaci refetchu po reconnect i pollingu co 3-5 s przy aktywnych zadaniach.

Bezpieczniki: sweeper w pg_cron co minutę (zadania po `deadline_at`: ostatni polling, potem `expired` i zwrot; blokady bez rozliczenia); retry tylko kroków idempotentnych; **failover wyłącznie przed przyjęciem zadania przez dostawcę** (5xx, 429, otwarty circuit breaker), nigdy po odrzuceniu przez moderację; tabela `model_routes` (model logiczny → lista tras z kosztem i stanem zdrowia).

| Opcja | Plus | Minus |
|---|---|---|
| **Vercel Workflow (rekomendacja)** | Ten sam deploy i preview co aplikacja, ok. 0,0006 USD za generację (ok. 30 zdarzeń, [szacunek 3 zdarzeń na krok][render-wf]) | Młody produkt, status GA nie potwierdzony |
| Tylko Postgres (pgmq + pg_cron + funkcje) | Zero nowych dostawców | Ręczne retry i timeouty |
| Trigger.dev / Inngest | Dojrzała obserwowalność i kolejki per użytkownik | Osobny deploy, 50-99 USD/mies. |

[wnioskowanie]

### (b) Storage i dostarczanie mediów

| Opcja | Storage / GB-mies. | Egress / GB | Ocena |
|---|---|---|---|
| Supabase Storage | 0,0213 | 0,09 / 0,03 | Wygodne RLS, drogie przy mediach |
| Vercel Blob | 0,023 | 0,05 | Proste, bez przewagi kosztowej |
| **Cloudflare R2** | 0,015 | **0** | API S3, presigned URL; operacje 4,50 / 0,36 USD za 1M ([przegląd][r2]) |
| Bunny Storage + CDN | 0,01 | 0,01 | Firma z UE, tokeny na CDN, Bunny Stream do HLS ([cennik][bunny]) |

Rekomendacja: **R2 od pierwszego dnia**, trzy buckety (`uploads-private`, `outputs-private`, `public`), w bazie tylko `bucket + key`, nigdy pełny URL. Prywatne zasoby przez krótkie presigned GET, galeria przez własną subdomenę z cache. [wnioskowanie] Domena dla R2 musi być strefą w Cloudflare, a presigned URL nie działają na domenie własnej. [niepewne]

Wideo: klipy 5-15 s jako **MP4 z `faststart`** i range requests; HLS (Mux ok. 0,0008 USD/min, Cloudflare Stream 1 USD/1000 min dostarczonych i 5 USD/1000 min przechowywanych, Bunny Stream, wg [porównania][video-cost]) dopiero przy treściach powyżej minuty. [wnioskowanie] Miniatury: 2-3 stałe warianty WebP generowane przy ingest; transformacje w locie w Supabase kosztowałyby ok. 700 USD za 140k obrazów. [wnioskowanie]

### (c) Przetwarzanie mediów

| Gdzie | Ocena |
|---|---|
| Supabase Edge Functions | Odpada (2 s CPU, brak sharp) [zweryfikowane] |
| Funkcja Vercel + `sharp` | Dobre dla obrazów [wnioskowanie] |
| Funkcja Vercel + `ffmpeg-static` | Mieści się (ok. 76 MB z 250 MB), ale Vercel odradza i proces ma dostęp do sekretów ([analiza][ffmpeg-vercel]) |
| **Vercel Sandbox** | Izolowana mikro-VM, `apt-get install ffmpeg` zamrożone w snapshocie, sieć `deny-all`; ok. 10 USD za 6k klipów [wnioskowanie] |
| Trigger.dev | Dobre, jeśli i tak jest orkiestratorem |
| Remotion | Oficjalny render w Vercel Sandbox; darmowe do 3 pracowników ([docs][remotion-sbx], [licencja][remotion-lic]). Na później, do szablonów reklam |
| Hostowane API ffmpeg, Modal, Cloudflare Containers | Nie zweryfikowane [niepewne] |

Rekomendacja: sharp w kroku workflow dla obrazów; cały ffmpeg (poster, probe, trim, concat, mux audio, znak wodny) w Vercel Sandbox. [wnioskowanie]

### (d) Upload mediów referencyjnych

1. Serwer wydaje presigned PUT po sprawdzeniu planu, deklarowanego MIME i rozmiaru; plik idzie prosto do R2. Pliki powyżej ok. 100 MB: multipart S3 przez Uppy.
2. `complete`: HEAD obiektu, magic bytes, `ffprobe` w sandboxie, przekodowanie obrazu przez sharp (usuwa EXIF/GPS, limit megapikseli), SHA-256.
3. Moderacja NSFW/CSAM zanim zasób stanie się referencją: `pending → clean | rejected`.
4. Import z URL tylko z ochroną przed SSRF.

Klasyczny antywirus ma małą wartość po przekodowaniu; realne ryzyka to treści nielegalne, twarze osób trzecich i exploity dekoderów, stąd izolacja. [wnioskowanie] Wybór dostawcy moderacji: [niepewne].

### (e) Model wielodostępny i RLS

- `workspaces` (personal tworzony przy rejestracji, team później), `workspace_members(role)`; **każdy wiersz biznesowy ma `workspace_id`**, a portfel kredytów należy do workspace.
- Polityki: `workspace_id in (select private.user_workspace_ids())`, funkcja `security definer stable`, `(select auth.uid())`, indeksy i `TO authenticated`, zgodnie z [zaleceniami wydajności RLS][s-rls]. [zweryfikowane]
- Ledger, salda, przejścia stanów i koszty dostawców: zero polityk zapisu dla klienta, tylko RPC i klucz secret w modułach `server-only`.
- Galeria publiczna jako osobna tabela `posts` z bezpiecznymi kolumnami dla roli `anon`; `generations` nigdy nie jest publiczne. [wnioskowanie]

### (f) Rate limiting i nadużycia

1. Brzeg: Vercel Firewall (reguły i rate limit per IP), BotID Basic na formularzach, Deep Analysis tylko przy rejestracji i odbiorze darmowych kredytów.
2. Auth: CAPTCHA Supabase, potwierdzony e-mail; anonimowi bez płatnych modeli.
3. Aplikacja: `checkRateLimit` z kluczem `workspaceId`.
4. **Limity biznesowe w Postgres** przy submit: równoległość per plan, dzienny limit darmowych generacji, blokada kredytów.
5. Wydatki: dzienny limit per workspace, globalny kill switch, budżety kluczy AI Gateway, osobne klucze per środowisko.

Główny wektor to farmienie darmowych kredytów na wielu kontach. [wnioskowanie]

### (g) Obserwowalność i koszt generacji

- Sentry (błędy, tracing) i PostHog w chmurze UE (lejki, replay, flagi). Cenniki nie sprawdzone. [niepewne]
- Logi z `generation_id`, `workspace_id`, `provider_request_id`.
- Na `generations`: `credits_held`, `credits_charged`, `provider`, `route_id`, `price_snapshot`, `provider_cost_usd`, `storage_bytes`, czasy etapów. Dzienna rekoncyliacja z raportami dostawców. Alerty: odsetek błędów per trasa, p95, liczba zadań zawieszonych, wydatek dzienny kontra przychód. [wnioskowanie]

### (h) Search i feed galerii

Postgres wystarcza do ok. miliona postów: paginacja keyset po `(score, id)`, `trending_score` liczony w pg_cron, `tsvector` + GIN + `pg_trgm`, liczniki zdenormalizowane. Semantyka: pgvector `halfvec` z indeksem HNSW ([docs][s-embed]). Feed jest wspólny dla wszystkich, więc `"use cache"` z tagami. Typesense/Meilisearch dopiero przy potrzebie facetingu. [wnioskowanie; silniki zewnętrzne niepewne]

### (i) i18n

next-intl z segmentem `[locale]` (pl, en), negocjacja języka w `proxy.ts`, ICU (polskie formy mnogie), tłumaczenia presetów w tabeli `preset_translations`, hreflang i sitemap per język. Wersja next-intl i zgodność z Cache Components: [niepewne].

### (j) Testy i CI/CD

- Vitest dla cen, kredytów i maszyny stanów; **pgTAP dla RLS i niezmienników ledgera**.
- **Mock provider** (zwraca próbkę i woła webhook) jako domyślny w dev, preview i E2E.
- Playwright na preview: rejestracja, zakup w trybie testowym, generacja, publikacja.
- GitHub Actions: lint, typecheck, testy, `supabase db push` przed promocją; migracje expand/contract.
- Baza dla preview: lokalny stack plus jeden projekt staging (ok. 10 USD/mies.); Branching per PR tylko dla ryzykownych migracji, bo jest w becie i poza Spend Cap. [wnioskowanie]

### (k) Mobile

PWA na start (instalacja, Web Push, share target, checkout webowy bez prowizji sklepów). Furtka do Expo: logika za HTTP route handlers z kontraktem zod (Server Actions nie są API dla klienta natywnego), presigned upload, Supabase Auth z PKCE. [wnioskowanie; stan Expo niepewne]

## 3. Rekomendowany stack

Założenia [wnioskowanie]: 1k MAU = 20k generacji, 70 GB nowych mediów, 350 GB transferu; 10k MAU = 200k generacji, ok. 4 TB narastająco po pół roku, 4-5 TB transferu. Bez inferencji, opłat płatniczych i podatków.

| Komponent | Wybór | Dlaczego | 0 MAU | 1k MAU | 10k MAU |
|---|---|---|---|---|---|
| Framework | Next.js 16.4, React 19, TypeScript | Aktualna linia, Cache Components, `proxy.ts` | 0 | 0 | 0 |
| Hosting | Vercel Pro, `fra1` (Hobby tylko na etap budowy) | Konto już jest; do 800 s | 0-20 | 20-40 | 100-250 |
| Baza, Auth, Realtime | Supabase Pro, region UE | RLS, pg_cron, pgmq, brak pauzy | 0-25 | 25-35 | 75-200 |
| Orkiestracja | Vercel Workflow + sweeper pg_cron | Jeden deploy, trwałe kroki i webhooki | 0 | ok. 11 | ok. 120 |
| Media | Cloudflare R2 + subdomena | Zero egress, API S3 | 0 | 1-6 | 60-90 |
| Przetwarzanie | sharp + Vercel Sandbox (ffmpeg) | Izolacja, płatność za CPU | 0 | ok. 10 | ok. 100 |
| Modele | Adaptery fal, AI Gateway, Replicate | Trasy per model, failover | poza tabelą | poza tabelą | poza tabelą |
| Anty-abuse | Vercel Firewall, BotID, limity w Postgres | Bez nowego dostawcy | 0 | 1-10 | 10-40 |
| Moderacja | API moderacji (do wyboru) | Wymóg prawny i dostawców | 0 | 0-20 | 50-200 [niepewne] |
| Błędy | Sentry | Standard dla Next.js | 0 | 0-29 | 29-80 [niepewne] |
| Analityka, flagi | PostHog EU | Jedno narzędzie | 0 | 0 | 0-100 [niepewne] |
| E-mail | Własny SMTP w Supabase Auth ([docs][s-smtp]) | Dostarczalność | 0 | 0-20 | 20-40 [niepewne] |
| Search | Postgres FTS + pgvector | Wystarcza do ok. 1M postów | 0 | 0 | 0 |
| CI/CD | GitHub Actions, preview Vercel, staging Supabase | Tani i przewidywalny | 0 | ok. 10 | 10-20 |
| Mobile | PWA | Bez prowizji sklepów | 0 | 0 | 0 |
| **Razem (USD/mies.)** | | | **0-45** | **ok. 80-190** | **ok. 570-1250** |

## 4. Decyzje drogie do odwrócenia

1. **`workspace_id` na każdej tabeli od pierwszej migracji.**
2. **Ledger kredytów**: append-only, blokady, jednostki całkowite.
3. **Schemat kluczy obiektów i dostawca storage**; w bazie klucze, nie URL-e.
4. **Domena produkcyjna i Supabase Auth**: passkeys są związane z RP ID, OAuth z redirect URI, a identyfikatory użytkowników trafiają do każdego FK.
5. **Region**: Supabase w UE i funkcje Vercel w `fra1`; zmiana regionu bazy to migracja.
6. **Schemat `generations` niezależny od dostawcy** (model logiczny kontra trasa, wersjonowane parametry, osobna tabela `assets`) oraz presety jako dane.
7. **Powierzchnia API**: HTTP + zod od początku, nie same Server Actions.
8. **Routing i18n i permalinki galerii** (SEO).
9. **Model moderacji i dziennik audytu** z retencją.
10. **Identyfikatory**: UUIDv7 wewnątrz, krótkie ID publiczne.

Łatwe do odwrócenia, jeśli są za interfejsem: orkiestrator, dostawca modeli, Sentry/PostHog, silnik wyszukiwania.

## 5. Czego nie udało się zweryfikować

- Status GA Vercel Workflow, max sesja Sandbox na Pro, limit 4,5 MB body, zakaz użycia komercyjnego na Hobby.
- Cenniki Sentry, PostHog, e-mail, Modal, Cloudflare Containers, moderacji; aktualne wersje next-intl i Expo.
- Szczegóły R2 (własna domena, presigned URL) i integracji Supabase-Vercel dla branchingu.

## Źródła

Next.js i AI SDK: [Next.js 16.4][next164], [Next.js 16][next16], [Releasebot][releasebot], [VersionLog][versionlog], [AI SDK 7][aisdk7], [AI SDK docs][aisdk-docs].

Vercel: [Fluid compute][v-fluid], [maxDuration][v-duration], [limity funkcji][v-limits], [vercel.ts][v-ts], [Flat Rate CDN][v-flatcdn], [przegląd cennika][usagepricing], [Workflows][v-wf], [Workflow pricing][v-wf-price], [Render o Workflows][render-wf], [Queues][v-queues], [Queues API][v-queues-api], [Schedules][v-sched], [Blob pricing][v-blob], [Sandbox][v-sbx], [Sandbox firewall][v-sbx-fw], [Sandbox limity Hobby][v-sbx-harbor], [Sandbox pricing (wtórne)][sbx-price], [AI Gateway wideo][v-gw-video], [AI Gateway obraz][v-gw-image], [Veo changelog][v-gw-veo], [budżety][v-gw-budget], [BotID][v-botid], [WAF rate limiting][v-waf], [Rate limiting SDK][v-waf-sdk].

Supabase: [billing][s-billing], [billing FAQ][s-faq], [pauzowanie Free][s-freepause], [okno przywracania][s-pause], [limity plików][s-filelimits], [resumable uploads][s-tus], [egress][s-egress], [image transformations][s-img], [Realtime limits][s-rt], [statusy funkcji][s-features], [Edge Functions limits][s-fn], [passkeys][s-passkeys], [anonymous sign-ins][s-anon], [Queues][s-queues], [pgmq + pg_cron + pgvector][s-embed], [branching][s-branch], [RLS][s-rls], [custom SMTP][s-smtp].

Pozostałe: [Inngest][inngest], [Trigger.dev limits][trigger], [Trigger.dev pricing][trigger-price], [QStash][qstash], [Upstash Workflow][upwf], [Cloudflare Workers pricing][cf-workers], [R2][r2], [Bunny][bunny], [koszty wideo][video-cost], [ffmpeg na Vercel][ffmpeg-vercel], [Remotion + Sandbox][remotion-sbx], [licencja Remotion][remotion-lic].

[next164]: https://nextjs.org/blog/next-16-4
[next16]: https://nextjs.org/blog/next-16
[releasebot]: https://releasebot.io/updates/vercel/next-js
[versionlog]: https://versionlog.com/nextjs/16/
[aisdk7]: https://vercel.com/blog/ai-sdk-7
[aisdk-docs]: https://vercel.com/docs/ai-sdk
[v-fluid]: https://vercel.com/docs/fluid-compute
[v-duration]: https://vercel.com/docs/functions/configuring-functions/duration
[v-limits]: https://vercel.com/docs/functions/limitations
[v-ts]: https://vercel.com/docs/project-configuration/vercel-ts
[v-flatcdn]: https://vercel.com/changelog/flat-rate-cdn-is-now-ga-for-pro-teams
[usagepricing]: https://www.usagepricing.com/blueprint/vercel
[v-wf]: https://vercel.com/docs/workflows/concepts
[v-wf-price]: https://vercel.com/docs/workflows/pricing
[render-wf]: https://render.com/articles/render-workflows-vs-vercel-workflows
[v-queues]: https://vercel.com/docs/queues
[v-queues-api]: https://vercel.com/docs/queues/api
[v-sched]: https://vercel.com/docs/schedules/migrate-from-cron-jobs
[v-blob]: https://vercel.com/docs/vercel-blob/usage-and-pricing
[v-sbx]: https://vercel.com/docs/sandbox/working-with-sandbox
[v-sbx-fw]: https://vercel.com/docs/sandbox/concepts/firewall
[v-sbx-harbor]: https://vercel.com/docs/sandbox/ecosystem/harbor
[s-freepause]: https://supabase.com/docs/guides/platform/free-project-pausing
[sbx-price]: https://lizard.build/blog/vercel-sandbox-pricing
[v-gw-video]: https://vercel.com/docs/ai-gateway/modalities/video-generation
[v-gw-image]: https://vercel.com/docs/ai-gateway/sdks-and-apis/openai-chat-completions/image-generation
[v-gw-veo]: https://vercel.com/changelog/veo-video-models-on-ai-gateway
[v-gw-budget]: https://vercel.com/docs/ai-gateway/observability-and-spend/budgets
[v-botid]: https://vercel.com/docs/botid
[v-waf]: https://vercel.com/docs/vercel-firewall/vercel-waf/rate-limiting
[v-waf-sdk]: https://vercel.com/docs/vercel-firewall/vercel-waf/rate-limiting-sdk
[s-billing]: https://supabase.com/docs/guides/platform/billing-on-supabase
[s-faq]: https://supabase.com/docs/guides/platform/billing-faq
[s-pause]: https://supabase.com/docs/guides/platform/upgrading
[s-filelimits]: https://supabase.com/docs/guides/storage/uploads/file-limits
[s-tus]: https://supabase.com/docs/guides/storage/uploads/resumable-uploads
[s-egress]: https://supabase.com/docs/guides/platform/manage-your-usage/egress
[s-img]: https://supabase.com/docs/guides/storage/serving/image-transformations
[s-rt]: https://supabase.com/docs/guides/realtime/limits
[s-features]: https://supabase.com/docs/guides/getting-started/features
[s-fn]: https://supabase.com/docs/guides/functions/limits
[s-passkeys]: https://supabase.com/docs/guides/auth/passkeys
[s-anon]: https://supabase.com/docs/guides/auth/auth-anonymous
[s-queues]: https://supabase.com/docs/guides/queues
[s-embed]: https://supabase.com/docs/guides/ai/automatic-embeddings
[s-branch]: https://supabase.com/docs/guides/platform/manage-your-usage/branching
[s-rls]: https://supabase.com/docs/guides/database/postgres/row-level-security
[s-smtp]: https://supabase.com/docs/guides/auth/auth-smtp
[inngest]: https://hokai.io/hub/tools/inngest
[trigger]: https://trigger.dev/docs/limits
[trigger-price]: https://www.usagepricing.com/blueprint/trigger-dev
[qstash]: https://upstash.com/pricing/qstash
[upwf]: https://upstash.com/pricing/workflow
[cf-workers]: https://developers.cloudflare.com/workers/platform/pricing/
[r2]: https://upstash.com/kb/cloudflare-r2-pricing-in-2026-storage-operations-and-real-monthly-bills
[bunny]: https://bunny.net/pricing/
[video-cost]: https://www.forasoft.com/blog/article/how-to-estimate-the-server-cost-for-a-video-platform-249
[ffmpeg-vercel]: https://verygoodffmpeg.com/blog/vercel-ffmpeg-video-processing-serverless-functions-limits-2026
[remotion-sbx]: https://www.remotion.dev/docs/vercel-sandbox
[remotion-lic]: https://www.remotion.dev/docs/license
