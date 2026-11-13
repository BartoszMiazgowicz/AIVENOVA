# 03 - Dostawcy modeli i API (stan na 2026-11-13)

Metoda: WebSearch (ok. 45 zapytań) plus dwa źródła "na żywo" przez MCP: katalog Vercel AI Gateway (ceny listowe, odczyt 2026-11-13) i katalog modeli Higgsfield. WebFetch i curl były zablokowane, więc stron cenników fal.ai, kling.ai, BytePlus itd. nie otwierałem bezpośrednio; ceny spoza MCP pochodzą ze streszczeń wyników wyszukiwania (często blogi wtórne). Tagi: [zweryfikowane] = jest źródło, [wnioskowanie] = mój wniosek, [niepewne] = źródła sprzeczne lub tylko wtórne.

## TL;DR

- **Nie ma jednego dostawcy na wszystko.** Rekomendacja: **fal.ai jako dostawca katalogowy** (najszerszy katalog, kolejka + webhooki, trenowanie LoRA, lipsync, 3D, upscale; regulamin wprost dopuszcza własny produkt z użytkownikami końcowymi) oraz **Vercel AI Gateway jako dostawca cenowy** dla modeli, które sprzedaje po cenie listowej bez marży (Seedance, Veo, obrazy Google/OpenAI/BFL, ElevenLabs). Failover: Replicate. [wnioskowanie]
- **Różnice cen tego samego modelu sięgają 2x.** Seedance 2.5 w 720p: ok. $0.231/s po cenie listowej (BytePlus, Vercel, Replicate) kontra ok. $0.473/s na fal. Kling 3.0 odwrotnie: fal $0.084-0.168/s, Vercel $0.168-0.336/s. Routing per model to warunek marży. [zweryfikowane]
- **OpenAI nie ma już wideo:** Sora API wyłączone 24.09.2026, bez następcy. Veo znika z Gemini API i z fal (17.11.2026); zostaje Vertex AI i Vercel. Nowa linia Google to Gemini Omni Flash. [zweryfikowane / częściowo niepewne]
- **Higgsfield ma publiczne API** (od 16-17.09.2026, pay-as-you-go w USD), ale jego regulamin uznaje nieautoryzowaną redystrybucję dostępu deweloperskiego za istotne naruszenie. Nie nadaje się na źródło podaży dla produktu konkurencyjnego. [zweryfikowane + wnioskowanie]
- **Ograniczenia istotne dla UE:** Veo w lokalizacjach UE/UK/CH dopuszcza tylko `personGeneration: allow_adult`; Seedance 2.x blokuje referencje z twarzami realnych osób bez weryfikacji; OpenAI wymaga weryfikacji organizacji dowodem tożsamości dla modeli obrazowych. [zweryfikowane]
- Koszt typowej generacji: obraz $0.01-0.05, klip 5 s 720p $0.18-1.16, klip premium 1080p $1.2-2.9, voiceover 500 znaków $0.02-0.04.

## 1. Co się zmieniło na rynku w 2026

| Zdarzenie | Skutek dla planu | Status |
|---|---|---|
| Sora: aplikacja wyłączona 26.04.2026, API 24.09.2026, brak zamiennika ([źródło][sora-shutdown]) | Nie planować Sory; "Sora-class" pokrywają Kling 4.0, Seedance 2.5, Veo 3.1 | [zweryfikowane] |
| Google przestało sprzedawać Veo przez Gemini API ok. 22.10.2026; fal wycofuje Veo 3.1 17.11.2026 ([veopricing][veo-providers], [fal deprecation][fal-veo-deprecation]) | Veo tylko przez Vertex AI, Vercel AI Gateway, Replicate; ryzyko dalszego wygaszania | [niepewne] (źródła wtórne); katalog Vercel nadal listuje Veo 3.1 [zweryfikowane][vercel-mcp] |
| Kling 4.0 (komunikat 16.10.2026), na fal od 23-24.10; Kling 4.0 Flash GA 4.11.2026 ([aireiter][kling4-aireiter], [orcarouter][kling4-flash]) | Flagowy model wideo; fal miał go po ok. tygodniu, Vercel nie ma do dziś | [zweryfikowane] |
| Seedance 2.5 (07.08.2026), FLUX 3 obraz+wideo (04.08.2026), Wan 3.0, MiniMax H3 (następca Hailuo), Seedream 5.5 (9-12.11.2026) | Aktualne wersje do adapterów | [zweryfikowane][vercel-mcp] |
| Cloudflare przejął Replicate (ogłoszenie 17.11.2025, zamknięcie na początku 2026); marka i API bez zmian ([the-decoder][replicate-cf]) | Replicate stabilny jako failover | [zweryfikowane] |
| Vercel AI Gateway obsługuje obraz (41 modeli), wideo (36) i mowę/muzykę (24) | Realny drugi dostawca na istniejącym koncie Vercel | [zweryfikowane][vercel-mcp] |

## 2. Modele: dostęp i ceny jednostkowe

Ceny z oznaczeniem "Vercel" to odczyt katalogu na żywo z 2026-11-13 ([katalog][vercel-mcp]); Vercel deklaruje brak marży na wideo, więc traktuję je jako ceny listowe producenta ([changelog][vercel-seedance]).

### 2.1 Wideo

