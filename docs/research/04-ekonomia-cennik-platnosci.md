# 04 - Ekonomia, cennik, płatności i ledger kredytów (stan na 2026-11-13)

Tagi: **[zweryfikowane]** = jest źródło, **[wnioskowanie]** = mój wniosek lub wyliczenie, **[niepewne]** = źródła sprzeczne albo brak potwierdzenia. Wszystkie ceny w USD netto, o ile nie zaznaczono inaczej.

## TL;DR

- **Higgsfield sprzedaje kredyt za ok. 0,033-0,070 USD** (Ultra roczny 99 USD / 3 000 kr. do Starter 19 USD / 270 kr.), a w promocji 11.11 nawet za 0,022 USD (Ultra roczny 65 USD/mies.). Doładowania są droższe: 0,085 USD cennikowo, 0,05 USD w auto-refill.
- **Ceny detaliczne Higgsfield to ok. 50-75% cennikowych cen API** u agregatorów (Nano Banana Pro: 0,07-0,10 USD wobec 0,134-0,15 USD kosztu; Kling 3.0 5 s: 0,20-0,30 USD wobec 0,42 USD). Bez hurtowych rabatów, kapitału VC i breakage ten cennik jest nie do skopiowania. **Nowy gracz nie wygra ceną na flagowych modelach.**
- Realny model dla nowego gracza: kredyt przypięty do kosztu (ok. 0,0066 USD COGS na kredyt), plany 10 / 29 / 79 USD, marża brutto 25-34% przy pełnym wykorzystaniu i 40-60% przy typowym. Wkład na płacącego ok. **8,9 USD/mies.**, więc break-even to ok. 30 płacących przy 250 USD kosztów stałych i ok. 560 przy 5 000 USD.
- **"Unlimited" na modelach płatnych per generacja to ryzyko rzędu 190-235 USD na ciężkiego użytkownika tygodniowo.** Na start: brak unlimited albo tylko na najtańszych modelach, z kolejką 1 równoległej generacji.
- **Płatności: Stripe bezpośrednio** (Checkout + Billing + Tax + Radar, BLIK i P24, OSS w polskim urzędzie). Merchant-of-record (Paddle, Polar, Creem) kosztują podobnie dla kart spoza EOG, ale ich regulaminy zakazują face swap, deepfake i klonowania głosu, czyli części funkcji klasy Higgsfield.
- **Ledger**: własny, append-only, double-entry w Postgres (Supabase), z rezerwacją przy zgłoszeniu zadania i rozliczeniem lub zwrotem po webhooku. Stripe ma być tylko kasą, nie źródłem prawdy o saldzie.

## 1. Cennik Higgsfield

Źródło pierwotne: konfiguracja cennika zwrócona przez oficjalny konektor MCP Higgsfield (odczyt 2026-11-13; konektor pokazuje tylko plany dostępne dla danego konta, więc zwrócił kartę Ultra, a ceny paczek zawierają rabat planu). Strony higgsfield.ai nie dało się pobrać bezpośrednio (host poza dozwoloną siecią sesji), więc Starter i Plus opieram na serwisach trzecich.

### 1.1 Plany i efektywna cena kredytu

| Plan | Cena / mies. | Kredyty / mies. | USD za kredyt | Status |
|---|---|---|---|---|
| Free | 0 | 0 (ograniczone obrazy, znak wodny, bez wideo) | - | [niepewne] |
| Starter | 19 | 270 | 0,070 | [zweryfikowane, serwisy trzecie] |
| Plus mies. / roczny | 59 / 47 | 1 200 | 0,049 / 0,039 | [zweryfikowane, serwisy trzecie] |
| Ultra mies. | 129 | 3 000 | 0,043 | [zweryfikowane: MCP] |
| Ultra roczny (regularnie) | 99 | 3 000 | 0,033 | [zweryfikowane, serwisy trzecie] |
| Ultra roczny, promocja 11.11 | 65 | 3 000 | 0,022 | [zweryfikowane: MCP] |
| Doładowanie cennikowe | 42,50-340 za 500-4 000 kr. | - | 0,085 | [zweryfikowane: MCP] |
| Doładowanie z rabatem planu | 29,41 / 55,56 / 105,26 / 210,53 | 500 / 1 000 / 2 000 / 4 000 | 0,059-0,053 | [zweryfikowane: MCP] |
| Auto-refill | 20-300 | 20 kr. za 1 USD | 0,050 | [zweryfikowane: MCP] |

