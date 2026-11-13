# 01 - Mapa produktu i funkcji Higgsfield (stan na 2026-11-13)

> Metoda: WebSearch (tryb extended) plus odczyt (read-only, bez wydawania kredytów) oficjalnego serwera Higgsfield MCP: katalog modeli, galerie presetów, cennik GPU, lista workflow. Bezpośredni WebFetch stron (higgsfield.ai, techcrunch.com, wikipedia.org) był zablokowany przez politykę sieci, więc daty z changeloga pochodzą z podsumowań wyników wyszukiwania tej strony, nie z pełnego odczytu. Tagi: **[zweryfikowane]** = jest źródło, **[wnioskowanie]** = moja dedukcja, **[niepewne]** = źródła sprzeczne lub słabe. Nazwy własne (Soul, Cinema Studio, Genjutsu itd.) są znakami Higgsfield i służą tu wyłącznie jako odniesienie badawcze.

## TL;DR

- Higgsfield to agregator ok. 140 pozycji modelowych (51 image, 60 video, 11 audio, 18 3D) od ok. 20 dostawców, opakowany w studia, presety i agenta; własne są głównie warstwy "smaku" (Soul, Cinema Studio, Genjutsu) i workflow, nie modele bazowe [zweryfikowane: MCP tool output].
- Skala: run rate 1,35 mld USD (październik 2026, liczone jako 4 tygodnie x 13), 32 mln+ użytkowników, prawie 1 mln płacących, wycena 5,4 mld USD po Series B 400 mln USD [zweryfikowane: [SaaStr](https://www.saastr.com/higgsfield-went-from-1b-to-1-35b-in-run-rate-in-one-month-now-its-aiming-for-2b-by-year-end/), [blog HF](https://higgsfield.ai/blog/higgsfield-1b-annualized-revenue-run-rate), [TechCrunch](https://techcrunch.com/2026/08/17/higgsfield-raises-400m-series-b-quadrupling-its-valuation-in-8-months-to-5-4b/)]. Liczby są deklaracjami firmy, nieaudytowane.
- Pieniądze robi marketing: w styczniu 2026 85% użycia pochodziło od social media marketerów; subskrypcje spadły z >90% do nieco ponad 60% przychodu na rzecz dokupywanych kredytów [zweryfikowane: [Sacra](https://sacra.com/c/higgsfield/)].
- Kadencja: wpis w changelogu średnio co 1-2 dni; nowe modele zwykle 0-1 dnia po udostępnieniu API dostawcy [zweryfikowane/wnioskowanie, sekcja 5].
- Od kwietnia 2026 firma przesuwa się z "galerii narzędzi" w stronę agenta i dystrybucji poza własnym UI: MCP (30.04), Canvas (ok. 29.04), Supercomputer (14-15.05), API pay-per-generation (16.09), pluginy Adobe/Figma/Resolve.
- Brak oficjalnej aplikacji mobilnej (tylko web responsywny) i brak darmowych kredytów na planie Free [zweryfikowane: [help center](https://higgsfield.ai/creator-hub/help-center/getting-started/official-higgsfield-platforms), [Krea](https://www.krea.ai/blog/what-is-higgsfield-ai-pricing-free-plan-and-alternatives-in-2026)].
- Dla solo foundera realny MVP to grupy 1-6 taksonomii z sekcji 7; buildery gier/stron, GPU rental, 3D scene builder i manga to "skip-for-now".

## 1. Firma

| Parametr | Wartość | Status |
|---|---|---|
| Założenie | 2023, Alex Mashrabov (ex-Snap, wcześniej AI Factory) i Erzat Dulat | [zweryfikowane: [Wikipedia](https://en.wikipedia.org/wiki/Higgsfield_AI)] |
| HQ | San Francisco; największy zespół w Azji Centralnej (ok. 60% headcountu wg Revelio) | [zweryfikowane: [Revelio](https://www.reveliolabs.com/companies/higgsfield/employees)] |
| Pierwszy produkt | Aplikacja mobilna Diffuse (kwiecień 2024), seed 8 mln USD (Menlo Ventures) | [zweryfikowane: [BusinessWire](https://www.businesswire.com/news/home/20240403369573/en/Higgsfield-AI-Secures-$8M-in-Seed-Funding-to-Unlock-Personalized-AI-Video-Creation)] |
| Series A | 50 mln USD (09.2025) + 80 mln USD (01.2026) = 130 mln USD przy wycenie 1,3 mld USD; Accel, Menlo, GFT, AI Capital Partners | [zweryfikowane: [TechCrunch](https://techcrunch.com/2026/01/15/ai-video-startup-higgsfield-founded-by-ex-snap-exec-lands-1-3b-valuation)] |
| Series B | 400 mln USD, 17.08.2026, wycena 5,4 mld USD, lead DST Global; Goldman Sachs Alternatives, Intel Capital, Tribe, Valor | [zweryfikowane: [TechCrunch](https://techcrunch.com/2026/08/17/higgsfield-raises-400m-series-b-quadrupling-its-valuation-in-8-months-to-5-4b/), [Intel Capital](https://www.intelcapital.com/higgsfield-raises-400-million-series-b-financing-at-5-4-billion-valuation-with-annualized-revenue-reaching-700-million/)] |
| Rozszerzenie B | 23.10.2026, TCV i NVIDIA, kwota nieujawniona | [zweryfikowane: [blog HF](https://higgsfield.ai/blog/higgsfield-series-b-extension-tcv-nvidia)] |
| Run rate | ok. 200 mln (01.2026), 500 mln (06), 700 mln (08), 1 mld (09), 1,35 mld USD (10.2026); cel 2 mld w 3 miesiące | [zweryfikowane: [SaaStr](https://www.saastr.com/higgsfield-went-from-1b-to-1-35b-in-run-rate-in-one-month-now-its-aiming-for-2b-by-year-end/); SaaStr Fund jest inwestorem] |
| Użytkownicy | 30 mln+ (08.2026), 32 mln+ i prawie 1 mln płacących (09.2026); "390 z Fortune 500" | [zweryfikowane jako deklaracja firmy: [blog HF](https://higgsfield.ai/blog/higgsfield-1b-annualized-revenue-run-rate)] |
| Zespół | 160 (PitchBook/SaaStr), 378 (Revelio, 03.2026), 650 (Tracxn, 09.2026) | [niepewne: źródła rozbieżne; [Tracxn](https://tracxn.com/d/companies/higgsfield/__HOGu4TInAP4ifiKkUkJ2LqOJJnDsgiF12TQdX5qsv9Q)] |

Ryzyka reputacyjne istotne dla naśladowcy: zawieszenie konta X w lutym 2026 i spór o licencję "perpetual, irrevocable" w ToS z lipca 2026 [zweryfikowane: [AI Photo Labs](https://aiphotolabs.com/news/higgsfieldai-x-fiasco), [BottleRocket](https://www.bottlerocketcontent.com/higgsfield-tos-controversy-explained/)].

## 2. Architektura produktu (jak to jest poukładane)

Cztery warstwy [wnioskowanie na podstawie katalogu MCP]:

1. **Katalog modeli zewnętrznych** z jednolitym schematem parametrów (role mediów, aspect ratio, czas, tryb) i routerem "Auto".
2. **Modele/pipeline'y markowane jako własne** (27 pozycji z providerem "Higgsfield"), z których część jawnie stoi na cudzych modelach: Ad Multiplier "powered by Seedance 2.5", 3D Jutsu Angles "powered by Seedream 5.0 Pro", Genjutsu Lite na Wan 3.0 i Kling 4.0 [zweryfikowane: MCP tool output].
3. **Studia i presety**: formularze nad pipeline'ami (Marketing Studio, Cinema Studio, Apps, Viral).
4. **Agent i dystrybucja**: Supercomputer, Canvas, MCP/CLI/Skills, API, pluginy.

Część modeli (Inworld TTS, Mirelo SFX, Sonilo Music) ma w katalogu providera "FAL", czyli Higgsfield sam korzysta z pośredników inference [zweryfikowane: MCP tool output]. To potwierdza, że model "agregator na agregatorze" jest wykonalny.

## 3. Inwentarz powierzchni produktu

### 3.1 Generacja bazowa

| Powierzchnia | Co robi / dla kogo | Modele pod spodem (katalog MCP, 13.11.2026) | Gating |
|---|---|---|---|
| Image | T2I, edycja instrukcją, multi-reference, SVG/GIF; wszyscy | Nano Banana (1, 2, 2 Lite, 2.1, Pro), GPT Image 2/2.5/2.6, Seedream 4.5/5.0/5.5, FLUX.2, FLUX 3, Flux Kontext, Ideogram 4.5 i Vector, Recraft V4.1, Grok Image 2.0, Kling O1 Image, MiniMax H3 Image, Z Image + Soul | Starter: wybrane modele; Plus/Ultra: wszystkie [zweryfikowane: [cennik HF](https://higgsfield.ai/blog/higgsfield-pricing-explained)] |
| Video | T2V, I2V, first/last frame, keyframes, reference-to-video, video edit, extend, natywne audio | Kling 2.6/3.0/3.0 Omni/4.0/4.0 Flash, Veo 3.1 i Lite, Seedance 2.0/2.0 Mini/2.5/2.5 Flash, Wan 2.6/2.7/3.0/3.0 Prime, MiniMax Hailuo/H3, Grok Video 1.5, FLUX 3 Video, Gemini Omni Flash 1.1/1.2, Happy Horse | Starter bez Seedance 2.5 i Veo 3.1 [niepewne: [Krea](https://www.krea.ai/blog/what-is-higgsfield-ai-pricing-free-plan-and-alternatives-in-2026)] |
| Audio | TTS (do 10 głosów w dialogu), klonowanie głosu z próbki, voice change, dubbing, muzyka | Eleven v4 i Turbo, ElevenLabs Music v2/v2.5, ElevenLabs Dubbing, Seed Audio 1.0, Qwen Audio 3.0 TTS, "Text to Speech V2" (silniki ElevenLabs, MiniMax, Seed Speech, Vibe Voice, Cozy Voice) | Plany płatne [zweryfikowane: MCP; [voice-over](https://higgsfield.ai/ai-voice-over)] |
| 3D (assety) | Image/text do GLB, rigging, remesh, retexture | Meshy 5/6/7, Tripo H3.1/P2, Hunyuan3D v3/v3.1, Meta SAM 3 3D | Kredyty [zweryfikowane: MCP] |

Sora 2 nie ma w katalogu: OpenAI wyłączył modele i Videos API 24.09.2026 [zweryfikowane: [blog HF](https://higgsfield.ai/blog/sora-api-migration-guide)]. To konkretny przykład ryzyka zależności od dostawcy.

### 3.2 Studia i modele własnej marki

| Powierzchnia | Co robi | Start | Uwagi / gating |
|---|---|---|---|
| Soul 2.0 (+ Soul Cinema, Soul Cast, Soul Location) | Fotorealistyczny model obrazu pod UGC, modę, postacie; galeria stylów | Soul 2.0: 26.02.2026 [zweryfikowane: [changelog](https://higgsfield.ai/creator-hub/changelog)] | W zestawie Unlimited; ok. 0,125 kredytu/obraz [niepewne: [geo.higgsfield](https://geo.higgsfield.ai/higgsfield-ai-pricing-guide)] |
| Soul ID | Trening tożsamości postaci z 20-80 zdjęć, 3-5 min, 25 kredytów; działa w całej rodzinie Soul i przez "Elements" w video | 2025 [niepewne] | Tylko plany płatne [zweryfikowane: [help](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-create-and-use-a-soul-id-character)] |
| Cinema Studio 4.0 | Studio filmowe: Director's Panel (korpus kamery, 5 obiektywów, przysłona, światło), sceny multi-shot do 30 s, do 50 referencji, Elements (postacie, lokacje, rekwizyty) | 3.0: 31.03.2026; 3.5: 04-05.2026; 4.0: 12.08.2026 (PR 28.10) [niepewne co do dat; [blog](https://higgsfield.ai/blog/cinema-studio-4-0), [PR](https://www.morningstar.com/news/pr-newswire/20261028ny82854/higgsfield-cinema-studio-40-gives-ai-filmmakers-more-control-over-every-scene)] | Nigdy w Unlimited; 4.0 podobno na Seedance 2.5 [niepewne] |
| Popcorn / Storyboard | Sekwencje do 8 spójnych klatek, tryb Auto i Manual, do 4 referencji; wejście do Cinema Studio | 2025 [niepewne] | [zweryfikowane: [help](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-use-popcorn)] |
| Genjutsu | Video-to-video: Motion Transfer, Object Swap, Restyle (20+ stylów animacji); także API i node ComfyUI | 31.08-01.09.2026; Restyle 30.09 [zweryfikowane: [changelog](https://higgsfield.ai/creator-hub/changelog), [X](https://x.com/higgsfield_ai/status/2105412853914284117)] | 3 darmowe generacje na Plus/Ultra |
| Katana | Skill dla Claude: remiks wideo referencyjnego z własnymi osobami/produktami (do 5 zdjęć) | 12.10.2026 [zweryfikowane: [blog](https://higgsfield.ai/blog/higgsfield-katana)] | Przez MCP |
| Lipsync Studio / Speak 2.0 / Intone | Talking head ze zdjęcia + audio, dialog 2 postaci, dubbing z lipsync (18 języków wg strony produktu) | Speak: 2025; Intone: 2026 [niepewne] | Modele: Veo 3.1, Kling Lipsync/Avatars 2.0, Wan 2.5 Speak, Infinite Talk, Sync Lipsync 3 [zweryfikowane: [help](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-use-lipsync-voiceover-and-aspect-ratios)] |

### 3.3 Marketing, reklamy, UGC

| Powierzchnia | Co robi | Start | Uwagi |
|---|---|---|---|
| Marketing Studio | Link do produktu lub zdjęcie, auto Brand Kit, awatar (40+ gotowych lub własny), 9 formatów reklamy (UGC, unboxing, tutorial, TV spot, try-on...), klipy do 15 s | 04.2026, na Seedance 2.0 [zweryfikowane: [X](https://x.com/higgsfield/status/2043752265472004424), [ai-ad-generator](https://higgsfield.ai/ai-ad-generator)] | Galeria szablonów: 649 pozycji (product shots, product shots z ludźmi, hypermotion, mixed media, 2D motion, SaaS motion) [zweryfikowane: MCP] |
| Ads Studio | Statyczne kreacje z copy (Meta), brand z URL, batch do 20 reklam/produkt (30.09), wideo reklamy (09.11) | 09-11.2026 [zweryfikowane: [changelog](https://higgsfield.ai/creator-hub/changelog)] | |
| Ad Multiplier | Z jednej reklamy 4-30 s wiele wariantów (osoba, produkt, tło, tekst) lub "recreate" pod inny rynek/język | 08-10.2026 [niepewne co do daty; [blog](https://higgsfield.ai/blog/ad-multiplier-ads-studio)] | Seedance 2.5 [zweryfikowane: MCP] |
| Product shots / Click to Ad / Product Placement | Packshoty, lifestyle, try-on, karuzele | 2025-2026 | Workflow "product-photoshoot" w MCP |
| UGC / Shorts Studio / Content Factory / Faceless | Gotowe krótkie formy: prezenter AI 9:16 (15 s-2 min), "What if" 15 s-5 min, narracja + napisy | Shorts: ok. 07.2026, relaunch 03.11; Content Factory: 22.10.2026 [zweryfikowane: [blog](https://higgsfield.ai/blog/higgsfield-introduces-shorts-studio), [blog](https://higgsfield.ai/blog/higgsfield-introduces-content-factory)] | |
| AI Influencer Studio + Earn | Kreator postaci z menu (ok. 20 grup cech), arkusz postaci, animacja; program wypłat za wyświetlenia (pula 100 tys. USD/tydz., limit 2 500 USD/wideo) | 01.2026, przebudowa 03.10.2026 [niepewne co do dat; [Earn](https://higgsfield.ai/earn)] | 10 darmowych generacji Starter, 30 Plus/Ultra |
| Virality Predictor / Video Analysis | Ocena klipu do 15 s: viral potential, hook score, hold rate, "heatmapa mózgu" (metodologia nieujawniona) | 09.05.2026, preview bez kredytów [zweryfikowane: [X](https://x.com/higgsfield/status/2053139109074657482)] | |
| Publikacja social | Konektory agenta: Instagram, Threads, X (LinkedIn sporny), 32 narzędzia; TikTok publish i trendująca muzyka w MCP | 25.05.2026 [zweryfikowane: [social-connectors](https://higgsfield.ai/social-connectors); TikTok: nazwy narzędzi MCP] | Wszystkie plany płatne |

### 3.4 Apps, presety, efekty

- **Apps**: 80+ jednocelowych narzędzi (Face Swap, Video Face Swap, Recast, Character Swap 2.0, Headshot Generator, Click to Ad...) [zweryfikowane: [apps](https://higgsfield.ai/apps), [blog](https://higgsfield.ai/blog/The-Complete-Guide-to-Viral-Higgsfield-Apps)].
- **Viral presets**: 87 presetów typu "chain" (wieloetapowy pipeline) w kategoriach Motion / Product shot / Effects [zweryfikowane: MCP]; firma dokłada paczki po kilkanaście (13 nowych 10.08.2026).
- **Marketplace apps** wywoływane przez MCP (np. zestaw match-cut/tracking z 28 akcjami) [zweryfikowane: MCP].
- Presety to zapisane łańcuchy prompt + model + parametry + sloty wejść, a nie osobne modele [wnioskowanie]. To najtańsza technicznie i najbardziej "contentowa" część produktu.

### 3.5 Edycja i ulepszanie

| Typ | Funkcje | Modele |
|---|---|---|
| Obraz | Inpaint, Draw to Edit, Layers (dekompozycja), Relight, Angles, Expand (outpaint), Remove BG, Skin Enhancer, Upscale 2K/4K, wektoryzacja | Nano Banana Pro, FLUX.2 Pro Outpaint, Topaz, Bytedance Upscale, Ideogram Vector [zweryfikowane: [image-editing](https://higgsfield.ai/image-editing), MCP] |
| Wideo | Upscale, Reframe, FPS Boost, Deflicker, Remove BG (SAM 3), depth map, SDR do HDR, Draw to Video, 34 color grade'y i 62 looki oświetlenia (jako edycje Seedance 2.5) | Topaz, Bytedance, FLUX 3 Video Upscaler (28.08.2026), Depth Anything [zweryfikowane: MCP, [changelog](https://higgsfield.ai/creator-hub/changelog)] |
| Montaż | Sklejanie klipów, napisy, motion graphics, AI Motion Designer w After Effects (11.09.2026) | Własny silnik renderu + sandbox [zweryfikowane: MCP] |

### 3.6 Agent, Canvas, MCP, API, GPU

| Powierzchnia | Co robi | Start | Gating / cena |
|---|---|---|---|
| Supercomputer | Agent w chmurze: brief, plan, dobór modeli, wykonanie; LLM-y Claude/GPT/Gemini/Kimi/Grok; "AI Employees 2.0" z pamięcią, Scheduled Tasks, App Builder, 30+ konektorów | 14-15.05.2026 [zweryfikowane: [X](https://x.com/higgsfield_ai/status/2054989169446023181)] | Plany płatne; tryb Auto dla tekstu bez kredytów (06.08); storage 20 GB |
| Canvas | Node-based board: prompty, referencje i generacje dowolnych modeli w pipeline, szablony, współpraca | ok. 29.04.2026 [zweryfikowane: [canvas-intro](https://higgsfield.ai/canvas-intro)] | Budowa grafu darmowa, płaci się za generacje |
| MCP + CLI + Skills | Hostowany endpoint, OAuth bez klucza API; Claude, ChatGPT (plugin), Claude Code, Cursor; ok. 170 narzędzi widocznych w tej sesji | 30.04.2026 [zweryfikowane: [mcp.directory](https://mcp.directory/blog/higgsfield-mcp-guide), [help](https://higgsfield.ai/creator-hub/help-center/integrations/how-do-i-connect-higgsfield-to-ai-agent)] | Plan płatny; 3-dniowy trial Plus tylko dla MCP [zweryfikowane: opis narzędzia MCP] |
| API | REST + SDK Python/TS, async + webhooki, płatność tylko za udane generacje, min. doładowanie 5 USD, "50+ modeli" | Pay-per-generation 16.09.2026 [zweryfikowane: [docs](https://docs.higgsfield.ai/docs/help/faq), [help](https://higgsfield.ai/creator-hub/help-center/integrations/what-is-the-higgsfield-api)] | Osobne saldo, bez subskrypcji |
| GPU rental | Wynajem L40S/RTX PRO 6000/H100/H200/B200/B300 (71-197 kredytów za GPU-godzinę, do 8 GPU), otwarte modele (Wan 2.2, LTX Video, Qwen Image, MiniMax H3), import LoRA i modeli z Hugging Face | Data nieznana [niepewne: brak źródła web; istnienie zweryfikowane w MCP] | Kredyty |
| Pluginy | Photoshop, Premiere Pro, After Effects, DaVinci Resolve, Figma | 05-06.2026 [zweryfikowane: [help](https://higgsfield.ai/creator-hub/help-center/integrations/external-integrations-higgsfield)] | Resolve od Plus [niepewne] |

### 3.7 Buildery i formaty niszowe

- **Website / App / Game builder**: trzy typy produktu; "app" loguje przez konto Higgsfield i generuje na kredytach użytkownika; deploy pod linkiem, publikacja w marketplace [zweryfikowane: MCP, [CLI](https://github.com/higgsfield-ai/cli)]. Games 2.0 ok. 04-07.09.2026, Playable (gry mobilne z opisu) 26.10.2026; Playable Ads tylko Enterprise [zweryfikowane: [changelog](https://higgsfield.ai/creator-hub/changelog)].
- **3D Jutsu**: edytowalna scena 3D z promptu (obiekty, kamery, światło, animacja), potem render przez model wideo; 04.09.2026 [zweryfikowane: [changelog](https://higgsfield.ai/creator-hub/changelog)].
- **Mangaka**: agent do mangi/komiksów/webtoonów, 4 style, do 30 rozdziałów, 14 języków; 01.11.2026 [zweryfikowane: [blog](https://higgsfield.ai/blog/higgsfield-introduces-mangaka)].

### 3.8 Społeczność, zespoły, mobile

- **Community**: feed publikacji, konkursy (Global Film Festival z pulą 1 mln USD, 2026), Originals (własne serie AI), Academy [zweryfikowane: [festiwal](https://higgsfield.ai/contests/higgsfield-global-film-festival)].
- **Zespoły**: Team (2-9 miejsc, 1 000 kredytów/miejsce, pula wspólna), Scale (2 500/miejsce, basic SSO), Enterprise (bez limitu miejsc, SSO/SAML, sub-workspace per klient, dedykowane GPU w USA, SOC 2 Type II) [zweryfikowane: [blog](https://higgsfield.ai/blog/higgsfield-pricing-explained), [enterprise](https://higgsfield.ai/enterprise)].
- **Mobile**: brak natywnej aplikacji; redesign interfejsu mobilnego web 24.09.2026 [zweryfikowane: [help](https://higgsfield.ai/creator-hub/help-center/getting-started/official-higgsfield-platforms)].
- **Języki UI**: hiszpański (12.08), koreański i japoński (31.08.2026) [zweryfikowane: changelog].

## 4. Gating planów (skrót)

| Plan | Cena / kredyty | Co odblokowuje |
|---|---|---|
| Free | 0 kredytów, bez wideo | Przeglądanie; okazjonalne triale |
| Starter | 15-19 USD, 200-270 kredytów | Wybrane modele, 2 wideo + 4 obrazy równolegle |
| Plus | 49-59 USD, 1 000-1 200 kredytów | Wszystkie modele, okna Unlimited |
| Ultra | 129 USD, 3 000 (do 9 000) kredytów | Więcej okien Unlimited i równoległości |
| Team / Scale / Enterprise | 65-79 USD / ok. 150-215 USD za miejsce / custom | Wspólna pula, SSO, kontrola wydatków |

[zweryfikowane, ale źródła rozbieżne: październikowy i listopadowy opis cennika na domenach Higgsfield podają różne kwoty ([blog](https://higgsfield.ai/blog/higgsfield-pricing-explained), [geo](https://geo.higgsfield.ai/higgsfield-ai-pricing-guide)); część serwisów podaje starszą drabinkę Basic/Pro/Max]. "Unlimited" to czasowe okna (7 lub 365 dni) na nazwane modele; nie obejmuje Cinema Studio, MCP, CLI, Canvas ani Supercomputera. Kredyty nie przechodzą na kolejny okres; paczki 500/1 000/2 000/4 000 wygasają po 90 dniach.

## 5. Kadencja wydań

- 1-9 listopada 2026: 9 wpisów w 9 dni (Mangaka, Shorts Studio, Kling 4.0 Flash, GPT Image 2.6, Gemini Omni Flash 1.2, Inkling 2 Small, Seedream 5.5, wideo w Ads Studio, fix Klinga). Wrzesień 2026: ponad 20 wpisów [zweryfikowane: [changelog](https://higgsfield.ai/creator-hub/changelog)].
- GPT Image 2.6: OpenAI 04.11, Higgsfield 05.11 (+1 dzień) [zweryfikowane: [Wikipedia](https://en.wikipedia.org/wiki/GPT_Image)].
- Kling 4.0: premiera 15.10, API ok. 21.10, Higgsfield 22.10 [zweryfikowane/niepewne co do daty API: [MartechSeries](https://martechseries.com/video/kling-ai-officially-launches-next-generation-kling-4-0-raising-the-bar-for-professional-grade-video-models/)].
- Seedance 2.5: premiera 31.07, na Higgsfield wg jednego źródła dopiero 08.09 [niepewne: [reapi](https://reapi.ai/blog/seedance-2-5-on-higgsfield)]. Modele ByteDance mają ograniczenia regionalne (Seedream 5.5 poza USA).
- Wniosek: opóźnienie zależy od dostępności API dostawcy, nie od Higgsfield; integracja nowego modelu to u nich 0-1 dnia. Wymaga to adaptera modeli sterowanego konfiguracją, nie kodem per model [wnioskowanie].
- Co najmniej 6 wpisów od lipca do listopada 2026 to komunikaty o awariach dostawców z automatycznym zwrotem kredytów. Refund przy błędzie to funkcja obowiązkowa [zweryfikowane: changelog].

## 6. Co napędza użycie i przychód

- 85% użycia od social media marketerów, 80% z nich robi pracę komercyjną (01.2026) [zweryfikowane: [Sacra](https://sacra.com/c/higgsfield/)].
- Ok. 70% przychodu od agencji przy run rate ok. 300 mln USD; klienci biznesowi stanowią dziś większość [niepewne: wtórne streszczenia wywiadu SaaStr].
- Subskrypcje >90% do ok. 60% przychodu; reszta to top-upy, auto-refill, API [zweryfikowane: Sacra].
- 1,35 mld USD przy ok. 1 mln płacących daje rząd 100 USD miesięcznie na płacącego, czyli wyraźnie ponad cenę Plus. Top-upy i plany zespołowe są kluczowe [wnioskowanie].
- Najmocniej promowane i najgęściej rozwijane w H2 2026: flagowe modele wideo (Seedance, Kling, Veo) jako magnes Unlimited, Marketing/Ads Studio, Soul + Soul ID, viral presets jako kanał akwizycji [wnioskowanie z changeloga i promocji].
- Brak publicznych danych o udziale poszczególnych studiów w przychodzie [niepewne].

## 7. Proponowana taksonomia zdolności

Skala 1-5 (5 = najwyższa wartość / najtrudniejsze). Trudność zakłada budowę na API zewnętrznych przez jedną osobę.

| # | Grupa | Zakres | Wartość | Trudność | Werdykt |
|---|---|---|---|---|---|
| 1 | Rdzeń platformy | Konta, kredyty, kolejka jobów async, webhooki, refund przy błędzie, biblioteka assetów/projektów | 5 | 4 | Table-stakes |
| 2 | Image multi-model | T2I, edycja, multi-reference, router Auto, 5-8 modeli | 5 | 2 | Table-stakes |
| 3 | Video multi-model | T2V, I2V, first/last frame, reference, extend; 4-6 modeli | 5 | 3 | Table-stakes |
| 4 | Presety / efekty / apps | Silnik szablonów "chain" + galeria + CMS | 5 | 2 (tech), 4 (content) | Table-stakes |
| 5 | Narzędzia enhance | Upscale, outpaint, reframe, remove BG, inpaint, relight | 4 | 2 | Table-stakes |
| 6 | Spójność postaci | Najpierw referencje wielozdjęciowe i "elementy"; trening LoRA później | 5 | 3-4 | Table-stakes (lite), differentiator (trening) |
| 7 | Lipsync / talking video / dubbing | Zdjęcie + audio, dubbing z lipsync | 4 | 3 | Table-stakes dla UGC |
| 8 | Audio | TTS, klonowanie głosu, muzyka, SFX | 3 | 2 | Table-stakes (wąsko) |
| 9 | Video-to-video | Motion transfer, character swap, restyle, object replace | 4 | 3 | Differentiator, faza 2 |
| 10 | Marketing / Ads / UGC studio | URL do reklamy, brand kit, awatary, product shots, batch wariantów | 5 | 4 | Differentiator nr 1 (tu jest przychód) |
| 11 | Studio filmowe | Panel kamery/obiektywu jako warstwa promptów, storyboard, multi-shot | 4 | 3-4 | Differentiator, faza 2 |
| 12 | Agent + MCP + API | Czat-orkiestrator, serwer MCP, publiczne API | 4 | 3-4 | Differentiator; MCP tanie przy czystym backendzie |
| 13 | Canvas / node workflow | Graf generacji, szablony pipeline'ów | 3 | 5 | Skip-for-now |
| 14 | Społeczność i dystrybucja | Feed, konkursy, publikacja social, analiza viralowości, zespoły | 3 | 3-4 | Feed lite w fazie 2; reszta później |
| 15 | Nisze | 3D i sceny 3D, buildery stron/gier, GPU rental, manga, monetyzacja influencerów, pluginy desktop | 2 | 5 | Skip-for-now |

Uzasadnienie kolejności [wnioskowanie]: grupy 1-5 dają produkt "wygląda i działa jak Higgsfield" przy niskim ryzyku technicznym. Grupy 6-8 domykają scenariusz UGC. Grupa 10 jest najbliżej pieniędzy i ma najmniej substytutów w języku polskim/EU. Grupy 13 i 15 to u Higgsfield efekt setek ludzi i miliardowego run rate, a nie warunek wejścia na rynek.

## Źródła

- Higgsfield: [changelog](https://higgsfield.ai/creator-hub/changelog), [API changelog](https://docs.higgsfield.ai/docs/changelog), [1 mld run rate](https://higgsfield.ai/blog/higgsfield-1b-annualized-revenue-run-rate), [rozszerzenie Series B](https://higgsfield.ai/blog/higgsfield-series-b-extension-tcv-nvidia), [cennik objaśniony](https://higgsfield.ai/blog/higgsfield-pricing-explained), [przewodnik cenowy](https://geo.higgsfield.ai/higgsfield-ai-pricing-guide), [oficjalne platformy](https://higgsfield.ai/creator-hub/help-center/getting-started/official-higgsfield-platforms), [Soul ID](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-create-and-use-a-soul-id-character), [Cinema Studio 4.0](https://higgsfield.ai/blog/cinema-studio-4-0), [Popcorn](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-use-popcorn), [Katana](https://higgsfield.ai/blog/higgsfield-katana), [Lipsync](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-use-lipsync-voiceover-and-aspect-ratios), [AI voice over](https://higgsfield.ai/ai-voice-over), [AI ad generator](https://higgsfield.ai/ai-ad-generator), [Ad Multiplier](https://higgsfield.ai/blog/ad-multiplier-ads-studio), [Shorts Studio](https://higgsfield.ai/blog/higgsfield-introduces-shorts-studio), [Content Factory](https://higgsfield.ai/blog/higgsfield-introduces-content-factory), [Mangaka](https://higgsfield.ai/blog/higgsfield-introduces-mangaka), [Earn](https://higgsfield.ai/earn), [Apps](https://higgsfield.ai/apps), [przewodnik po Apps](https://higgsfield.ai/blog/The-Complete-Guide-to-Viral-Higgsfield-Apps), [image editing](https://higgsfield.ai/image-editing), [social connectors](https://higgsfield.ai/social-connectors), [Canvas](https://higgsfield.ai/canvas-intro), [MCP help](https://higgsfield.ai/creator-hub/help-center/integrations/how-do-i-connect-higgsfield-to-ai-agent), [API help](https://higgsfield.ai/creator-hub/help-center/integrations/what-is-the-higgsfield-api), [API FAQ](https://docs.higgsfield.ai/docs/help/faq), [integracje](https://higgsfield.ai/creator-hub/help-center/integrations/external-integrations-higgsfield), [Enterprise](https://higgsfield.ai/enterprise), [festiwal](https://higgsfield.ai/contests/higgsfield-global-film-festival), [migracja z Sora](https://higgsfield.ai/blog/sora-api-migration-guide), [CLI na GitHub](https://github.com/higgsfield-ai/cli)
- Posty X Higgsfield: [Marketing Studio](https://x.com/higgsfield/status/2043752265472004424), [Canvas](https://x.com/higgsfield/status/2049582424535830917), [Virality Predictor](https://x.com/higgsfield/status/2053139109074657482), [Supercomputer](https://x.com/higgsfield_ai/status/2054989169446023181), [Genjutsu Restyle](https://x.com/higgsfield_ai/status/2105412853914284117)
- Prasa i analitycy: [TechCrunch 17.08.2026](https://techcrunch.com/2026/08/17/higgsfield-raises-400m-series-b-quadrupling-its-valuation-in-8-months-to-5-4b/), [TechCrunch 15.01.2026](https://techcrunch.com/2026/01/15/ai-video-startup-higgsfield-founded-by-ex-snap-exec-lands-1-3b-valuation), [Intel Capital](https://www.intelcapital.com/higgsfield-raises-400-million-series-b-financing-at-5-4-billion-valuation-with-annualized-revenue-reaching-700-million/), [SaaStr](https://www.saastr.com/higgsfield-went-from-1b-to-1-35b-in-run-rate-in-one-month-now-its-aiming-for-2b-by-year-end/), [Sacra](https://sacra.com/c/higgsfield/), [Wikipedia](https://en.wikipedia.org/wiki/Higgsfield_AI), [BusinessWire](https://www.businesswire.com/news/home/20240403369573/en/Higgsfield-AI-Secures-$8M-in-Seed-Funding-to-Unlock-Personalized-AI-Video-Creation), [Revelio Labs](https://www.reveliolabs.com/companies/higgsfield/employees), [Tracxn](https://tracxn.com/d/companies/higgsfield/__HOGu4TInAP4ifiKkUkJ2LqOJJnDsgiF12TQdX5qsv9Q), [PR Cinema Studio 4.0](https://www.morningstar.com/news/pr-newswire/20261028ny82854/higgsfield-cinema-studio-40-gives-ai-filmmakers-more-control-over-every-scene)
- Strony trzecie: [Krea](https://www.krea.ai/blog/what-is-higgsfield-ai-pricing-free-plan-and-alternatives-in-2026), [mcp.directory](https://mcp.directory/blog/higgsfield-mcp-guide), [reapi.ai](https://reapi.ai/blog/seedance-2-5-on-higgsfield), [MartechSeries](https://martechseries.com/video/kling-ai-officially-launches-next-generation-kling-4-0-raising-the-bar-for-professional-grade-video-models/), [GPT Image, Wikipedia](https://en.wikipedia.org/wiki/GPT_Image), [AI Photo Labs](https://aiphotolabs.com/news/higgsfieldai-x-fiasco), [BottleRocket](https://www.bottlerocketcontent.com/higgsfield-tos-controversy-explained/)
- "MCP tool output": odczyt read-only serwera Higgsfield MCP z 2026-11-13 (models_explore: 140 pozycji; get_presets: 87 presetów viral i 649 szablonów Marketing Studio; gpu_list_gpus; gpu_list_models; get_workflow_instructions: 23 workflow; apps_search; list_website_categories).