| Rodzina (wersja) | API oficjalne | Agregatory | Cena za sekundę |
|---|---|---|---|
| **Kling** 4.0, 4.0 Flash, 3.0, 3.0 Turbo, O3 | kling.ai/dev, przedpłacone pakiety "units" (lista $0.14/unit; pakiety od $700/5000 units, ważność 180 dni, -10% od 30k units) ([vidirect][kling-vidirect]) | fal, Replicate, Runware, WaveSpeed, Atlas; Vercel tylko do 3.0 | 4.0: 1.0 unit/s 720p, 1.5 unit/s 1080p ([felloai][kling-felloai]); fal $0.157 / $0.235 ([aireiter][kling4-aireiter]). 4.0 Flash: 0.6 unit/s, tylko 720p, ok. $0.094 ([kling.ai][kling-dev-pricing]). 3.0 na fal: Std $0.084, Pro $0.112, Pro+audio $0.168 ([rendercents][kling3-rendercents]); Vercel: Std $0.168, Pro $0.224, Pro+audio $0.336 [zweryfikowane] |
| **Google Veo** 3.1 / Fast / Lite | Vertex AI (Gemini API: sprzedaż zakończona [niepewne]) | Vercel, Replicate; fal do 17.11 | Vercel: 3.1 $0.20 bez audio / $0.40 z audio (720p-1080p), 4K $0.40/$0.60; Fast $0.10/$0.15, 4K $0.30/$0.35; Lite $0.03/$0.05 (720p), $0.05/$0.08 (1080p) [zweryfikowane] |
| **Gemini Omni Flash** 1.1 / 1.2 | Gemini API (płatny tier) | Vercel, OpenRouter, Runware | 1.2: $12 za 1M tokenów wideo, ok. $0.07/s w 720p, ok. $0.023/s w 360p ([eesel][omni-eesel]) [zweryfikowane wtórnie] |
| **Seedance** 2.5, 2.0, 2.0 Fast, 2.0 Mini | BytePlus ModelArk (rozliczenie tokenowe) | Vercel, Replicate, fal, OpenRouter, Runware, WaveSpeed, Atlas, Kie | Vercel/BytePlus 2.5: $10.7/M tokenów (480-720p), $11.7/M (1080p), z wejściem wideo $6.4-7.0/M. Daje to $0.103 / $0.231 / $0.569 za s (480/720/1080p) ([argolink][seedance-argolink]). 2.0: $7.0/M; Fast $5.6/M; Mini $3.5/M [zweryfikowane]. fal 2.5: $0.2205 / $0.473 / $1.164 ([fal][seedance-fal]), ok. 2.05x listy ([audyt][seedance-audit]) |
| **Wan** 3.0, 3.0 Prime, 2.7 | Alibaba Cloud Model Studio | Vercel, fal, Replicate, Together (2.7), DeepInfra | 3.0: $0.05 / $0.10 / $0.20 (480/720/1080p); Prime $0.068 / $0.14 / $0.28 ([Alibaba][wan3-alibaba], Vercel) [zweryfikowane] |
| **MiniMax** H3, H3 Max | platform.minimax.io | Vercel, fal | H3: $0.08 (768p), $0.13 (2K); H3 Max: $0.05 (480p), $0.08 (768p) ([MiniMax][minimax-docs]) [zweryfikowane] |
| **FLUX 3 Video** | bfl.ai | Vercel (bez ceny w katalogu), fal | $0.15-0.41/s wg jednego przewodnika ([layer3][flux3-layer3]) [niepewne] |
| **Grok Imagine Video** 1.5, 1.5 Lite | xAI API | Vercel (prefiks `spacexai/`), fal | 1.5: $0.08 / $0.14 / $0.25; Lite: $0.02 / $0.03 / $0.14 (480/720/1080p) [zweryfikowane][vercel-mcp] |
| **Runway** Gen-4.5, Aleph 2.0 | dev.runwayml.com, $0.01 za kredyt, progi wydatków | głównie bezpośrednio | Gen-4.5 12 kr/s = $0.12; Aleph 2.0 $0.28; Gen-4 Turbo $0.05 ([toolcolumn][runway-toolcolumn]) [zweryfikowane wtórnie] |
| **Luma** Ray3.2 | Luma API, cena za klip | Atlas i inni | 5 s: $0.15 (540p), $0.30 (720p), $1.20 (1080p); HDR x2 ([picassoia][luma-picasso]) [zweryfikowane wtórnie] |
| **Pika** 2.5 | brak jasnego API pierwszej strony | fal | $0.04 (720p), $0.09 (1080p) ([apiframe][pika-apiframe]) [niepewne] |
| **Sora** | wyłączone | - | - |

### 2.2 Obraz

| Rodzina (wersja) | API oficjalne | Cena za obraz |
|---|---|---|
| **Nano Banana 2.1** (`gemini-nano-banana-2.1`) | Gemini API, Vertex; Vercel, fal, Replicate | $0.0336 (1K), $0.0504 (2K), $0.1134 (4K) [zweryfikowane][vercel-mcp]; fal ok. $0.04 [niepewne] |
| **Nano Banana Pro** | jw. | $0.134 (1K/2K), $0.24 (4K) [zweryfikowane]; fal $0.15 / $0.30 ([argolink][nbpro-argolink]) |
| **GPT Image 2.6** (także 2.5, 2) | OpenAI API (wymaga weryfikacji organizacji dokumentem tożsamości, [forum][openai-verify]); Vercel, fal | Tokenowo: $5/M tekst, $8/M obraz wej., $30/M obraz wyj. Dla 1024x1024: low $0.025, medium $0.043, high $0.053 ([eesel][gptimg-eesel]); medium ok. 3x drożej niż w 2.5 ([dev.to][gptimg-dev]) [zweryfikowane wtórnie] |
| **Seedream** 5.5, 5.0 Pro/Lite, 4.5 | BytePlus; OpenRouter, WaveSpeed, Kie; Vercel do 5.0 | 5.5: od $0.02, hi-res $0.035 ([OpenRouter][seedream55-openrouter]); 5.0 Lite/Pro $0.035, 4.5 $0.04 (Vercel) [zweryfikowane] |
| **FLUX 3 Image** / Klein | bfl.ai; Vercel, fal, Replicate, Together, OpenRouter | FLUX 3: $0.041 (768), $0.048 (1K), $0.07 (1.5K), $0.10 (2K), $0.607 (4K). Klein: $0.008-0.036 ([BFL][bfl-release], Vercel) [zweryfikowane] |
| **Grok Imagine Image** 2.0 | xAI API; Vercel | $0.06 (low $0.04, 2K $0.08); wersja bazowa $0.02 [zweryfikowane][vercel-mcp] |
| **Ideogram 4.5** | Ideogram API; fal, Replicate | od $0.008 (najniższa jakość), medium $0.06, high $0.10, edycja high $0.22 ([glbgpt][ideogram-glb], [alphasignal][ideogram-alpha]) [niepewne] |
| **Recraft V4.1** | recraft.ai API; Vercel, fal | $0.035 raster, $0.08 wektor, Pro $0.21 / $0.30, Flash $0.007 ([Recraft][recraft-pricing]) [zweryfikowane] |