- Starter 19 i Plus 59 USD raportowane są od października 2026 ([heygen](https://www.heygen.com/blog/higgsfield-pricing), [hermoso](https://hermoso.ai/pricing/higgsfield/), [krea](https://www.krea.ai/blog/higgsfield-pricing-explained-2026-unlimited-credits-and-real-monthly-costs)); wcześniej 15 i 49 USD, co nadal podaje własny blog Higgsfield ([blog](https://higgsfield.ai/blog/higgsfield-pricing-explained)). Dokładna data podwyżki [niepewne].
- Jeden serwis raportuje z 4.11.2026 inną drabinkę Basic 9 / Pro 29 / Max 79 USD (120 / 600 / 1 800 kr.) ([versely](https://www.versely.studio/blog/higgsfield-pricing-2026)). Konektor MCP z 13.11 pokazuje Ultra 3 000 kr. za 129 USD, więc traktuję to jako test A/B lub błąd [niepewne].
- Promocja 11.11 (11-15.11.2026): rabat do 60%, do 60 dni unlimited na modelach obrazu i do 14 dni na Seedance 2.5 [zweryfikowane: MCP]. Konfiguracja zawiera kilkanaście takich akcji od lipca 2026 oraz okresy 18 i 24 miesiące, czyli promocja i długi prepaid są stałym elementem cennika [wnioskowanie].
- Kredyty z planu nie przechodzą na kolejny okres; doładowania i auto-refill wygasają po 90 dniach, auto-refill ma próg 300 kredytów [zweryfikowane: MCP]. Część serwisów podaje 365 dni dla paczek ([krater](https://krater.ai/blog/higgsfield-pricing)) [niepewne].
- Team: ok. 79 USD za miejsce (65 rocznie), 1 000 kr. na miejsce; Scale ok. 215 / 150 USD. Jeden zrzut cennika już ich nie pokazuje ([camclo3d](https://camclo3d.com/blog/higgsfield-pricing)) [niepewne]. Kredyty zespołu kupuje tylko właściciel workspace [zweryfikowane: MCP].
- Cennik regionalny: konfiguracja zwraca wyłącznie USD; nie znalazłem dowodu na ceny regionalne [niepewne].
- Operator płatności: Stripe (identyfikatory `price_...` w konfiguracji [zweryfikowane: MCP], [Stripe customer story](https://stripe.com/customers/higgsfield)) oraz Solidgate do zapobiegania sporom ([case study](https://solidgate.com/case-studies/how-higgsfield-protects-subscription-revenue-with-solidgate/)) [zweryfikowane].

### 1.2 Koszt typowej generacji

| Generacja | Kredyty | USD przy Plus mies. (0,049) | USD przy Ultra rocznym (0,033) | Status |
|---|---|---|---|---|
| Tani obraz (3 000 kr. = ok. 12 000 obrazów) | ok. 0,25 | 0,012 | 0,008 | [zweryfikowane: MCP] |
| Nano Banana Pro (3 000 kr. = 1 500 generacji) | 2 | 0,098 | 0,066 | [zweryfikowane: MCP] |
| Kling 3.0, 720p / 5 s (3 000 kr. = ok. 500 wideo) | ok. 6; serwisy trzecie 7,5-10 | 0,30-0,49 | 0,20-0,33 | [zweryfikowane: MCP] / [niepewne] |
| Seedance 2.0, 720p / 5 s | ok. 22 | 1,08 | 0,73 | [zweryfikowane, serwisy trzecie] |
| Seedance 2.5, 720p / 5 s | ok. 35 | 1,72 | 1,16 | [niepewne] |
| Veo 3.1, 4 s (Fast: ok. 16) | ok. 40 | 1,97 | 1,32 | [niepewne] |
| Generacja postaci (3 000 kr. = ok. 100) | ok. 30 | 1,47 | 0,99 | [zweryfikowane: MCP] |
| Upscale (Topaz) | brak danych | - | - | [niepewne] |

Źródła wartości z serwisów trzecich: [wireflow](https://www.wireflow.ai/blog/higgsfield-ai-pricing), [toolcolumn](https://www.toolcolumn.com/learn/higgsfield-credits-explained), [aliteq](https://aliteq.com/which-higgsfield-model-to-use).

### 1.3 Jak ograniczone jest "unlimited"

- Zakres to konkretny model i rozdzielczość, nie cała platforma: 365 dni na Seedream 5.0 Lite, Flux.2 Pro (1K), Seedream 4.5, Nano Banana, Kling O1 Image i GPT Image; 7 dni na Nano Banana 2 i Nano Banana Pro (1K/2K), a w planie rocznym także Kling 3.0 (720p / 5 s) [zweryfikowane: MCP].
- Każdy pakiet ma termin zakupu ("Buy until: Nov 14") i działa tylko w aplikacji web [zweryfikowane: MCP]. MCP, CLI, Canvas i API zawsze zużywają kredyty ([aliteq](https://aliteq.com/higgsfield-unlimited-explained)) [zweryfikowane].
- Modele własne (Soul V2, Cinema) to nie unlimited, lecz 5 000 lub 10 000 darmowych generacji [zweryfikowane: MCP].
- Kolejka relaxed: 1 obraz, 1 wideo i 1 audio jednocześnie ([blog Higgsfield](https://higgsfield.ai/blog/credits-vs-unlimited-ai-video-generation), [aiimagetovideo](https://aiimagetovideo.pro/blog/higgsfield-unlimited/)) [zweryfikowane, serwisy trzecie].

### 1.4 Free, trial, zwroty

- Free: 0 kredytów miesięcznie, znak wodny ([krea](https://www.krea.ai/blog/what-is-higgsfield-ai-pricing-free-plan-and-alternatives-in-2026), [novoads](https://novoads.ai/en/blog/is-higgsfield-free)) [niepewne w szczegółach].
- Trial: 3 dni planu Plus za 0 USD, wymagana karta, automatyczne obciążenie po trialu [zweryfikowane: opis narzędzia MCP]. Pozycja `freegen_card_bonus`: 40 kredytów ważnych 90 dni, z nazwy bonus po podaniu karty [niepewne co do interpretacji].
- Zwrot tylko przy pierwszym zakupie, w krótkim oknie (raportowane 7 dni) i bez zużytych kredytów. Powtarzające się skargi dotyczą domyślnie zaznaczonego planu rocznego ([help center](https://higgsfield.ai/creator-hub/help-center/refunds/why-didnt-i-receive-a-refund-after-canceling-my-subscription), [mindstudio](https://www.mindstudio.ai/blog/higgsfield-subscription-cancellation-complaints)) [zweryfikowane].

## 2. Porównywalne platformy

| Platforma | Wejście | Środek | Góra | Free / uwagi |
|---|---|---|---|---|
| Freepik (pod marką Magnific) | Premium 20 (14,50 rocznie) | Premium+ 45 (33,75), unlimited na ok. 30 modelach | Pro 110 (82,50) | Essential ok. 5-9 [niepewne] |
| Krea | Basic 9 / 5 000 jedn. | Pro 35 / 20 000 | Max 105 / 60 000 [niepewne: 70] | 100 jedn. dziennie |
| OpenArt | Starter 14 / 4 000 | Plus 34 / 12 000, Pro 56 / 24 000 | Wonder 240 / 106 000 | add-on 15 USD / 5 000 kr., przechodzi dalej |
| Leonardo | Essential 12 / 8 500 | Premium 30 / 25 000 | Ultimate 60 / 60 000 | 150 tokenów dziennie; bank rollover 3x |
| Runway | Standard 15 / 625 | Pro 35 / 2 250 | Unlimited 95 (tryb Explore) | 125 kredytów jednorazowo |
| Kling (własna aplikacja) | Standard 10 (8,80) / 660 | Pro 37 / 3 000 | Premier 92 / 8 000, Ultra 180 / 26 000 | dzienne kredyty już tylko dla subskrybentów [niepewne] |
| Pika | 10 / 700 | 35 / 2 300 | 95 / 6 000 | free bez kredytów [niepewne] |
| Luma | Plus 30 / 10 000 | Pro 90 / 40 000 | Ultra 300 / 150 000 | plan free wycofany w 2026 |

Źródła: [renderahouse Freepik](https://www.renderahouse.com/blog/freepik-pricing), [renderahouse Krea](https://www.renderahouse.com/blog/krea-ai-pricing), [voyager OpenArt](https://voyager.so/blog/openart-pricing), [renderahouse Leonardo](https://www.renderahouse.com/blog/leonardo-ai-pricing), [pixara Runway](https://www.pixara.ai/blogs/runway-pricing), [kling.ai](https://kling.ai/app/membership/membership-plan?r=26), [aitoolsbakery](https://aitoolsbakery.com/blog/ai-video-generator-pricing-compared/), [kavel](https://www.kavel.ai/blog/best-free-ai-video-generators-2026) [zweryfikowane na serwisach trzecich; przed publikacją cennika sprawdzić strony oficjalne].

Wnioski [wnioskowanie]: progi cenowe rynku to 9-15 / 29-37 / 79-105 USD, rabat roczny 20-27%, a darmowe plany w 2026 r. kurczą się u wszystkich (Luma, Pika, Kling, Higgsfield).

## 3. Unit economics

### 3.1 Koszt API (COGS) reprezentatywnych generacji

| Generacja | Cena API | COGS | Źródło |
|---|---|---|---|
| FLUX.2 [pro], 1 MP | 0,03 za pierwszy MP | 0,03 | [fal](https://fal.ai/models/fal-ai/flux-2-pro) |
| Seedream 5.0 Lite | 0,035 za obraz | 0,035 | [fal learn](https://fal.ai/learn/tools/nano-banana-vs-seedream) |
| GPT Image 2, medium 1024 | 0,053 | 0,053 | [fal learn](https://fal.ai/learn/tools/gpt-image-2-vs-nano-banana-2) |
| Nano Banana 2, 1K | 0,08 fal; 0,067 Google | 0,07-0,08 | [fal learn](https://fal.ai/learn/tools/gpt-image-2-vs-nano-banana-2), [veonano](https://veonano.com/blog/posts/nano-banana-pricing) |
| Nano Banana Pro, 1K/2K | 0,15 fal; 0,134 Google | 0,134-0,15 | [teamday](https://www.teamday.ai/blog/fal-ai-pricing-2026), [usagebox](https://usagebox.com/articles/nano-banana-pro-api-pricing-cost-per-image-2026) |
| Kling 3.0 std, 5 s bez audio | 0,084 za s | 0,42 | [fal learn](https://fal.ai/learn/tools/seedance-2-0-vs-kling-3-0) |
| Kling 3.0 pro, 5 s z audio | 0,168 za s | 0,84 | jw. |
| Kling 4.0, 720p / 5 s | 0,157 za s (resellerzy 0,11-0,126) | 0,785 | [aireiter](https://aireiter.com/blog/kling-4-0-api-pricing-fal-cost-vs-seedance-vidu), [argolink](https://argolink.io/en/blog/kling-4-0-api-pricing) |
| Veo 3.1 Fast, 4 s z audio | 0,15 za s (standard 0,40) | 0,60 (1,60) | [teamday](https://www.teamday.ai/blog/fal-ai-pricing-2026) |
| Seedance 2.0, 720p / 5 s z audio | 0,3034 za s (Fast 0,2419) | 1,52 (1,21) | [fal](https://fal.ai/models/bytedance/seedance-2.0/text-to-video) |
| Seedance 2.5, 720p / 5 s | 0,473 za s fal; ok. 0,23 BytePlus | 2,37 (ok. 1,15) | [kreatorflow](https://kreatorflow.ai/ai-video-api-pricing), [mindstudio](https://www.mindstudio.ai/blog/seedance-2-5-review-pricing) |
| ElevenLabs TTS, 1 000 znaków | 0,08 (Flash 0,04) | 0,08 | [assemblyai](https://www.assemblyai.com/blog/tts-api-pricing) |

Wszystkie pozycje [zweryfikowane na serwisach trzecich lub stronach modeli fal]. Uwaga: endpointy Veo 3.1 na fal mają być wyłączone 17.11.2026, a wersje preview w Gemini API według jednego źródła już zamknięto ([teamday](https://www.teamday.ai/blog/fal-ai-pricing-2026)) [niepewne]. Wniosek: katalog modeli i tabela cen muszą być konfiguracją, nie kodem.

### 3.2 Co to mówi o marży Higgsfield

Stosunek ceny detalicznej Higgsfield do cennikowego kosztu API [wnioskowanie z tabel 1.2 i 3.1]:

| Generacja | Detal Higgsfield (Ultra roczny - Plus mies.) | COGS cennikowy | Detal / COGS |
|---|---|---|---|
| Nano Banana Pro | 0,066-0,098 | 0,134 | 49-73% |
| Kling 3.0, 5 s | 0,20-0,30 | 0,42 | 47-70% |
| Seedance 2.0, 5 s | 0,73-1,08 | 1,52 | 48-71% |
| Seedance 2.5, 5 s | 1,16-1,72 | 2,37 (fal) | 49-73% |
| Veo 3.1, 4 s | 1,32-1,97 | 1,60 | 83-123% |

Przy cenach cennikowych Higgsfield miałby ujemną marżę brutto przy pełnym wykorzystaniu, więc musi mieć rabaty hurtowe lub bezpośrednie umowy, subsydiować wzrost kapitałem (runda 400 mln USD przy wycenie 5,4 mld w sierpniu 2026) i zarabiać na breakage [wnioskowanie]. Firma sama przyznaje marże poniżej typowego SaaS ([sacra](https://sacra.com/research/higgsfield-at-230m-arr/), [saasrise](https://www.saasrise.com/deals/higgsfield-just-raised-400-million-at-a-54-billion-valuation-cdd69c44-9235-4423-9d67-487660520830)) [zweryfikowane].

### 3.3 Model dla nowego gracza

Założenia [wnioskowanie, do kalibracji na własnych danych]:

- Cena generacji w kredytach = zaokrąglone w górę `COGS w USD x 100 x M`. Mnożnik M: 2,0 dla tanich obrazów, audio i upscale; 1,5 dla obrazów premium; 1,4 dla wideo.
- Miks zużycia kredytów: 20% tanie obrazy, 20% obrazy premium, 60% wideo. Daje to średni COGS **0,0066 USD na kredyt**.
- Wykorzystanie kredytów (breakage to dopełnienie): Starter 60%, Creator 70%, Pro 80%. Twardych benchmarków brak; jedyna publikowana liczba to 5-15% niewykorzystanych kredytów prepaid bez podanego źródła ([agenticaipricing](https://www.agenticaipricing.com/how-to-prevent-credit-breakage-from-hurting-customer-trust/)) [niepewne], dlatego model musi być dodatni także przy 100%.
- Opłaty płatnicze: średnio 4,5% + 0,35 USD za transakcję (miks kart PL/EOG, BLIK i kart spoza EOG).

| Plan | Cena | Kredyty | USD / kr. | Marża brutto przy 100% | Wykorzystanie | COGS | Opłata | Wkład |
|---|---|---|---|---|---|---|---|---|
| Starter | 10 | 1 000 | 0,0100 | 33,8% | 60% | 3,97 | 0,80 | 5,23 (52%) |
| Creator | 29 | 3 200 | 0,0091 | 27,0% | 70% | 14,83 | 1,66 | 12,51 (43%) |
| Pro | 79 | 9 000 | 0,0088 | 24,6% | 80% | 47,66 | 3,91 | 27,43 (35%) |

Przykładowe ceny generacji w tym modelu: FLUX.2 pro 6 kr., Nano Banana Pro 23 kr., Kling 3.0 std 5 s 59 kr., Kling 4.0 5 s 110 kr., Seedance 2.0 5 s 213 kr. Przy 0,0088-0,010 USD za kredyt klip Kling 3.0 kosztuje 0,52-0,59 USD, czyli 1,1-3 razy więcej niż w Higgsfield, a Nano Banana Pro 0,20-0,23 USD, czyli 2-3,5 raza więcej [wnioskowanie]. Rabat roczny 20% obniża marżę przy 100% wykorzystania do 6-17%, więc nie powinien być większy.

### 3.4 Ile kosztuje "unlimited"

Liczby użycia to założenia; kolejka 1 równoległej generacji [wnioskowanie].

| Oferta | Użytkownik typowy | Użytkownik ciężki | Sufit techniczny |
|---|---|---|---|
| 7 dni Nano Banana Pro (0,134-0,15) | 20 dziennie: 19-21 USD | 200 dziennie: 188-210 USD | ok. 2 880 dziennie: 2 700-3 000 USD |
| 7 dni Kling 3.0, 720p / 5 s (0,42) | 8 dziennie: 24 USD | 80 dziennie: 235 USD | ok. 480 dziennie: 1 400 USD |
| 365 dni taniego modelu obrazu (0,03-0,04) | 5 dziennie: 55-73 USD rocznie | 100 dziennie: 1 100-1 460 USD rocznie | - |

Roczny Plus daje Higgsfield 564 USD, więc nawet tani unlimited na 365 dni jest ujemny dla ciężkich użytkowników bez rabatów hurtowych. Bezpieczny wariant dla nowego gracza to tryb relaxed tylko na modelach kosztujących do ok. 0,005 USD za obraz, z 1 równoległą generacją i dziennym limitem fair use zapisanym w regulaminie.

### 3.5 Koszty stałe małego produktu (miesięcznie)

| Pozycja | Koszt | Uwagi |
|---|---|---|
| Vercel Pro | 20 | 1 miejsce, zawiera 20 USD kredytu na zużycie ([flexprice](https://flexprice.io/blog/vercel-pricing-breakdown)) |
| Supabase Pro | 25 | 8 GB bazy, 100 GB plików, 250 GB egress, 100 tys. MAU; nadwyżka egress 0,09 USD/GB ([activepieces](https://www.activepieces.com/blog/supabase-pricing-free-tier-limits-pro-costs-egress)) |
| Cloudflare R2 | 8-30 | 0,015 USD/GB, zerowy egress; 0,5-2 TB ([upstash](https://upstash.com/kb/cloudflare-r2-pricing-in-2026-storage-operations-and-real-monthly-bills)) |
| Resend Pro | 20 | ([resend](https://resend.com/pricing.md)) |
| Sentry Team | 26-29 | ([activepieces](https://www.activepieces.com/blog/sentry-pricing-2026-developer-team-business-plans)) |
| PostHog | 0 | 1 mln zdarzeń za darmo ([posthog](https://posthog.com/pricing.md)) |
| Kolejka zadań, domena, drobne | 10-30 | [wnioskowanie] |
| **Razem infrastruktura** | **ok. 110-160** | [wnioskowanie] |
| Księgowość z obsługą OSS | ok. 100-200 | [wnioskowanie] |

Media generowane trzymać w R2, nie w Supabase Storage ani za proxy Vercel: 1 TB ruchu wideo to ok. 68 USD nadwyżki egress w Supabase i 0 USD w R2 [wnioskowanie].

## 4. Rekomendowany cennik i break-even

- **Jednostka**: 1 kredyt to ok. 0,01 USD wartości detalicznej. Tabela cen generacji jest wersjonowana w bazie i liczona z COGS.
- **Plany**: Starter 10 USD / 1 000 kr., Creator 29 USD / 3 200 kr., Pro 79 USD / 9 000 kr., Team 39 USD za miejsce / 4 000 kr. we wspólnej puli (minimum 2 miejsca).
- **Rabat roczny**: 17-20%, kredyty przyznawane co miesiąc, nigdy 12 miesięcy z góry (ekspozycja na chargeback).
- **Paczki**: 1 000 kr. za 12 USD, 5 000 za 55 USD, 20 000 za 200 USD, ważne 12 miesięcy, tylko dla kont ze zweryfikowaną płatnością. Auto-refill z progiem i miesięcznym limitem kwoty.
- **Rollover**: kredyty z planu przechodzą dalej do limitu 1 miesięcznej puli. To tani wyróżnik wobec Higgsfield, który kasuje je co miesiąc.
- **Free odporny na nadużycia**: zero kredytów na wideo; 10 obrazów dziennie na najtańszym modelu (do 0,005 USD), znak wodny, galeria publiczna, 1 zadanie naraz. Jednorazowe 50 kredytów dopiero po weryfikacji karty (autoryzacja 0 USD, jeden bonus na odcisk karty).
- **Waluty**: baza kosztowa w USD. Trzy cenniki: USD (świat), EUR (strefa euro), PLN (Polska; BLIK działa tylko w PLN). Ceny dla konsumentów w UE pokazywać brutto z VAT. Kurs i zaokrąglenia PLN korygować kwartalnie.
- **Pozycjonowanie**: nie cena flagowych generacji, lecz niższy próg wejścia, PLN i BLIK, paczki ważne rok, rollover i presety pod konkretną niszę [wnioskowanie].

**Break-even** [wnioskowanie]. Miks płacących 55% Starter / 33% Creator / 12% Pro daje ARPU 24,55 USD i wkład 10,30 USD. Po odjęciu kosztu darmowych kont (25 darmowych na płacącego po 0,04 USD = 1,00 USD) i 3% COGS na nieudane generacje (0,38 USD) zostaje **ok. 8,9 USD na płacącego miesięcznie (36% ARPU)**.

| Koszty stałe / mies. | Potrzebni płacący |
|---|---|
| 250 USD (sama infrastruktura i księgowość) | ok. 29 |
| 1 000 USD (plus narzędzia i mały marketing) | ok. 113 |
| 5 000 USD (plus wynagrodzenie założyciela) | ok. 562 |
| 10 000 USD | ok. 1 124 |

Przy 100% wykorzystania wkład spada do ok. 3,8 USD i progi rosną 2,4 raza. Każde 10 punktów procentowych wyższego wykorzystania to ok. 1,8 USD mniej wkładu.

## 5. Płatności dla sprzedawcy z Polski

### 5.1 Stripe bezpośrednio

| Element | Stawka | Status |
|---|---|---|
| Karty EOG standard / premium | 1,5% / 1,9% + 1,00 zł | [zweryfikowane: [Stripe PL](https://stripe.com/en-pl/pricing)] |
| Karty międzynarodowe | 3,25% + 1,00 zł, plus 2% przy przewalutowaniu | [zweryfikowane: [Stripe PL](https://stripe.com/en-pl/pricing/local-payment-methods)] |
| BLIK | 1,6% + 1,00 zł | [zweryfikowane, serwisy trzecie: [paymentreview](https://paymentreview.com/blog/poland-card-blik-payment-fees-2026/)] |
| Przelewy24 | 1,9% + 1 zł albo 2,2% | [niepewne] |
| Billing | 0,7% wolumenu | [zweryfikowane: [flexprice](https://flexprice.io/blog/stripe-pricing-breakdown-2026)] |
| Tax | 0,5% transakcji; samo naliczanie, deklaracje osobno | [zweryfikowane: [Stripe support](https://support.stripe.com/questions/understanding-stripe-tax-pricing)] |
| Radar | Lite za darmo; płatne poziomy od 10 USD/mies. lub 0,05 USD za transakcję; zmiana cennika 22.01.2027 | [zweryfikowane: [Stripe support](https://support.stripe.com/questions/updates-to-radar-pricing-(january-2027))] |
| Spór (chargeback) | 20 EUR, bez zwrotu po wygranej | [niepewne: komunikat z 2023] |

- **BLIK cykliczny** działa w Stripe Billing od 2026 r.: tylko PLN, do 2 000 zł za transakcję, wymaga włączenia na koncie ([changelog](https://docs.stripe.com/changelog/dahlia/2026-04-22/stripe-billing-blik-recurring-payments), [changelog 09.2026](https://docs.stripe.com/changelog/endive/2026-09-30/blik-recurring-off-session-payments)) [zweryfikowane].
- **Adaptive Pricing**: przewalutowanie 2-4% płaci klient ([Stripe docs](https://docs.stripe.com/payments/checkout/localize-prices/adaptive-pricing)) [zweryfikowane].
- Koszt całkowity [wnioskowanie]: karta PL lub BLIK przy 119 zł to ok. 3,5%; karta z USA przy 29 USD to ok. 7,4% (3,25% + 2% + 0,7% + 0,5% + 1 zł).
- **Stripe Billing credits** rozliczają się przy finalizacji faktury dla cen metrowanych, a wariant real-time jest w private preview ([Stripe docs](https://docs.stripe.com/billing/subscriptions/usage-based/billing-credits)) [zweryfikowane]. Nie nadają się na autoryzację zadań w czasie rzeczywistym [wnioskowanie].

### 5.2 Merchant of record

| Dostawca | Opłata | Uwagi |
|---|---|---|
| Paddle | 5% + 0,50 USD | BLIK tylko jednorazowo, wymaga zgody ([Paddle docs](https://developer.paddle.com/concepts/payment-methods/blik)) |
| Lemon Squeezy | 5% + 0,50, plus 1,5% karty zagraniczne i 0,5% subskrypcje | przejęty przez Stripe, kierunek to Managed Payments ([dodopayments](https://dodopayments.com/blogs/lemonsqueezy-review)) |
| Polar | od 27.05.2026: 5% + 0,50 (plan darmowy) do 3,4% + 0,30 (400 USD/mies.), plus 1,5% karty zagraniczne i opłaty wypłat | wypłaty przez Stripe Connect ([dodopayments](https://dodopayments.com/blogs/polar-sh-review), [Polar docs](https://polar.sh/docs/merchant-of-record/supported-countries)) |
| Creem | 3,9% + 0,40 | skargi na blokady środków ([Trustpilot](https://www.trustpilot.com/review/creem.io?page=2)) |
| Stripe Managed Payments | opłaty Stripe + 3,5% | GA od 2026; dostępność dla firmy z Polski niepotwierdzona ([Stripe](https://stripe.com/managed-payments)) [niepewne] |

Stawki [zweryfikowane: [aliteq](https://aliteq.com/cheapest-merchant-of-record), [fintechspecs](https://fintechspecs.com/blog/merchant-of-record-fees-compared/)]. Przy 29 USD od klienta z USA: Paddle 1,95 USD, Creem 1,53 USD, Stripe bezpośrednio ok. 2,14 USD. MoR nie jest więc droższy poza EOG, ale jest o ok. 3 punkty procentowe droższy w Polsce i UE [wnioskowanie].

### 5.3 Ograniczenia dla biznesów generatywnych

- **Paddle** zakazuje face swap, deepfake obrazu i wideo, podszywania się głosem oraz generowania z cudzego wizerunku bez zgody ([Paddle help](https://www.paddle.com/help/start/intro-to-paddle/what-am-i-not-allowed-to-sell-on-paddle)) [zweryfikowane]. Doniesienia o odrzucaniu generatorów obrazu jako kategorii ([boathouse](https://www.boathouse.co/paddle-video-series-episode/34-aup-update-gen-ai)) [niepewne].
- **Polar** wyklucza treści dla dorosłych generowane przez AI, face swap, deepfake i klonowanie głosu ([Polar AUP](https://polar.sh/legal/acceptable-use-policy)) [zweryfikowane].
- **Creem** wymaga integracji własnego Moderation API dla produktów obrazu i wideo; zakazuje face swap i narzędzi typu nudify ([Creem docs](https://docs.creem.io/merchant-of-record/account-reviews/account-reviews)) [zweryfikowane].
- **Stripe** zakazuje treści dla dorosłych, także generowanych przez AI; zwykła generacja obrazu i wideo jest dopuszczalna, ale z wyższym ryzykiem przeglądu konta ([Stripe](https://stripe.com/legal/restricted-businesses)) [zweryfikowane co do zakazu; reszta to wnioskowanie].

Wniosek: funkcje klasy Higgsfield (zamiana twarzy i postaci, lipsync, klonowanie głosu) są wprost sprzeczne z regulaminami MoR. Stripe bezpośrednio z twardą polityką treści (bez NSFW, oświadczenie o zgodzie na wizerunek, moderacja wejścia i wyjścia) to jedyna spójna ścieżka [wnioskowanie].

### 5.4 VAT

- Usługi elektroniczne B2C do innych krajów UE: do 10 000 EUR rocznie można rozliczać polski VAT; powyżej obowiązuje VAT kraju konsumenta przez OSS (kwartalna VIU-DO) ([przelewy24](https://www.przelewy24.pl/blog/vat-oss-w-e-commerce-kompletny-przewodnik-dla-sprzedawcow), [plumm](https://plumm.pl/wiedza/vat-oss)) [zweryfikowane].
- Zwolnienie podmiotowe to 240 000 zł od 1.01.2026, ale nie rozciąga się na inne kraje UE ([amavat](https://amavat.pl/nowy-limit-zwolnienia-z-vat-a-sprzedaz-internetowa-kiedy-limit-krajowy-nie-chroni-przed-vat-za-granica/)) [zweryfikowane]. Procedura SME z limitem 100 000 EUR wymaga sprawdzenia [niepewne].
- Wielka Brytania: sprzedawca spoza UK rejestruje się do VAT od pierwszej sprzedaży B2C, OSS tego nie pokrywa ([Stripe](https://stripe.com/resources/more/uk-vat-on-digital-products)) [zweryfikowane]. Na start warto zablokować sprzedaż konsumencką do UK albo skierować ją przez MoR.
- Zakup API od dostawców zagranicznych to import usług: podatnik zwolniony podmiotowo i tak nalicza polski VAT bez prawa odliczenia, co podniosłoby COGS o 23%. Status czynnego podatnika VAT od pierwszego dnia wygląda na konieczny [wnioskowanie, do potwierdzenia z księgowym].

### 5.5 Nadużycia i przeciwdziałanie

Stripe raportuje 6,2 raza więcej nadużyć darmowych triali między listopadem 2025 a lutym 2026 oraz 10 razy więcej prób nadużyć w samoobsługowych startupach AI ([Stripe](https://stripe.com/resources/more/how-to-prevent-free-trial-abuse-in-saas-and-ai-products)) [zweryfikowane]. Próg Visa VAMP dla sprzedawców w UE spadł 1.04.2026 do 1,5% sporów i zgłoszeń fraudu łącznie ([justt](https://justt.ai/blog/visa-vamp-threshold-changes-april-2026/)) [zweryfikowane].

| Wzorzec | Przeciwdziałanie |
|---|---|
| Card testing na najtańszej paczce | Checkout hostowany, CAPTCHA przed utworzeniem płatności, limity per IP i konto, reguła Radar "karta testowana u wielu sprzedawców", minimalna paczka 10 USD, brak zakupu bez zalogowania |
| Kradzione karty: duża paczka i natychmiastowe spalenie na wideo | 3DS przy pierwszej płatności i paczkach, limit dziennego COGS dla kont młodszych niż 7 dni, kredyty roczne wydawane co miesiąc, blokada konta po wczesnym ostrzeżeniu o fraudzie |
| Farmienie darmowych kredytów | brak darmowego wideo, bonus dopiero po weryfikacji karty, jeden bonus na odcisk karty i urządzenie, lista jednorazowych domen e-mail, Turnstile przy rejestracji, bonus polecający dopiero po płatności poleconego |
| Friendly fraud i spory o odnowienia | plan roczny nigdy domyślnie, e-mail przed odnowieniem, anulowanie jednym kliknięciem, proaktywny zwrot nieużytego odnowienia, czytelny deskryptor na wyciągu |
| Zwrot po zużyciu kredytów | zwrot tylko niewykorzystanej części; cofnięcie kredytów w ledgerze; saldo ujemne blokuje konto |

Reguły [wnioskowanie], oparte na wytycznych Stripe ([Radar rules](https://stripe.com/guides/radar-rules-101), [free trial abuse](https://stripe.com/resources/more/free-trial-abuse)).

## 6. Ledger kredytów

Praktyki poniżej to [wnioskowanie] zgodne z opisami wdrożeń ([stigg](https://www.stigg.io/blog-posts/ai-credits), [flexprice](https://flexprice.io/blog/how-to-implement-real-time-credit-gating), [autumn](https://useautumn.com/blog/ai-billing-infrastructure), [solvimon](https://www.solvimon.com/blog/credit-billing-infrastructure-that-scales-for-ai)).

- **Tabele**: `credit_accounts` (użytkownik lub workspace), `credit_grants` (partie: źródło, kwota, pozostało, `expires_at`, priorytet), `ledger_entries` (append-only, każda operacja jako para debet/kredyt między kontami `available`, `reserved`, `consumed`, `expired`, `promo`), `reservations` (zadanie, kwota, status, TTL).
- **Rezerwacja**: przy zgłoszeniu zadania jedna transakcja Postgres blokuje wiersz konta, sprawdza saldo, przenosi kwotę z `available` do `reserved` i dopiero potem wysyła zadanie do dostawcy. Po webhooku sukcesu następuje rozliczenie faktycznej kwoty i zwolnienie różnicy; po błędzie, timeoucie lub blokadzie moderacji pełny zwrot. Cron zwalnia rezerwacje po upływie TTL.
- **Kolejność zużycia**: najpierw partie wygasające najwcześniej, promocyjne przed płatnymi, kredyty z planu przed paczkami. Czyste FIFO po dacie przyznania potrafi spalić kupione kredyty zamiast wygasających.
- **Idempotencja**: unikalny klucz na każdej rezerwacji i każdym przyznaniu. Dla webhooków Stripe kluczem jest ID zdarzenia lub faktury, dla dostawcy modeli ID żądania. Klucz ma chronić wywołanie płatnego API, nie tylko wpis w ledgerze.
- **Saldo**: kolumna z saldem jest tylko cache; prawdą jest suma wpisów. Nocna rekoncyliacja, `CHECK (available >= 0)`, zapis wyłącznie przez funkcje RPC z rolą serwisową; klient nie ma prawa zapisu (RLS).
- **Wygasanie i rollover**: nocne zadanie przenosi wygasłe partie na konto `expired` (to jest breakage do raportowania). Rollover z limitem to nowa partia z datą końca następnego okresu.
- **Auto-refill**: próg, kwota i miesięczny limit; płatność off-session z jedną próbą na przekroczenie progu (blokada), a przy wymaganym 3DS e-mail do użytkownika.
- **Zespoły**: konto kredytowe należy do workspace, wpisy niosą `actor_user_id`, limity miesięczne na członka, zakup tylko przez właściciela.
- **Analityka marży**: przy każdym zadaniu zapisywać `credits_charged`, `cogs_usd` i wersję cennika. Bez tego nie da się skalibrować mnożników ani założeń o breakage.

## Ograniczenia badania

- Bezpośrednie pobieranie stron było zablokowane (higgsfield.ai, versely.studio i hermoso.ai nie rozwiązywały się w sieci sesji), więc dane spoza konektora MCP pochodzą z wyników wyszukiwania, w większości z serwisów trzecich. Do pełnej weryfikacji trzeba dopuścić te hosty w ustawieniach sieci sesji.
- Stawki Stripe, Vercel i Supabase oraz ceny API należy potwierdzić na stronach oficjalnych w dniu wdrożenia.
- Kursu USD/PLN nie weryfikowałem; ceny w PLN trzeba wyliczyć z bieżącego kursu.

## Źródła

Higgsfield
- Konektor MCP Higgsfield, konfiguracja cennika, odczyt 2026-11-13 (bez URL)
- https://higgsfield.ai/blog/higgsfield-pricing-explained
- https://higgsfield.ai/blog/credits-vs-unlimited-ai-video-generation
- https://higgsfield.ai/creator-hub/help-center/refunds/why-didnt-i-receive-a-refund-after-canceling-my-subscription
- https://stripe.com/customers/higgsfield
- https://solidgate.com/case-studies/how-higgsfield-protects-subscription-revenue-with-solidgate/
- https://www.heygen.com/blog/higgsfield-pricing
- https://hermoso.ai/pricing/higgsfield/
- https://www.krea.ai/blog/higgsfield-pricing-explained-2026-unlimited-credits-and-real-monthly-costs
- https://www.krea.ai/blog/what-is-higgsfield-ai-pricing-free-plan-and-alternatives-in-2026
- https://www.versely.studio/blog/higgsfield-pricing-2026
- https://krater.ai/blog/higgsfield-pricing
- https://camclo3d.com/blog/higgsfield-pricing
- https://www.wireflow.ai/blog/higgsfield-ai-pricing
- https://www.toolcolumn.com/learn/higgsfield-credits-explained
- https://aliteq.com/which-higgsfield-model-to-use
- https://aliteq.com/higgsfield-unlimited-explained
- https://aiimagetovideo.pro/blog/higgsfield-unlimited/
- https://novoads.ai/en/blog/is-higgsfield-free
- https://www.mindstudio.ai/blog/higgsfield-subscription-cancellation-complaints
- https://sacra.com/research/higgsfield-at-230m-arr/
- https://www.saasrise.com/deals/higgsfield-just-raised-400-million-at-a-54-billion-valuation-cdd69c44-9235-4423-9d67-487660520830

Konkurencja
- https://www.renderahouse.com/blog/freepik-pricing
- https://www.renderahouse.com/blog/krea-ai-pricing
- https://voyager.so/blog/openart-pricing
- https://www.renderahouse.com/blog/leonardo-ai-pricing
- https://www.pixara.ai/blogs/runway-pricing
- https://kling.ai/app/membership/membership-plan?r=26
- https://aitoolsbakery.com/blog/ai-video-generator-pricing-compared/
- https://www.kavel.ai/blog/best-free-ai-video-generators-2026

Ceny API i infrastruktura
- https://fal.ai/models/fal-ai/flux-2-pro
- https://fal.ai/models/bytedance/seedance-2.0/text-to-video
- https://fal.ai/learn/tools/seedance-2-0-vs-kling-3-0
- https://fal.ai/learn/tools/gpt-image-2-vs-nano-banana-2
- https://fal.ai/learn/tools/nano-banana-vs-seedream
- https://www.teamday.ai/blog/fal-ai-pricing-2026
- https://aireiter.com/blog/kling-4-0-api-pricing-fal-cost-vs-seedance-vidu
- https://argolink.io/en/blog/kling-4-0-api-pricing
- https://kreatorflow.ai/ai-video-api-pricing
- https://www.mindstudio.ai/blog/seedance-2-5-review-pricing
- https://veonano.com/blog/posts/nano-banana-pricing
- https://usagebox.com/articles/nano-banana-pro-api-pricing-cost-per-image-2026
- https://www.assemblyai.com/blog/tts-api-pricing
- https://flexprice.io/blog/vercel-pricing-breakdown
- https://www.activepieces.com/blog/supabase-pricing-free-tier-limits-pro-costs-egress
- https://upstash.com/kb/cloudflare-r2-pricing-in-2026-storage-operations-and-real-monthly-bills
- https://resend.com/pricing.md
- https://www.activepieces.com/blog/sentry-pricing-2026-developer-team-business-plans
- https://posthog.com/pricing.md
- https://www.agenticaipricing.com/how-to-prevent-credit-breakage-from-hurting-customer-trust/

Płatności, podatki, fraud
- https://stripe.com/en-pl/pricing
- https://stripe.com/en-pl/pricing/local-payment-methods
- https://paymentreview.com/blog/poland-card-blik-payment-fees-2026/
- https://flexprice.io/blog/stripe-pricing-breakdown-2026
- https://support.stripe.com/questions/understanding-stripe-tax-pricing
- https://support.stripe.com/questions/updates-to-radar-pricing-(january-2027)
- https://docs.stripe.com/changelog/dahlia/2026-04-22/stripe-billing-blik-recurring-payments
- https://docs.stripe.com/changelog/endive/2026-09-30/blik-recurring-off-session-payments
- https://docs.stripe.com/payments/checkout/localize-prices/adaptive-pricing
- https://docs.stripe.com/billing/subscriptions/usage-based/billing-credits
- https://stripe.com/managed-payments
- https://stripe.com/legal/restricted-businesses
- https://stripe.com/resources/more/how-to-prevent-free-trial-abuse-in-saas-and-ai-products
- https://stripe.com/resources/more/free-trial-abuse
- https://stripe.com/guides/radar-rules-101
- https://stripe.com/resources/more/uk-vat-on-digital-products
- https://aliteq.com/cheapest-merchant-of-record
- https://fintechspecs.com/blog/merchant-of-record-fees-compared/
- https://developer.paddle.com/concepts/payment-methods/blik
- https://www.paddle.com/help/start/intro-to-paddle/what-am-i-not-allowed-to-sell-on-paddle
- https://www.boathouse.co/paddle-video-series-episode/34-aup-update-gen-ai
- https://polar.sh/legal/acceptable-use-policy
- https://polar.sh/docs/merchant-of-record/supported-countries
- https://dodopayments.com/blogs/polar-sh-review
- https://dodopayments.com/blogs/lemonsqueezy-review
- https://docs.creem.io/merchant-of-record/account-reviews/account-reviews
- https://www.trustpilot.com/review/creem.io?page=2
- https://justt.ai/blog/visa-vamp-threshold-changes-april-2026/
- https://www.przelewy24.pl/blog/vat-oss-w-e-commerce-kompletny-przewodnik-dla-sprzedawcow
- https://plumm.pl/wiedza/vat-oss
- https://amavat.pl/nowy-limit-zwolnienia-z-vat-a-sprzedaz-internetowa-kiedy-limit-krajowy-nie-chroni-przed-vat-za-granica/

Ledger kredytów
- https://www.stigg.io/blog-posts/ai-credits
- https://flexprice.io/blog/how-to-implement-real-time-credit-gating
- https://useautumn.com/blog/ai-billing-infrastructure
- https://www.solvimon.com/blog/credit-billing-infrastructure-that-scales-for-ai