### 2.3 Audio

| Usługa | Dostęp | Cena |
|---|---|---|
| **ElevenLabs TTS** v4, v4 Turbo, v3, Flash v2.5 | ElevenLabs API (plany $6-$990/mies. lub użycie), Vercel, fal | v4, v3, Multilingual v2: $0.08 za 1k znaków; v4 Turbo, Flash: $0.04 za 1k [zweryfikowane][vercel-mcp] |
| **Eleven Music** v2.5, **Sound Effects** v2 | jw. | Music $0.0025/s ($0.15/min); SFX $0.002/s [zweryfikowane][vercel-mcp] |
| **Dubbing, Voice Changer** | ElevenLabs API | Dubbing ok. $0.33/min, Voice Changer $0.12/min; dane z 06.2026 ([puter][eleven-puter]) [niepewne] |
| Tańsze TTS | Vercel | Fish Audio S2.1 Pro i OpenAI TTS-1 $0.015 za 1k; MAI-Voice-2.1 $0.022 za 1k [zweryfikowane][vercel-mcp] |

Klonowanie głosu: wymaga uprawnień do głosu i świadomej zgody osoby; ElevenLabs zastrzega szeroką licencję na model głosu ([terms.law][eleven-consent]). Odsprzedaż samej usługi jest zabroniona, komercyjne użycie outputu dozwolone na planach płatnych ([terms.law][eleven-terms]) [zweryfikowane wtórnie].

### 2.4 Narzędzia

| Kategoria | Opcje i ceny | Status |
|---|---|---|
| **Lipsync** | Sync (sync.so): lipsync-2 $0.04-0.05/s, lipsync-2-pro $0.067-0.083/s, sync-3 $0.107-0.133/s przy 25 fps ([Sync][sync-docs]); WaveSpeed lipsync-3 $0.134/s ([WaveSpeed][sync-wavespeed]); VEED Lipsync v2 na fal $0.07/s ([fal][veed-lipsync]); Kling Lipsync ok. $0.014-0.017/s ([fairstack][kling-lipsync]); MiniMax H3 Max Lip Sync $0.05-0.16/s ([fal][h3-lipsync]) | [zweryfikowane], Kling [niepewne] |
| **Upscale wideo** | Topaz Starlight Precise 2.6 / Fast 3: $0.059/s do 1080p, $0.124/s 1440p-4K ([yotta][topaz-yotta]); Topaz Video Upscale na fal ok. $0.08/s ([llm-stats][topaz-llmstats]). Oficjalnego cennika Topaz API nie znalazłem; Vercel listuje modele Topaz bez ceny | [niepewne] |
| **Image-to-3D** | SAM 3D Objects na fal $0.02 ([fal][sam3d-fal]); Tripo $0.20-0.30 ([Tripo][tripo-pricing]); Meshy 20-30 kredytów, aktualny meshy-7.1 ([Meshy][meshy-pricing]); Hunyuan3D v3 na fal $0.375 z teksturą ([apitariff][hunyuan-apitariff]) | [zweryfikowane] |
| **Usuwanie tła** | Bria RMBG 2.0 na fal ok. $0.018/obraz; BiRefNet na Replicate ok. $0.0005/obraz ([aireiter][bg-aireiter]). Dla wideo ceny nie znalazłem | [niepewne] |
| **Trening LoRA** | fal `flux-lora-fast-training` ok. $2 za 1000 kroków; FLUX.2 [dev] trainer $0.008/krok ([fal][lora-fal-flux2]); Z-Image trainer $2.26/1000 kroków ([tech-insider][lora-techinsider]); Replicate ok. $1.46 za 1000 kroków | [zweryfikowane wtórnie] |

## 3. Porównanie agregatorów

| Kryterium | fal.ai | Vercel AI Gateway | Replicate | Runware | WaveSpeedAI | Kie.ai | Atlas Cloud |
|---|---|---|---|---|---|---|---|
| Katalog | Najszerszy: wideo, obraz, audio, lipsync, 3D, trening | 41 obraz / 36 wideo / 24 mowa; brak treningu, lipsync, 3D, Kling 4.0, Seedream 5.5 | Bardzo szeroki, także modele społeczności | 300+ modeli, mocny w obrazie | 700+ modeli, szybko dodaje modele chińskie | Popularne modele, rozliczenie kredytami | Szeroki, multimodalny |
| Marża wobec listy | Zmienna: 0% (Kling 3.0, MiniMax), ok. 12% (NB Pro), ok. 105% (Seedance 2.5) | 0% deklarowane; ale Kling 3.0 2x drożej niż fal | Seedance 2.5 po liście; Kling 3 Pro 2x fal ([teamday][fal-vs-replicate]) [niepewne] | Zbliżona do listy | Poniżej fal na Seedance ($0.18/s) | Najtańszy, 30-50% poniżej fal | Średnia; promocje |
| Nowe modele | Kling 4.0 po ok. 7 dniach | Wolniej (brak Kling 4.0 po 4 tyg.) | Szybko | Szybko | Bardzo szybko | Bardzo szybko | "Day-zero" wg własnych deklaracji |
| Kolejka i webhooki | Dojrzałe: queue, webhook, status, retry 429 w kliencie | `experimental_startVideo`, webhook ze zdarzeniami terminalnymi, idempotency-key; API eksperymentalne, wideo w becie na planach płatnych ([docs][vercel-video-docs]) | Predictions + webhooki | Tak [niepewne] | Tak [niepewne] | Tak | Tak |
| Limity nowych kont | 2 równoległe żądania, rośnie z zakupami do 40, wyżej przez sprzedaż; nadmiar jest kolejkowany ([fal][fal-concurrency]) | Nie znalazłem | 600 predykcji/min; 6/min bez metody płatności ([Replicate][replicate-limits]) | Nie znalazłem | 5 predykcji/min i 2 równoległe do pierwszego doładowania ([gengrades][wavespeed-review]) | Nie znalazłem | Nie znalazłem |
| Niezawodność | Publiczny status; incydenty 2026: 4 h degradacji 8.04, 30 min niedostępności 4.09 ([status][fal-status]) | Metryki uptime per endpoint w katalogu | Zaplecze Cloudflare | Brak danych | Deklaruje 99.9-99.99% | Własna dokumentacja przyznaje niższą stabilność; Trustpilot ok. 2.5/5 ([gengrades][kie-review]) | Deklaruje 99.99% |
| UE / DPA | DPA opublikowane (rola procesora); brak rezydencji danych w UE ([fal DPA][fal-dpa], [magichour][fal-review]) | Flagi no-training i ZDR per endpoint; region `eu` dla części modeli Google | Nie zweryfikowałem | Deklaruje GDPR, ISO 27001, SOC 2, infrastrukturę w Europie i USA ([Runware][runware-zdr]) | Nie znalazłem | Brak SOC 2 / GDPR | DPA nie znalazłem |

Dane a UE: w katalogu Vercel endpointy Kling i ByteDance mają siedzibę dostawcy "CN", flagę no-training ustawioną i brak ZDR; alternatywny endpoint Tencent dla Seedance 2.5 nie ma flagi no-training [zweryfikowane][vercel-mcp]. Przy każdej trasie dane wejściowe (w tym twarze użytkowników) trafiają do producenta modelu, co trzeba ująć w rejestrze podprocesorów. [wnioskowanie]

Pozostali: **OpenRouter** ma już wideo i obraz (Seedance 2.5, Veo 3.1, Gemini Omni, Seedream 5.5), ceny bez marży, ale 5.5% opłaty przy zakupie kredytów ([OpenRouter][openrouter-fee]) [zweryfikowane]. **Together AI** ma 40+ modeli obrazu i wideo, m.in. Wan 2.7 po $0.10/s ([Together][together-wan]) [zweryfikowane]. Kredyty przedpłacone wygasają po 365 dniach na fal i Atlas ([signunder][fal-signunder], [Atlas][atlas-aup]).

## 4. Warunki: resale, prawa do outputu, moderacja

| Dostawca | Budowa własnego produktu / resale | Prawa do outputu | Moderacja i zakazy |
|---|---|---|---|
| **fal.ai** | "API Services" pozwala używać platformy przez API w "Client Solution" i udostępniać ją "End Users"; fal może ograniczyć nadmierne wywołania ([fal][fal-api-terms]) [zweryfikowane] | Klient zachowuje input; output "at Customer's sole risk", może być nieunikalny; komercyjność zależy od modelu ([signunder][fal-signunder]) | AUP: zakaz CSAM, NCII, treści nielegalnych; fal uruchamia moderację po swojej stronie, modele partnerów mają własne filtry ([fal][fal-trust]) |
| **Vercel AI Gateway** | Zwykły przypadek użycia platformy [wnioskowanie]; osobny Vercel AI Acceptable Use Policy | Wg warunków producenta modelu | AUP: CSAM, NCII |
| **Replicate** | Regulamin zakazuje "make available any Services... including SaaS" ([Replicate][replicate-terms]). To klauzula przeciw odsprzedaży samej usługi, ale wymaga lektury tekstu źródłowego przed oparciem produktu na Replicate | Replicate przenosi na klienta prawa do outputu, z zastrzeżeniem licencji modelu; np. Ideogram zakazuje użycia outputów do produktów konkurencyjnych | Per model |
| **Runware** | Nie znalazłem zakazu | Nie bierze licencji na outputy, nie trenuje na danych klienta ([Runware][runware-terms]) | - |
| **Kie.ai** | Wg recenzji nie jest licencjonowanym partnerem większości producentów; musiał usunąć Midjourney na żądanie ([sharkly][kie-sharkly]) | Regulamin nie adresuje jasno własności outputu | Ryzyko nagłego zniknięcia modeli |
| **Kling (direct)** | Warunki konsumenckie zakazują dystrybucji i sprzedaży usługi; warunków API nie udało się potwierdzić ([everypixel][everypixel-licenses]) [niepewne] | Komercyjne dla płacących; brak indemnifikacji IP | Filtry producenta |
| **BytePlus (direct)** | Nie zweryfikowałem | BytePlus nie rości praw do outputu ([toolso][byteplus-toolso]) | Seedance 2.x: brak uploadu referencji z realnymi twarzami bez weryfikacji i zgody ([seedrouter][seedance-realperson]) |
| **Google Veo** | Przez Vertex/Vercel | - | W lokalizacjach UE/UK/CH/MENA tylko `allow_adult`; image-to-video wszędzie tylko `allow_adult` ([Google][veo-docs]) [zweryfikowane] |

Wniosek: obowiązki moderacji spadają na operatora produktu. Filtry dostawcy są pierwszą linią, ale nie zwalniają z własnej polityki treści i obsługi błędów typu `content_policy_violation`. [wnioskowanie]

## 5. Higgsfield API jako źródło podaży

- Publiczne API istnieje od 16-17.09.2026, jako osobny produkt z saldem w USD (min. doładowanie $5, środki wygasają po roku, zwrot za nieudane generacje, output przechowywany min. 7 dni) ([Higgsfield][hf-api-blog], [catclaw][hf-catclaw]). [zweryfikowane wtórnie]
- Ceny wg oficjalnego cennika cytowanego w wynikach: Kling 4.0 od $0.126/s, Kling 4.0 Flash od $0.063/s, Seedance 2.5 od $0.118/s; źródła podają też $0.0738 i $0.2057 dla Seedance 2.5 (promocje startowe kontra lista) ([cennik][hf-open-pricing], [apiframe][hf-apiframe]). [niepewne]
- Limity: 2 równoległe żądania poniżej $25 doładowań z 28 dni, 10 od $25, 20 od $100, 40 od $1000; webhooki ponawiane do 2 godzin ([Higgsfield][hf-vs-sub]). [zweryfikowane wtórnie]
- Regulamin: nieautoryzowana redystrybucja "Developer Access" to istotne naruszenie; klucz może zostać cofnięty w każdej chwili; sekcja 5.2 ogranicza komercyjną eksploatację samej usługi ([Terms][hf-terms], [aliteq][hf-commercial]). [zweryfikowane wtórnie]
- Katalog Higgsfield oznacza część modeli audio (Sonilo, Mirelo, Inworld TTS) dostawcą "FAL", czyli sam Higgsfield kupuje długi ogon z fal [zweryfikowane, MCP].

**Ocena:** nie używać jako źródła podaży. Produkt konkurencyjny zależałby od klucza, który konkurent może cofnąć, a regulamin daje mu do tego podstawę. Przydatne tylko jako benchmark cenowy. [wnioskowanie]

## 6. Rekomendowana strategia podaży

1. **Dostawca katalogowy: fal.ai.** Wszystko, czego nie ma gdzie indziej: Kling 4.0 i Flash, lipsync, upscale, 3D, usuwanie tła, trening LoRA. Doładować wcześnie, bo limit równoległości rośnie z historią zakupów.
2. **Dostawca cenowy: Vercel AI Gateway.** Seedance 2.x, Veo 3.1, Nano Banana, GPT Image, FLUX 3, Grok Imagine, Wan 3.0, ElevenLabs. Jeden rachunek na istniejącym koncie, ceny listowe, brak weryfikacji organizacji w OpenAI [wnioskowanie]. Ryzyko: API wideo jest eksperymentalne.
3. **Failover: Replicate** (Seedance 2.5 po liście, Veo nadal w katalogu), po lekturze regulaminu.
4. **Kontrakty bezpośrednie później** (BytePlus, Kling, Vertex AI), gdy wolumen uzasadni pakiety i rabaty. Kie.ai i podobnych resellerów nie włączać do produkcji.

**Shortlista startowa i koszt typowej generacji** (trasa = najtańsza wiarygodna):

| # | Model | Rola | Trasa | Koszt typowej generacji |
|---|---|---|---|---|
| 1 | Nano Banana 2.1 | domyślny obraz + edycja | Vercel | $0.034 (1K), $0.050 (2K) |
| 2 | GPT Image 2.6 | tekst w obrazie, reklamy | Vercel | $0.043 (medium, 1024x1024) |
| 3 | FLUX 3 Image Klein / FLUX 3 | tani tier / fotorealizm | Vercel | $0.009 / $0.048 (1K) |
| 4 | Seedream 5.0 Lite (potem 5.5) | spójność postaci, serie | Vercel (5.5: OpenRouter lub BytePlus) | $0.035 ($0.02 dla 5.5) |
| 5 | Kling 4.0 | flagowe wideo | fal | 5 s: $0.79 (720p), $1.18 (1080p) |
| 6 | Kling 4.0 Flash | szybkie wideo, presety | Runware lub fal (dostępność na fal niepotwierdzona) | 5 s 720p: ok. $0.47 [niepewne] |
| 7 | Seedance 2.5 / 2.0 Fast | wideo z referencjami i audio | Vercel | 5 s 720p: $1.16 / ok. $0.60 [wnioskowanie z formuły tokenów] |
| 8 | Veo 3.1 Fast / Lite | wideo z natywnym audio | Vercel | 8 s z audio: $1.20 (Fast), $0.40 (Lite 720p) |
| 9 | Grok Imagine Video 1.5 Lite lub Wan 3.0 | tier darmowy / budżetowy | Vercel | 6 s 720p: $0.18 / 5 s 720p: $0.50 |
| 10 | ElevenLabs v4 Turbo + Music v2.5 | voiceover, muzyka | Vercel | 500 znaków: $0.02; 30 s muzyki: $0.075 |
| 11 | Sync lipsync-2 (sync-3 jako premium) | lipsync | fal lub Sync | 10 s: $0.40-0.50 (sync-3: $1.07-1.33) |
| 12 | Topaz upscale + Bria RMBG + trening LoRA | narzędzia | fal | upscale 5 s: ok. $0.30-0.40; tło: $0.018; LoRA: ok. $2 za trening |

## 7. Nota projektowa: warstwa abstrakcji dostawców

Jeden interfejs `ProviderAdapter` (`submit`, `getStatus`, `cancel`, `parseWebhook`, `estimateCost`) i tabela routingu `model_key -> [trasa główna, zapasowa]`. Adapter musi normalizować:

- **Identyfikatory:** własny `job_id` (UUID w Supabase), `provider`, `provider_job_id`, `idempotency_key` (Vercel przyjmuje nagłówek, fal ma `request_id`).
- **Stan:** `queued | running | succeeded | failed | canceled | expired`, z mapowaniem z `IN_QUEUE/IN_PROGRESS/COMPLETED` (fal), `starting/processing/succeeded` (Replicate), `video.generation.completed/failed/cancelled` (Vercel).
- **Webhook:** weryfikacja podpisu, deduplikacja po `provider_job_id`, obsługa ponowień. Webhook Vercel nie zawiera URL wideo, więc po zdarzeniu trzeba pobrać status. Zawsze fallback na polling z timeoutem.
- **Postęp:** `progress_pct` (często brak), `queue_position`, `eta_s`, logi.
- **Wejścia:** tylko URL-e (Vercel ogranicza żądanie startowe do 300 KiB, base64 kończy się 413), role referencji (`first_frame`, `last_frame`, `reference`, `video`, `audio`), limity per model.
- **Wyjścia:** natychmiastowa kopia do własnego storage (URL-e dostawców wygasają, np. po 7 dniach), metadane (rozdzielczość, czas, fps, audio, seed).
- **Koszt:** `cost_estimate_usd` przed startem i `cost_actual_usd` po zakończeniu, z jednostką rozliczenia (`per_second`, `per_image`, `per_token`, `per_char`, `per_step`), mnożnikami (rozdzielczość, audio, wejście wideo) i migawką cennika. Cennik kredytów liczyć od ceny trasy, nie modelu.
- **Taksonomia błędów:** `content_policy` (bez retry, zwrot kredytów), `invalid_input`, `rate_limited` / `concurrency_limit` (kolejkować), `provider_unavailable` i `timeout` (retry, potem failover), `insufficient_funds` (alert), `model_deprecated`, `unknown`. Osobne pole `billable` (część dostawców nalicza opłatę za odrzucone żądania).
- **Bezpieczeństwo:** `nsfw_flag`, `moderation_categories`, `blocked_stage` (prompt / input / output), `person_generation_mode`, znaczniki pochodzenia (SynthID, C2PA), flaga `real_person_reference`.

## 8. Luki i pytania otwarte

- Cenniki fal.ai, kling.ai, BytePlus, Topaz, Ideogram nie zostały otwarte bezpośrednio (blokada sieci); przed budżetowaniem zweryfikować je na stronach źródłowych.
- Nie potwierdziłem: warunków API Kling dla platform trzecich, DPA Replicate i WaveSpeed, limitów Vercel AI Gateway dla wideo, dostępności Seedance w regionie UE BytePlus (źródła sprzeczne, [regiony][byteplus-regions]).
- Rozbieżność cen Kling 3.0 między Vercel a fal (2x) nie ma wyjaśnienia.

## Źródła

[vercel-mcp]: https://vercel.com/ai-gateway/models
[vercel-video-docs]: https://vercel.com/docs/ai-gateway/modalities/video-generation
[vercel-seedance]: https://vercel.com/changelog/seedance-2.0-video-now-available-on-ai-gateway
[sora-shutdown]: https://techjacksolutions.com/ai-brief/openai-videos-api-sora-2-deprecated-september-2026/
[veo-providers]: https://www.veopricing.com/veo-3-1-api-providers/
[veo-docs]: https://ai.google.dev/gemini-api/docs/veo
[fal-veo-deprecation]: https://www.usagepricing.com/blueprint/activity/fal-ai-2026-10-15-veo-31-deprecation-date
[omni-eesel]: https://www.eesel.ai/blog/gemini-omni-1-2-flash-pricing
[kling-dev-pricing]: https://kling.ai/dev/pricing
[kling-vidirect]: https://vidirect.org/tools/kling/pricing
[kling4-aireiter]: https://aireiter.com/blog/kling-4-0-api-pricing-fal-cost-vs-seedance-vidu
[kling4-flash]: https://www.orcarouter.ai/blog/kling-4-0-flash-general-availability
[kling3-rendercents]: https://rendercents.com/pricing/kling-3-0-api
[kling-felloai]: https://felloai.com/kling-ai-pricing/
[seedance-argolink]: https://argolink.io/en/blog/seedance-2-5-api-pricing
[seedance-fal]: https://fal.ai/models/bytedance/seedance-2.5/us/reference-to-video
[seedance-audit]: https://ofox.ai/blog/seedance-2-5-price-audit-bytedance-formula-2026/
[seedance-realperson]: https://seedrouter.ai/blog/seedance-real-person-error
[byteplus-regions]: https://byteplus-sa.github.io/ComfyUI-BytePlus-ModelArk/concepts/keys-and-regions/
[byteplus-toolso]: https://toolso.ai/tool/byteplus
[seedream55-openrouter]: https://openrouter.ai/bytedance-seed/seedream-5-5
[wan3-alibaba]: https://www.alibabacloud.com/blog/wan3-0-30-second-ai-video-generation-from-any-input_603452
[minimax-docs]: https://platform.minimax.io/docs/guides/pricing-video
[bfl-release]: https://docs.bfl.ml/release-notes
[flux3-layer3]: https://www.layer3labs.io/guides/flux-3-image-pricing
[runway-toolcolumn]: https://www.toolcolumn.com/learn/runway-web-credits-vs-api-pricing
[luma-picasso]: https://blog.picassoia.com/luma-api-pricing-ray-3-2-api-docs-and-cost
[pika-apiframe]: https://apiframe.ai/guides/pika-labs-api-guide
[nbpro-argolink]: https://argolink.io/en/blog/nano-banana-pro-api-pricing
[gptimg-eesel]: https://www.eesel.ai/blog/chatgpt-images-2-6-pricing
[gptimg-dev]: https://dev.to/alanwest/openai-images-26-vs-25-same-token-price-up-to-42x-the-cost-per-image-554f
[openai-verify]: https://community.openai.com/t/gpt-images-1-403-what-are-the-conditions-for-requesting-this-model-gpt-image-1/1245846
[ideogram-glb]: https://www.glbgpt.com/hub/ideogram-4-5-review/
[ideogram-alpha]: https://alphasignal.ai/news/ideogram-4-5-fights-edit-drift-with-27x-pricing-spread-and-multi-turn-precision
[recraft-pricing]: https://www.recraft.ai/docs/api-reference/pricing
[eleven-puter]: https://developer.puter.com/tutorials/elevenlabs-api-pricing/
[eleven-terms]: https://terms.law/ai-output-rights/elevenlabs/
[eleven-consent]: https://terms.law/forum/thread/elevenlabs-voice-clone-legal.html
[sync-docs]: https://sync.so/docs/models/lipsync
[sync-wavespeed]: https://wavespeed.ai/models/sync/lipsync-3
[veed-lipsync]: https://fal.ai/veed-lipsync-v2
[kling-lipsync]: https://fairstack.ai/models/kling-lipsync-a2v
[h3-lipsync]: https://fal.ai/models/minimax/h3-max/lip-sync/image-to-video
[topaz-yotta]: https://www.yottalabs.ai/post/topaz-labs-starlight-precise-2-6-vs-fast-3-video-upscale-api
[topaz-llmstats]: https://llm-stats.com/models/topaz-video-upscale
[meshy-pricing]: https://docs.meshy.ai/en/api/pricing
[tripo-pricing]: https://developers.tripo3d.ai/en/pricing
[hunyuan-apitariff]: https://apitariff.com/models/fal-ai-hunyuan3d-v3-image-to-3d/
[sam3d-fal]: https://fal.ai/models/fal-ai/sam-3/3d-objects
[bg-aireiter]: https://aireiter.com/blog/best-background-removal-api
[lora-fal-flux2]: https://fal.ai/models/fal-ai/flux-2-trainer
[lora-techinsider]: https://tech-insider.org/train-custom-ai-image-lora-2026/
[fal-api-terms]: https://fal.ai/legal/api-services
[fal-dpa]: https://fal.ai/legal/data-processing-addendum
[fal-trust]: https://fal.ai/legal/trust-and-safety
[fal-concurrency]: https://fal.ai/docs/documentation/model-apis/concurrency-limits
[fal-status]: https://status.fal.ai/cmtn4hy2u0d4r1mqj4tgiir1w
[fal-signunder]: https://signunder.com/platforms/fal
[fal-review]: https://magichour.ai/blog/fal-ai-review
[fal-vs-replicate]: https://www.teamday.ai/blog/fal-ai-vs-replicate-comparison
[replicate-terms]: https://replicate.com/terms
[replicate-limits]: https://replicate.com/docs/topics/predictions/rate-limits
[replicate-cf]: https://the-decoder.com/cloudflare-acquires-replicate-with-its-50000-ai-models/
[runware-terms]: https://runware.ai/terms
[runware-zdr]: https://runware.ai/blog/runware-zero-data-retention
[wavespeed-review]: https://gengrades.com/wavespeed-ai
[kie-review]: https://gengrades.com/kie-ai
[kie-sharkly]: https://sharkly.ai/blog/is-kie-ai-legit/
[atlas-aup]: https://www.atlascloud.ai/acceptable-use
[openrouter-fee]: https://openrouter.ai/blog/announcements/simplifying-our-platform-fee/
[together-wan]: https://www.together.ai/blog/wan-2-7-now-available-on-together-ai
[everypixel-licenses]: https://journal.everypixel.com/ai-video-commercial-use
[hf-api-blog]: https://higgsfield.ai/blog/higgsfield-api
[hf-open-pricing]: https://open.higgsfield.ai/pricing
[hf-terms]: https://higgsfield.ai/terms-of-use-agreement
[hf-vs-sub]: https://higgsfield.ai/blog/ai-video-api-pricing-vs-subscriptions
[hf-catclaw]: https://www.catclaw.ai/guides/higgsfield-api-pricing-and-access
[hf-apiframe]: https://apiframe.ai/guides/higgsfield-api-guide
[hf-commercial]: https://aliteq.com/higgsfield-commercial-use

Lista źródeł (wszystkie odczytane 2026-11-13 przez WebSearch, o ile nie zaznaczono inaczej):

- Katalog Vercel AI Gateway, odczyt na żywo przez MCP: <https://vercel.com/ai-gateway/models>; dokumentacja wideo: <https://vercel.com/docs/ai-gateway/modalities/video-generation>; brak marży: <https://vercel.com/changelog/seedance-2.0-video-now-available-on-ai-gateway>
- Katalog modeli Higgsfield, odczyt na żywo przez MCP (`models_explore`)
- Sora: <https://techjacksolutions.com/ai-brief/openai-videos-api-sora-2-deprecated-september-2026/>
- Veo / Omni: <https://www.veopricing.com/veo-3-1-api-providers/>, <https://ai.google.dev/gemini-api/docs/veo>, <https://www.usagepricing.com/blueprint/activity/fal-ai-2026-10-15-veo-31-deprecation-date>, <https://www.eesel.ai/blog/gemini-omni-1-2-flash-pricing>
- Kling: <https://kling.ai/dev/pricing>, <https://vidirect.org/tools/kling/pricing>, <https://aireiter.com/blog/kling-4-0-api-pricing-fal-cost-vs-seedance-vidu>, <https://www.orcarouter.ai/blog/kling-4-0-flash-general-availability>, <https://rendercents.com/pricing/kling-3-0-api>, <https://felloai.com/kling-ai-pricing/>
- Seedance / Seedream / BytePlus: <https://argolink.io/en/blog/seedance-2-5-api-pricing>, <https://fal.ai/models/bytedance/seedance-2.5/us/reference-to-video>, <https://ofox.ai/blog/seedance-2-5-price-audit-bytedance-formula-2026/>, <https://seedrouter.ai/blog/seedance-real-person-error>, <https://byteplus-sa.github.io/ComfyUI-BytePlus-ModelArk/concepts/keys-and-regions/>, <https://toolso.ai/tool/byteplus>, <https://openrouter.ai/bytedance-seed/seedream-5-5>
- Wan, MiniMax, BFL, Runway, Luma, Pika: <https://www.alibabacloud.com/blog/wan3-0-30-second-ai-video-generation-from-any-input_603452>, <https://platform.minimax.io/docs/guides/pricing-video>, <https://docs.bfl.ml/release-notes>, <https://www.layer3labs.io/guides/flux-3-image-pricing>, <https://www.toolcolumn.com/learn/runway-web-credits-vs-api-pricing>, <https://blog.picassoia.com/luma-api-pricing-ray-3-2-api-docs-and-cost>, <https://apiframe.ai/guides/pika-labs-api-guide>
- Obraz: <https://argolink.io/en/blog/nano-banana-pro-api-pricing>, <https://www.eesel.ai/blog/chatgpt-images-2-6-pricing>, <https://dev.to/alanwest/openai-images-26-vs-25-same-token-price-up-to-42x-the-cost-per-image-554f>, <https://community.openai.com/t/gpt-images-1-403-what-are-the-conditions-for-requesting-this-model-gpt-image-1/1245846>, <https://www.glbgpt.com/hub/ideogram-4-5-review/>, <https://alphasignal.ai/news/ideogram-4-5-fights-edit-drift-with-27x-pricing-spread-and-multi-turn-precision>, <https://www.recraft.ai/docs/api-reference/pricing>
- Audio: <https://developer.puter.com/tutorials/elevenlabs-api-pricing/>, <https://terms.law/ai-output-rights/elevenlabs/>, <https://terms.law/forum/thread/elevenlabs-voice-clone-legal.html>
- Narzędzia: <https://sync.so/docs/models/lipsync>, <https://wavespeed.ai/models/sync/lipsync-3>, <https://fal.ai/veed-lipsync-v2>, <https://fairstack.ai/models/kling-lipsync-a2v>, <https://fal.ai/models/minimax/h3-max/lip-sync/image-to-video>, <https://www.yottalabs.ai/post/topaz-labs-starlight-precise-2-6-vs-fast-3-video-upscale-api>, <https://llm-stats.com/models/topaz-video-upscale>, <https://docs.meshy.ai/en/api/pricing>, <https://developers.tripo3d.ai/en/pricing>, <https://apitariff.com/models/fal-ai-hunyuan3d-v3-image-to-3d/>, <https://fal.ai/models/fal-ai/sam-3/3d-objects>, <https://aireiter.com/blog/best-background-removal-api>, <https://fal.ai/models/fal-ai/flux-2-trainer>, <https://tech-insider.org/train-custom-ai-image-lora-2026/>
- Agregatory i regulaminy: <https://fal.ai/legal/api-services>, <https://fal.ai/legal/data-processing-addendum>, <https://fal.ai/legal/trust-and-safety>, <https://fal.ai/docs/documentation/model-apis/concurrency-limits>, <https://status.fal.ai/cmtn4hy2u0d4r1mqj4tgiir1w>, <https://signunder.com/platforms/fal>, <https://magichour.ai/blog/fal-ai-review>, <https://www.teamday.ai/blog/fal-ai-vs-replicate-comparison>, <https://replicate.com/terms>, <https://replicate.com/docs/topics/predictions/rate-limits>, <https://the-decoder.com/cloudflare-acquires-replicate-with-its-50000-ai-models/>, <https://runware.ai/terms>, <https://runware.ai/blog/runware-zero-data-retention>, <https://gengrades.com/wavespeed-ai>, <https://gengrades.com/kie-ai>, <https://sharkly.ai/blog/is-kie-ai-legit/>, <https://www.atlascloud.ai/acceptable-use>, <https://openrouter.ai/blog/announcements/simplifying-our-platform-fee/>, <https://www.together.ai/blog/wan-2-7-now-available-on-together-ai>, <https://journal.everypixel.com/ai-video-commercial-use>
- Higgsfield API: <https://higgsfield.ai/blog/higgsfield-api>, <https://open.higgsfield.ai/pricing>, <https://higgsfield.ai/terms-of-use-agreement>, <https://higgsfield.ai/blog/ai-video-api-pricing-vs-subscriptions>, <https://www.catclaw.ai/guides/higgsfield-api-pricing-and-access>, <https://apiframe.ai/guides/higgsfield-api-guide>, <https://aliteq.com/higgsfield-commercial-use>
