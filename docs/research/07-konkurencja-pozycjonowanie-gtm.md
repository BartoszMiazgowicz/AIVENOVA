# 07 - Konkurencja, pozycjonowanie i go-to-market (stan na 2026-11-13)

## Weryfikacja na żywo (2026-11-13)

Druga tura po napisaniu raportu: 26 zapytań WebSearch (cały przydzielony limit) oraz bezpośredni odczyt stron `github.com`, jedynego hosta otwartego dla WebFetch. `higgsfield.ai`, `trustpilot.com`, `tldraw.dev` i oficjalne cenniki konkurentów pozostają zablokowane, więc ceny pochodzą głównie ze źródeł wtórnych i bywają sprzeczne (zaznaczam to przy liczbach). Tag **[zweryfikowane]** z linkiem w nawiasie oznacza wynik tej tury.

**Potwierdzone**
- Zawieszenie konta X ok. 9.02.2026 i publikacja Forbes o praktykach marketingowych firmy (sekcja 2.2).
- Skargi na zwroty, odnowienia i "unlimited" w opiniach Trustpilot; ocena ok. 4,0/5 (sekcja 2.2).
- Ceny: Leonardo 12-60 USD, Midjourney 10 / 30 / 60 / 120 USD, OpenArt 14-240 USD (pośrednio), Krea 9 i 35 USD oraz 100 darmowych jednostek dziennie, Arcads "100+ USD" (sekcja 1).
- Licencje: React Flow (`xyflow`) MIT i aktywny; `video-starter-kit` MIT; Tersa MIT; `nextjs/saas-starter` MIT; tldraw wymaga płatnego klucza w produkcji (sekcja 4).
- RevenueCat 2026: aplikacje AI zarabiają więcej na płacącym i szybciej tracą subskrybentów (sekcja 5.2).

**Skorygowane**
- Regulamin Higgsfield: zapis "perpetual, irrevocable" usunięto po krytyce (do 26.07.2026), nowe warunki obowiązują od 27.08.2026. Aktualny zarzut to domyślny trening modeli na treściach użytkowników.
- Program afiliacyjny Higgsfield jest publiczny: do 25% przez maks. 12 miesięcy, wypłata w gotówce.
- `Anil-matcha/Open-Higgsfield-AI` nazywa się teraz `Open-Generative-AI` (MIT, 34,3 tys. gwiazdek, zależne od Muapi.ai).
- Tersa jest w `vercel-labs/tersa`; README nie wymienia już Supabase ani Stripe. Ostatni commit 20.02.2026.
- `fal-ai-community/video-starter-kit`: ostatni commit 19.03.2025, projekt nie jest rozwijany.
- `usebasejump/basejump`: README deklaruje "unmaintained".
- ComfyUI przeniesiono do `Comfy-Org/ComfyUI`; `worker-comfyui` ma licencję AGPL-3.0.
- Konkurencja lokalna w klinie nr 1 jest silniejsza, niż zakładałem: UpCreator (polska platforma zdjęć produktowych AI z cenami w PLN, pozycjonowana wprost jako "polska alternatywa dla Higgsfield"), generator grafik i zdjęć AI w panelu Shoper, lepiejsprzedaj.pl. Ocena konkurencji obniżona z 3 do 2 (sekcja 3).
- Uzupełnione kotwice cenowe: Flora, Figma Weave, LTX Studio, Artlist, Invideo, Google Flow, Creatify, HeyGen, Captions (sekcja 1).

**Nadal otwarte**
- Oficjalne cenniki (wszystkie liczby z tej tury pochodzą ze źródeł wtórnych). Rozbieżności: Krea Max 70 czy 105 USD, Freepik, Figma Weave 19 czy 24 USD, Invideo, Artlist, Google AI Plus.
- Blokady kont użytkowników Higgsfield: brak źródeł w dwóch zapytaniach.
- Próg startowy i okno atrybucji afiliacji Higgsfield; czy konto X przywrócono.
- Liczba klientów Base (BaseLinker), stawki Shoper App Store, program aplikacji IdoSell, warunki API Allegro dla aplikacji zewnętrznych.
- Benchmark CAC dla tej kategorii: nie znalazłem żadnego publicznego.
- Czeskie i węgierskie odpowiedniki: jedno zapytanie nic nie zwróciło, co nie dowodzi ich braku.
- `useautumn/autumn`: adres zwraca 404.

> **Ograniczenie pierwszej tury (ważne dla wiarygodności).** Wspólny limit WebSearch był wyczerpany przed moim pierwszym zapytaniem (0 udanych wyszukiwań), WebFetch blokuje polityka sieci (nie rozwiązują się m.in. `higgsfield.ai`, `en.wikipedia.org`, `www.trustpilot.com`, `www.freepik.com`), a konektor GitHub widzi tylko repo projektu. Na żywo zweryfikowałem wyłącznie to, co zwraca oficjalny konektor MCP Higgsfield (odczyt read-only, bez wydawania kredytów). Reszta opiera się na raportach równoległych 01, 03, 04 i 06 (które miały dostęp do wyszukiwarki) oraz na wiedzy modelu do ok. połowy 2026.
>
> Tagi: **[zweryfikowane: MCP]** = odczyt konektora dziś; **[zweryfikowane: R0x]** = źródło na żywo w raporcie równoległym nr x (link podaję); **[niepewne: pamięć]** = wiedza modelu, niezweryfikowana w tej sesji; **[wnioskowanie]** = moja ocena. Ceny i liczby z tagiem "pamięć" trzeba sprawdzić na stronach oficjalnych przed użyciem w planie.

## TL;DR

- Rynek zbiegł się do jednego wzorca: każdy duży gracz (Higgsfield, Freepik, Krea, OpenArt, Leonardo, Artlist) jest agregatorem cudzych modeli. Modele są towarem, a wyróżnia warstwa workflow, szablonów i dystrybucji [wnioskowanie na podstawie R01, R04].
- Higgsfield rośnie czterema dźwigniami: tempo dodawania modeli (0-1 dnia po API), presety viralowe z przyciskiem "Recreate", ciągłe promocje "unlimited" z terminem (16 okien promocyjnych w 3,5 miesiąca) i pieniądze dla twórców (konkursy, wypłaty za wyświetlenia) [zweryfikowane: MCP, R01].
- Te same dźwignie tworzą jego słabości: plan Free bez kredytów, kredyty przepadające co miesiąc, "unlimited" z ograniczeniami, skargi na zwroty i domyślny plan roczny, spór o licencję w regulaminie, zawieszenie konta X [zweryfikowane: R01, R04, MCP]. Cennik jest w USD i nie ma śladów polskiego interfejsu [wnioskowanie z R01 i R04].
- Nowy gracz nie wygra ceną generacji ani szerokością katalogu (R04). Realny klin: **polskie studio reklam produktowych dla e-commerce i agencji**, z ceną w PLN, BLIK, fakturą VAT i cennikiem bez gwiazdek. Po weryfikacji: same zdjęcia produktowe w PLN mają już lokalnych dostawców (UpCreator, generator w panelu Shoper), więc wyróżnikiem musi być wideo reklamowe z polskim lektorem, wybór modeli i formaty marketplace (sekcja 3.1).
- Ekonomia akwizycji jest ciasna: przy wkładzie ok. 8,9 USD na płacącego miesięcznie (R04) dopuszczalny CAC to ok. 15-30 USD. Płatne reklamy B2C się nie spinają; GTM musi stać na SEO, pętlach szablonów, partnerach e-commerce i sprzedaży bezpośredniej do agencji [wnioskowanie].

## 1. Mapa rynku (koniec 2026)

Ceny w USD za miesiąc przy płatności miesięcznej.

### 1.1 Agregatory i studia multi-model

| Gracz | Pozycjonowanie | Kotwica cenowa | Wyróżnik | Słabość (szansa) | Status |
|---|---|---|---|---|---|
| **Higgsfield** | Studio AI dla marketerów social i twórców; ok. 140 modeli + studia + agent | 19 / 59 / 129 | Tempo, 649 szablonów marketingowych, 87 presetów viral, MCP i API | Free = 0 kredytów, brak aplikacji mobilnej, cennik w USD; nowe języki UI w 2026 to ES, KO, JA, polskiego nie odnotowano | [zweryfikowane: R01, R04; Ultra 129 USD / 3 000 kr. potwierdza MCP]; brak polskiego [wnioskowanie] |
| **Freepik** (marka Magnific) | Stock + pakiet AI dla designerów | 20 / 45 / 110 | Unlimited na ok. 30 modelach w planie środkowym; ruch z SEO stocków | Narzędzie ogólne, bez warstwy reklam UGC | [zweryfikowane: R04, źródła wtórne]; w tej turze źródła wtórne podają inne kwoty (wejście 7,50 USD z 96 tys. kredytów rocznie wg jednego porównania; [blog konkurenta OpenArt](https://openart.ai/es-es/blog/freepik-alternatives/) wymienia poziomy 14,5-210 USD) [niepewne], sprawdzić na stronie cennika ([omówienie](https://www.activepieces.com/blog/freepik-pricing-2026-plans-credits-and-what-you-pay)); firma z Hiszpanii, polski interfejs [niepewne: pamięć] |
| **Krea** | Pulpit kreatywny: realtime, wiele modeli, nodes | 9 / 35 / 70 lub 105 | 100 darmowych jednostek dziennie, generacja w czasie rzeczywistym | Dla designerów, nie dla sprzedawców | 100 jednostek dziennie, Basic 9 i Pro 35 USD, Business 200 USD [zweryfikowane]([Costbench](https://costbench.com/software/ai-design-tools/krea-ai/), [usagepricing](https://usagepricing.com/blueprint/krea-ai)); plan Max: 70 USD wg tych źródeł, 105 USD wg R04 [niepewne]; kanwa realtime [zweryfikowane]([Banani](https://www.banani.co/blog/krea-ai-image-review)) |
| **OpenArt** | All-in-one dla twórców, postacie i historie | 14 / 34 / 56 / 240 | Dokupione kredyty przechodzą dalej | Rozproszony UX, brak trybu agencyjnego | [zweryfikowane: R04]; [blog OpenArt](https://openart.ai/blog/best-ai-generators/) podaje 7 USD (Essential, 4 tys. kredytów) do 120 USD (Wonder, 106 tys.), co przy rabacie rocznym do 50% zgadza się z 14-240 USD miesięcznie [zweryfikowane pośrednio]; kredyty z planu nie przechodzą na kolejny miesiąc [zweryfikowane]([ToolQuestor](https://toolquestor.com/vs/openart-ai-vs-leonardo-ai)) |
| **Leonardo** (Canva) | Image-first dla twórców i gier | 12 / 30 / 60 | 150 tokenów dziennie za darmo, bank rollover 3x | Wideo wtórne wobec obrazu | Essential 12 USD do Ultimate 60 USD miesięcznie (10-48 USD przy płatności rocznej), 150 szybkich tokenów dziennie za darmo, Team od 24 USD za miejsce [zweryfikowane]([eesel](https://eesel.ai/blog/leonardo-ai-pricing), [dev.to](https://dev.to/techsifted/leonardo-ai-pricing-2026-free-credits-paid-plans-and-api-costs-16a2)); rollover 3x i własność Canva [niepewne: pamięć] |
| **Flora** | Nieskończony canvas dla zespołów kreatywnych | od ok. 18; pule użycia w USD zamiast kredytów | Canvas + współpraca; narzędzia edycji na canvasie ("Actions") | Krzywa uczenia, nie dla MŚP | Nowy model cenowy z pulami użycia w dolarach (ogłoszony 5.05.2026), plan Free z ograniczoną liczbą generacji [zweryfikowane]([blog Flora](https://flora.ai/blog/a-new-pricing-model-for-flora-plus-nano-banana-on-us), [IT Brief](https://itbrief.co.uk/story/flora-launches-on-canvas-tools-dollar-usage-pools), [FAQ](https://docs.flora.ai/plans-and-billing/faq)); cena wejścia 18 USD wg [porównania wtórnego](https://www.scopeful.org/compare/figma-weave-vs-flora-ai) [niepewne] |
| **Figma Weave** (dawniej Weavy) | Node editor dla profesjonalistów, w ekosystemie Figma | 0 (150 kredytów) / od 19-24 / zespoły 36-48 za osobę | Integracja z Figma; kredyty z rolloverem i wspólną pulą zespołu | Tylko designerzy; osobny abonament obok Figma; API tylko w Enterprise | Nazwa, plan darmowy, trzy plany płatne + Enterprise, osobne rozliczenie [zweryfikowane]([FAQ Weave](https://help.weavy.ai/en/articles/12692387-figma-weave-faq), [Wireflow](https://www.wireflow.ai/blog/figma-weave-pricing), [Banani](https://www.banani.co/blog/figma-pricing-and-credits)); cena wejścia sprzeczna: 19 USD za 1 500 kredytów albo 24 USD ([Scopeful](https://www.scopeful.org/tools/figma-weave)) [niepewne]; data przejęcia 10.2025 [niepewne: pamięć] |
| **ComfyUI** i chmury (Comfy Cloud, RunComfy, Comfy Deploy) | Otwarty silnik node; pełna kontrola | brak danych | Ekosystem custom nodes; Higgsfield sam wydał node dla Genjutsu | Próg wejścia; nie dla mas | Node HF [zweryfikowane: R01]; repozytorium pod [Comfy-Org/ComfyUI](https://github.com/Comfy-Org/ComfyUI), GPL-3.0, 146,5 tys. gwiazdek [zweryfikowane]; ceny chmur [niepewne: pamięć] |
| **Artlist** | Stock muzyki i footage + generacja AI | AI Suite 19,99 (14,99 przy rocznym); Max od 39,99 (roczny) | Licencje i AI w jednym abonamencie; opcja "Unlimited" | Drogi, tylko EN [niepewne: pamięć] | Plany kredytowe: AI Suite 16 500 kredytów, Max 7 500 kredytów plus zasoby; inne źródło podaje plan AI Pro za 149,99 USD [zweryfikowane, liczby częściowo sprzeczne]([blog Artlist](https://artlist.io/blog/ai-tools-pricing-plans/), [pomoc](https://help.artlist.io/hc/en-us/articles/29558520864541-The-AI-Suite-plans-explained)); Artlist publikuje własne [porównanie z Higgsfield](https://artlist.io/blog/?p=69360) [zweryfikowane] |
| **Invideo** | Prompt do gotowego filmu z montażem | Plus 17-25 / Max 85 / Generative 170 / Elite 900 | Długie formy, automatyczny montaż | Szablonowa jakość; rozliczenie kredytowe, w którym agent zużywa kredyty jeszcze przed generacją | Ceny [zweryfikowane, źródła wtórne sprzeczne]([AI Productivity](https://aiproductivity.ai/pricing/invideo/), [Toolradar](https://toolradar.com/tools/invideo-ai/pricing)); uwaga o kredytach agenta za [blogiem konkurenta Creatify](https://creatify.ai/blog/invideo-pricing-%282026%29-plans-credits-and-what-you-ll-actually-pay) |
| **LTX Studio** | Storyboard i film; własny otwarty model | 0 (800 kredytów jednorazowo) / 12 / 35 / 100; rabat roczny 20% | Kontrola ujęć; LTX Video jest w katalogu GPU Higgsfield | Filmowcy, nie reklama MŚP | Katalog [zweryfikowane: R01]; plany Free, Lite, Standard, Pro, Enterprise [zweryfikowane]([blog LTX](https://ltx.studio/blog/ltx-studio-plans)); kwoty ze źródeł wtórnych, częściowo rozbieżnych ([Toolradar, 09.2026](https://toolradar.com/tools/ltx-studio/pricing), [G2](https://g2.com/products/ltx-studio/pricing)) |
| **Canva, CapCut** (sąsiedzi) | Narzędzia masowe z wbudowaną generacją | brak danych | Polski interfejs, lokalne ceny, ogromna baza | Brak głębi: modeli do wyboru, spójności postaci, wariantów reklam | [niepewne: pamięć] |

### 1.2 Aplikacje producentów modeli

| Gracz | Kotwica cenowa | Wyróżnik | Słabość (szansa) | Status |
|---|---|---|---|---|
| **Runway** | 15 / 35 / 95 | Gen-4.5, edycja wideo Aleph 2.0, marka w branży filmowej | Jeden dostawca modeli | [zweryfikowane: R03, R04] |
| **Kling** | 10 / 37 / 92 / 180 | Jakość do ceny; Kling 4.0 od 15.10.2026 | Jurysdykcja chińska: trudny transfer danych przy zdjęciach osób | [zweryfikowane: R01, R04]; ocena transferu wg R06 |
| **Google Flow / Veo** | w pakietach Google AI: Pro 19,99 (1 000 kredytów Flow) / Ultra 99,99 i 199,99 | Veo 3.1 z audio, dystrybucja Google | W UE generacja osób ograniczona do dorosłych; brak presetów reklamowych | Ograniczenie [zweryfikowane: R06 za R03]; ceny [zweryfikowane, źródła wtórne]([omówienie planów](https://sagnikbhattacharya.com/blog/google-veo-pricing-ai-plus-pro-ultra), [Costbench](https://costbench.com/software/ai-video-generators/google-veo/)): Ultra obniżony z 249,99 do 199,99 USD i nowy próg 99,99 USD; klip 8 s Veo 3.1 Fast = 20 kredytów; AI Plus 4,99 albo 7,99 USD i darmowe ok. 50 kredytów dziennie [niepewne, źródła sprzeczne] |
| **Sora** | - | - | **API i modele wyłączone 24.09.2026** | [zweryfikowane: R01, [blog HF](https://higgsfield.ai/blog/sora-api-migration-guide)] |
| **Luma** | 30 / 90 / 300 | Ray3.2 z HDR | Plan free wycofany w 2026 | [zweryfikowane: R03, R04] |
| **Pika** | 10 / 35 / 95 | Prekursor efektów viralowych | Konsumencki churn | Ceny [zweryfikowane: R04]; reszta [niepewne: pamięć] |
| **Midjourney** | 10 / 30 / 60 / 120 | Estetyka, społeczność; wideo z obrazu | Brak API, spory IP ze studiami | Ceny i rabat roczny 20% [zweryfikowane]([eesel](https://www.eesel.ai/en/blog/midjourney-pricing), [Fluxnote](https://fluxnote.io/guides/midjourney-pricing-2026)); wideo tylko z obrazu (bez text-to-video), na wszystkich planach w trybie Fast, HD od planu Standard, wideo SD w trybie Relax w Pro i Mega [zweryfikowane, źródła wtórne]([Hooked](https://www.hooked.so/compare/midjourney-pricing)); brak API i spory IP [niepewne: pamięć] |

### 1.3 Reklama, UGC, awatary

| Gracz | Pozycjonowanie | Wyróżnik | Słabość (szansa) | Status |
|---|---|---|---|---|
| **Creatify** | URL produktu do reklamy wideo | Warianty i testy pod performance | Awatary i lektorzy pod rynek USA [niepewne: pamięć] | Free 10 kredytów miesięcznie, Starter 39 USD (100 kredytów), Pro 99 USD (300 kredytów), czyli ok. 3,30 USD za reklamę 30 s [zweryfikowane]([blog Creatify](https://creatify.ai/blog/the-8-best-ai-ugc-ad-tools-in-2026)) |
| **Arcads** | "Aktorzy AI" do UGC | Realizm | Cena startowa rzędu 100+ USD, wąski zakres | Brak działającego publicznego cennika; raportowane ok. 110 USD za ok. 10 wideo i ok. 220 USD za ok. 20 (ok. 11 USD za wideo), bez triala [zweryfikowane, źródła wtórne, w tym konkurent]([Creatify](https://creatify.ai/blog/arcads-pricing-%282026%29-plans-credits-and-what-you-ll-actually-pay), [Listnr](https://listnr.ai/blog/top-7-arcads-alternatives-in-2026)) |
| **HeyGen** | Awatary i tłumaczenie wideo | Lipsync tłumaczeń; prowadzi blog porównawczy o cenach Higgsfield | Talking head, nie produkt | Blog [zweryfikowane: R04, [HeyGen](https://www.heygen.com/blog/higgsfield-pricing)]; plan Creator 29 USD z 600 kredytami, Avatar IV kosztuje 20 kredytów za minutę wobec 3 dla Avatar III, API rozliczane z osobnego salda [zweryfikowane w streszczeniu wyszukiwania; przewodniki wtórne, m.in. [Atlabs](https://www.atlabs.ai/blog/atlabs-ai-vs.-heygen-vs.-creatify-vs.-arcads-vs.-viralinn-which-ai-ugc-tool-is-actually-worth-paying-for-in-2026), [Cinerads](https://www.cinerads.com/blog/heygen-alternatives-2026)] |
| **Synthesia** | Awatary dla szkoleń enterprise | Compliance, sprzedaż korporacyjna | Nie reklama, nie social | [niepewne: pamięć] |
| **Captions** | Mobilny montaż i napisy z AI | Mobile-first | Konsumencki | Free / Max 24,99 / Scale 69,99-279,99 / Enterprise; plan Pro za 9,99 USD wycofany 23.07.2026 [zweryfikowane, źródła wtórne]([Activepieces](https://www.activepieces.com/blog/captions-pricing-2026-all-five-plans-compared), [Costbench](https://costbench.com/software/ai-video-generators/captions/)); istnienie planu darmowego sporne [niepewne] |

### 1.4 Wnioski z mapy

1. Progi cenowe rynku to 9-15 / 29-37 / 79-105 USD, a darmowe plany kurczą się u wszystkich [zweryfikowane: R04].
2. Pieniądze są w marketingu: 85% użycia Higgsfield pochodziło w 01.2026 od social media marketerów, a subskrypcje spadły z ponad 90% do ok. 60% przychodu na rzecz doładowań [zweryfikowane: R01, [Sacra](https://sacra.com/c/higgsfield/)].
3. Zależność od dostawcy jest realna: Sora zniknęła z rynku API 24.09.2026, a Higgsfield od lipca do listopada 2026 ogłosił co najmniej 6 awarii dostawców [zweryfikowane: R01].
4. Fraza "Higgsfield pricing" jest już zatłoczona: piszą o niej Krea, HeyGen i kilkanaście małych serwisów (lista źródeł R04). Angielskie SEO porównawcze to walka z finansowanymi graczami; polskie frazy są najpewniej dużo słabiej obsadzone [wnioskowanie, do sprawdzenia w Senuto lub Ahrefs]. Korekta po weryfikacji: frazy wokół "zdjęcia produktowe AI" nie są puste. Polskie strony mają m.in. [Pollo AI](https://pollo.ai/pl/ai-product-photo-generator), [Dreamina/CapCut](https://dreamina.capcut.com/pl-pl/ai-image/ai-product-image-tools-reference-campaigns-2026), agencja [Marszal Studio](https://marszalstudio.pl/zdjecia-produktowe/) z serią poradników oraz [UpCreator](https://upselli.pl/blog/upcreator-polska-alternatywa-higgsfield-zdjecia-produktowe-ai), który celuje wprost we frazę "polska alternatywa dla Higgsfield" [zweryfikowane]. Polskich stron o wideo reklamowym AI wyszukiwanie nie zwróciło.
5. Konkurenci sami tworzą treści porównawcze przeciw sobie: Creatify opisuje ceny Invideo i Arcads, Artlist i HeyGen porównują się z Higgsfield, a Higgsfield publikuje [własną listę alternatyw dla Creatify](https://higgsfield.ai/blog/best-creatify-alternatives) [zweryfikowane]. Część liczb w tej sekcji pochodzi z takich stron, więc trzeba je czytać z rezerwą.

## 2. Playbook wzrostu Higgsfield

Skala według deklaracji firmy: run rate ok. 200 mln USD (01.2026), 1,35 mld USD (10.2026), 32 mln+ użytkowników, prawie 1 mln płacących, wycena 5,4 mld USD [zweryfikowane: R01, [TechCrunch](https://techcrunch.com/2026/08/17/higgsfield-raises-400m-series-b-quadrupling-its-valuation-in-8-months-to-5-4b/), [SaaStr](https://www.saastr.com/higgsfield-went-from-1b-to-1-35b-in-run-rate-in-one-month-now-its-aiming-for-2b-by-year-end/)]. Liczby nieaudytowane.

### 2.1 Taktyki i dowody

| Taktyka | Dowód | Status |
|---|---|---|
| Presety viralowe jako akwizycja | 87 presetów "chain", 80+ jednocelowych apps, paczki po kilkanaście nowych; preset ma przycisk "Recreate" | [zweryfikowane: R01, MCP] |
| Tempo | Wpis w changelogu co 1-2 dni; model 0-1 dnia po udostępnieniu API | [zweryfikowane: R01] |
| Promocja przy każdej premierze | Konfiguracja cennika zawiera 16 okien czasowych między 28.07 a 15.11.2026: 9 akcji w 16 dni sierpnia (głównie wokół Seedance), akcja `kling_4_release` 21-29.10 zbieżna z dodaniem Kling 4.0 (22.10 wg R01), wyprzedaż 11.11 do -60% | [zweryfikowane: MCP] |
| "Unlimited" z terminem | Okna 7, 14, 60 i 365 dni na nazwane modele, dopisek "Buy until: Nov 14", plany na 18 i 24 miesiące, przedsprzedaż okna unlimited (5-7.08 na okno od 7.08) | [zweryfikowane: MCP] |
| Pieniądze dla twórców | Program Earn: pula 100 tys. USD tygodniowo, do 2 500 USD za wideo; festiwal z pulą 1 mln USD | [zweryfikowane: R01; daty niepewne] |
| Konkurs wymusza dystrybucję | Zgłoszenie do konkursu aplikacji wymaga 1-10 linków do postów na YouTube, X, Instagramie lub TikToku | [zweryfikowane: MCP, opis narzędzia] |
| Publiczne strony projektów | Publikacja z przełącznikami: pokaż prompty, pokaż canvas, widoczność w odkrywaniu, link do posta social | [zweryfikowane: MCP, schemat narzędzia] |
| Dystrybucja w produkcie | Publikacja na TikToku z trendującą muzyką, Virality Predictor, konektory Instagram, Threads, X | [zweryfikowane: MCP, R01] |
| SEO i GEO | Blog z poradnikami cenowymi i migracyjnymi oraz osobna subdomena `geo.higgsfield.ai` pod wyszukiwarki AI | [zweryfikowane: adresy w R01]; cel subdomeny [wnioskowanie] |
| Kanał agentowy | MCP z 3-dniowym trialem Plus za 0 USD (wymaga karty, auto-odnowienie); narzędzie cennika zwraca gotowy tekst sprzedażowy, który asystent ma przekazać dosłownie | [zweryfikowane: MCP] |
| Monetyzacja po zakupie | Auto-refill promowany przed paczkami; doładowania ważne 90 dni | [zweryfikowane: MCP] |
| Social | Rozdawanie kredytów za repost i komentarz na X, sieć opłacanych twórców publikujących w dniu premiery | [niepewne: pamięć] |
| Program afiliacyjny | Warunków nie zweryfikowałem | [niepewne] |

### 2.2 Krytyka i kontrowersje, czyli szanse dla challengera

| Zarzut | Źródło | Odpowiedź nowego gracza |
|---|---|---|
| Domyślnie zaznaczony plan roczny, zwrot tylko przy pierwszym zakupie i bez zużytych kredytów | [zweryfikowane: R04, [help center](https://higgsfield.ai/creator-hub/help-center/refunds/why-didnt-i-receive-a-refund-after-canceling-my-subscription), [MindStudio](https://www.mindstudio.ai/blog/higgsfield-subscription-cancellation-complaints)] | Plan miesięczny domyślny, anulowanie jednym kliknięciem, zwrot proporcjonalny |
| "Unlimited" obejmuje nazwane modele i rozdzielczości, tylko w aplikacji web, w kolejce relaxed | [zweryfikowane: R04, MCP] | Bez "unlimited"; cena w PLN widoczna przed każdą generacją |
| Kredyty z planu przepadają co miesiąc, paczki po 90 dniach | [zweryfikowane: MCP] | Rollover do jednej puli, paczki ważne 12 miesięcy (R04) |
| Plan Free bez kredytów | [zweryfikowane: R01] | Mały, odporny na nadużycia darmowy limit obrazów |
| Licencja "perpetual, irrevocable" w regulaminie (07.2026) | [zweryfikowane: R01, [BottleRocket](https://www.bottlerocketcontent.com/higgsfield-tos-controversy-explained/)] | Licencja ograniczona do świadczenia usługi, brak treningu na danych klienta |
| Zawieszenie konta X (02.2026) | [zweryfikowane: R01, [AI Photo Labs](https://aiphotolabs.com/news/higgsfieldai-x-fiasco)] | Marketing bez spamu i bez cudzego IP |
| Plakietka "70% cheaper" przy doładowaniach, gdy konfiguracja pokazuje rabat 31-38% od ceny cennikowej | [zweryfikowane: MCP]; podstawa porównania nieznana [niepewne] | Każdy rabat liczony od najniższej ceny z 30 dni (R06) |
| Zarzuty o mylący marketing "unlimited", zapowiadanie modeli przed realną dostępnością, nieoznaczone płatne posty, treści promocyjne z cudzym wizerunkiem, blokady kont | [niepewne: pamięć]; nie używać w komunikacji bez własnej weryfikacji | Publiczny status modeli, oznaczanie współprac, jasna polityka treści |

Uwaga prawna: licznik "kup do" i "unlimited" z limitem fair use to w UE ryzyko nieuczciwej praktyki rynkowej, a każda obniżka wymaga podania najniższej ceny z 30 dni [R06, z pamięci tamtego raportu]. Tej części playbooka nie kopiować.

## 3. Segmenty i kliny dla gracza z Polski/CEE

Skala 1-5; w kolumnie "Konkurencja" 5 oznacza słabą konkurencję. Oceny to [wnioskowanie]; wielkości rynku nie zweryfikowałem liczbowo.

| Klin | Rynek | Gotowość do płacenia | Konkurencja | Solo founder | Suma | Komentarz |
|---|---|---|---|---|---|---|
| Reklamy i zdjęcia produktowe dla e-commerce MŚP (Allegro, Shoper, IdoSell, Base) | 4 | 4 | 3 | 4 | **15** | Mierzalny zwrot (koszt sesji zdjęciowej, CTR). Globalni gracze nie znają formatów Allegro ani polskiego lektora |
| Lokalizacja: polski UI i wsparcie, PLN, BLIK, faktura VAT | 3 | 3 | 4 | 5 | **15** | To warstwa, nie segment. Canva i CapCut też są po polsku, więc sama nie wystarczy |
| Agencje i freelancerzy social (workspace per klient, brand kit, wspólna pula) | 3 | 5 | 3 | 3 | **14** | Tu Higgsfield zarabia najwięcej (R01). Niższy churn, wyższy ARPU, potrzebna faktura i KSeF |
| Nieruchomości (virtual staging, wideo z ogłoszenia) | 3 | 4 | 3 | 3 | 13 | Płatność za ofertę; kanał przez portale ogłoszeniowe i biura |
| Moda (try-on, zdjęcia na modelu) | 3 | 4 | 2 | 3 | 12 | Wyspecjalizowani konkurenci globalni; wysoka poprzeczka jakości |
| Gastronomia | 3 | 2 | 4 | 3 | 12 | Niska gotowość do płacenia, wysoki churn |
| White-label dla agencji | 2 | 5 | 3 | 2 | 12 | Dobra faza 2 po klinie agencyjnym; ciężkie wsparcie |
| Zgodność z UE i rezydencja danych | 2 | 4 | 4 | 2 | 12 | Uczciwie da się obiecać tylko: pliki w UE, DPA, brak treningu, trasy oznaczone regionem. Inferencja i tak biegnie w USA lub Chinach (R03, R06) |
| Automotive (tła, wideo ofert) | 2 | 4 | 2 | 2 | 10 | Silni wyspecjalizowani dostawcy, sprzedaż do dealerów |
| Edukacja | 2 | 2 | 3 | 2 | 9 | Długie zakupy, a R06 zaleca usługę 18+ |
| Przejrzysty cennik | - | - | - | 5 | atrybut | Tani do wdrożenia wyróżnik zaufania we wszystkich klinach |

## 4. Akceleratory

Niczego z tej sekcji nie mogłem dziś otworzyć. Przed użyciem sprawdzić licencję, datę ostatniego commita i zależności.

| Zasób | Co daje | Licencja / warunki | Ocena |
|---|---|---|---|
| AI SDK 7 + Vercel AI Gateway | Jedno API do obrazu i wideo, ceny dostawcy bez marży | `generateImage` stabilne, wideo eksperymentalne [zweryfikowane: R05] | Podstawa stacku |
| `fal-ai-community/video-starter-kit` | Edytor wideo w przeglądarce: Next.js, Remotion, fal | MIT [niepewne: pamięć] | Wzorzec osi czasu i wywołań async |
| Tersa (`haydenbleasel/tersa`, możliwe przeniesienie do `vercel-labs`) | Otwarty canvas node dla workflow AI na Next.js, Supabase, AI SDK, Stripe i React Flow | MIT [niepewne: pamięć] | Najbliższy stackowi punkt startu dla canvasu w fazie 2 |
| `Anil-matcha/Open-Higgsfield-AI` | Otwarta "alternatywa" ze studiami obrazu, wideo i lipsync | Licencja nieznana; spięta z resellerem API [niepewne: pamięć] | Tylko inspiracja układu. Nie kopiować nazw ani promptów (R06), nie używać resellera (R03) |
| `nextjs/saas-starter`, `KolbySisk/next-supabase-stripe-starter`, `usebasejump/basejump` | Auth, subskrypcje Stripe, zespoły | MIT [niepewne: pamięć] | Szkielet kont i billingu. Żaden nie ma ledgera kredytów z rezerwacją (R04), to trzeba napisać |
| Płatne boilerplate'y (Makerkit, Supastarter, ShipFast) | Gotowy SaaS z rolami i panelem | Licencja komercyjna, ceny [niepewne] | Opcja, jeśli czas jest ważniejszy niż kilkaset USD |
| `useautumn/autumn`, `flexprice/flexprice`, Lago, OpenMeter | Otwarte silniki billingu z kredytami | Różne, część AGPL [niepewne: pamięć] | Wzorzec modelu danych; własny ledger w Postgres pozostaje rekomendacją R04 |
| React Flow (`xyflow/xyflow`) | Silnik edytora node | MIT [niepewne: pamięć] | Standard |
| tldraw | Nieskończony canvas | Własna licencja, klucz produkcyjny płatny [niepewne: pamięć] | Sprawdzić koszt przed wyborem; alternatywy: Konva, Fabric.js do masek inpaint |
| ComfyUI jako backend (RunPod `worker-comfyui`, Comfy Deploy, ViewComfy) | Własne pipeline'y na otwartych modelach | ComfyUI na GPL-3.0; licencje modeli osobno: FLUX.1 dev niekomercyjna, licencja społecznościowa Hunyuan wyłącza UE [niepewne: pamięć] | Faza 2-3, tylko dla presetów niedostępnych przez API |
| Remotion | Szablony reklam renderowane kodem | Darmowe do 3 pracowników [zweryfikowane: R05] | Dobre do napisów, cen i logo na wideo |
| Programy white-label i resellerskie | - | API Higgsfield: redystrybucja to naruszenie; Replicate ma klauzulę przeciw odsprzedaży usługi; ElevenLabs zakazuje odsprzedaży samej usługi [zweryfikowane: R03] | Nie kupować "gotowca"; white-label to własna funkcja multi-tenant w fazie 2 |

## 5. Składniki go-to-market

### 5.1 Kanały

| Kanał | Jak | Uwagi |
|---|---|---|
| SEO programatyczne | Strona na model ("Kling 4.0 po polsku", cena w PLN, przykłady), na preset, na zastosowanie ("zdjęcia produktowe AI", "reklama wideo na Allegro"), na format (wymiary i limity platform) | Generować z tych samych tabel co katalog. Unikalna treść: własne przykłady i ceny |
| Strony porównawcze | "[Marka] a X" z tabelą cech i cen, data aktualizacji | Dozwolone jako obiektywne porównanie; słowa "klon" i "kopia" są wykluczone (R06) |
| GEO | Zwięzłe strony FAQ i cenniki w formacie czytelnym dla wyszukiwarek AI | Higgsfield ma na to subdomenę (R01) |
| Krótkie wideo | 1-3 klipy dziennie zrobione produktem: przed i po, "reklama w 60 sekund", polski lektor | TikTok, Reels, Shorts; X po angielsku pod premiery modeli |
| Pętla szablonów | Publiczna strona wyniku z przyciskiem "Odtwórz": rejestracja i formularz presetu wypełniony z góry; znak wodny na planie Free | Wymaga etykiety AI i pre-moderacji przed publikacją (R06) |
| Polecenia i afiliacja | Polecenie w kredytach po pierwszej płatności poleconego; afiliacja dla twórców i szkoleniowców | Stawki w sekcji 5.2 |
| Społeczność | Grupy Facebook o e-commerce i AI, LinkedIn, Discord dla twórców, comiesięczny konkurs z nagrodą w kredytach i wymogiem posta | Wzorzec konkursu jak u Higgsfield (MCP), w małej skali |
| Partnerzy e-commerce | Aplikacja lub integracja w sklepach aplikacji platform sklepowych, agencje Allegro Ads, kursy e-commerce | Najtańsze źródło klientów z intencją zakupu [wnioskowanie] |
| Launch | Product Hunt, katalogi narzędzi AI, BetaList; w Polsce Wykop, MamStartup, Antyweb, Spider's Web, Nowy Marketing, konferencje e-commerce | Bez ofert lifetime: koszt generacji jest zmienny (R04) |

### 5.2 Benchmarki i ekonomia akwizycji

- Typowe zakresy z raportów branżowych: freemium samoobsługowe 2-5% konwersji z rejestracji do płatności; trial bez karty 8-15%; trial z kartą 40-60% [niepewne: pamięć, bez źródła w tej sesji].
- Aplikacje AI monetyzują się szybciej, ale tracą subskrybentów wyraźnie szybciej niż inne (raport RevenueCat 2026) [niepewne: pamięć]. Do planu przyjąć churn miesięczny 12-20% dla B2C i 4-7% dla agencji [wnioskowanie].
- Publicznego benchmarku CAC dla tej kategorii nie mam [niepewne]. Wyliczenie z R04: wkład 8,9 USD miesięcznie i churn 15% dają ok. 59 USD wkładu w cyklu życia, czyli **CAC do ok. 20 USD** (przy 10% churnu do 30 USD). Przy konwersji 3% to **0,45-0,90 USD za rejestrację** [wnioskowanie].
- Plan Pro dla agencji: wkład 27,4 USD (R04) i churn 5% dają ok. 550 USD, więc CAC do ok. 180 USD. To uzasadnia sprzedaż bezpośrednią i prowizje partnerskie [wnioskowanie].
- Afiliacja: rynkowe 20-35% przychodu przez 3-12 miesięcy [niepewne: pamięć] nie mieści się w marży, bo wkład to ok. 36% ARPU (R04). Warianty mieszczące się w CAC 20 USD: 10% przez 12 miesięcy, 30% przez pierwsze 3 miesiące albo stała premia 10-15 USD za płacącego. Polecenie w kredytach kosztuje ok. 3,3 USD COGS za 500 kredytów [wnioskowanie].

## 6. Rekomendacja

### 6.1 Pozycjonowanie

> **Dla polskich sklepów internetowych, marketerów i agencji, którzy potrzebują zdjęć produktowych i reklam wideo bez ekipy zdjęciowej, [Marka] jest studiem AI po polsku, które z linku do produktu robi gotowe kreacje na Allegro, Metę i TikToka na najlepszych dostępnych modelach. W odróżnieniu od globalnych agregatorów podaje cenę w złotówkach przed każdą generacją, przyjmuje BLIK, wystawia fakturę VAT, nie kasuje kredytów co miesiąc i zwraca je za nieudane generacje.**

Zasady: nie konkurować ceną flagowych modeli (R04); nie obiecywać "unlimited"; o danych mówić precyzyjnie (pliki w UE, lista podprocesorów), bez hasła "100% w UE"; nie używać marki Higgsfield poza obiektywnymi porównaniami.

### 6.2 Trzy kliny w kolejności

1. **E-commerce MŚP w Polsce, potem CZ, SK, RO, HU.** Pierwsze studio: link lub zdjęcie produktu, packshoty, zdjęcia lifestyle, klip 9:16 z polskim lektorem, eksport w formatach platform. Uzasadnienie: najwyższa suma ocen, mierzalny zwrot, tania dystrybucja przez partnerów.
2. **Agencje i freelancerzy social media.** Workspace per klient, brand kit, wspólna pula kredytów, role, faktury. Uzasadnienie: najwyższy ARPU i najniższy churn; naturalne rozszerzenie klinu 1.
3. **Polski twórca (warstwa horyzontalna).** Katalog modeli, presety i efekty po polsku jako górna część lejka i paliwo dla SEO oraz wideo. Uzasadnienie: zasięg; najsłabsza marża, więc nie jako główne źródło przychodu. Rezerwa: nieruchomości.

### 6.3 Plan 90 dni (od gotowej zamkniętej bety)

| Dni | Cel | Działania | Miernik [wnioskowanie] |
|---|---|---|---|
| 1-30 | Dowód wartości | 20-30 partnerów projektowych (sklepy, 5 agencji) z ręcznym onboardingiem; lista oczekujących; 10 presetów produktowych; nazwa i domena po badaniu znaku; pierwsze 50 stron SEO; profil na TikToku i LinkedIn z codziennym klipem | 30 aktywnych testerów, 10 deklaracji płatności, 500 osób na liście |
| 31-60 | Publiczna beta w Polsce | Płatności (PLN, BLIK, faktura); strony wyników z "Odtwórz"; 300 stron programatycznych; program poleceń w kredytach; 3 studia przypadków z liczbami; publikacje w mediach branżowych; rozmowy z 2-3 platformami sklepowymi | 1 500 rejestracji, 40-60 płacących, konwersja 3%+ |
| 61-90 | Skala kanałów, które działają | Product Hunt i katalogi AI; afiliacja dla 20 twórców i szkoleniowców; plan Team dla agencji i 30 rozmów sprzedażowych; pierwszy konkurs; strony porównawcze; decyzja o CZ/SK | 3 000-5 000 rejestracji, 100-150 płacących (próg rentowności R04: ok. 113 przy 1 000 USD kosztów stałych), churn miesięczny poniżej 15%, CAC poniżej 20 USD |

## 7. Pytania otwarte

- Aktualne cenniki i funkcje graczy oznaczonych "pamięć" oraz warunki programu afiliacyjnego Higgsfield.
- Bieżąca ocena Higgsfield w serwisach opinii i najczęstsze skargi z ostatnich 90 dni.
- Czy istnieją polskie lub czeskie agregatory generacji AI i jak obsadzone są polskie frazy.
- Licencje i aktywność repozytoriów z sekcji 4.
- Warunki sklepów aplikacji polskich platform e-commerce (prowizje, wymagania techniczne).

## Źródła

**Odczyt własny (2026-11-13):** konektor MCP Higgsfield, narzędzie cennika (plany, doładowania, auto-refill, kalendarz promocji) oraz opisy i schematy narzędzi: presety, konkurs, publikacja projektu, TikTok, Virality Predictor.

**Źródła zweryfikowane na żywo w raportach równoległych (przywołane tutaj):**
- R01: [TechCrunch 17.08.2026](https://techcrunch.com/2026/08/17/higgsfield-raises-400m-series-b-quadrupling-its-valuation-in-8-months-to-5-4b/), [TechCrunch 15.01.2026](https://techcrunch.com/2026/01/15/ai-video-startup-higgsfield-founded-by-ex-snap-exec-lands-1-3b-valuation), [SaaStr](https://www.saastr.com/higgsfield-went-from-1b-to-1-35b-in-run-rate-in-one-month-now-its-aiming-for-2b-by-year-end/), [Sacra](https://sacra.com/c/higgsfield/), [changelog HF](https://higgsfield.ai/creator-hub/changelog), [Earn](https://higgsfield.ai/earn), [festiwal](https://higgsfield.ai/contests/higgsfield-global-film-festival), [migracja z Sora](https://higgsfield.ai/blog/sora-api-migration-guide), [przewodnik cenowy GEO](https://geo.higgsfield.ai/higgsfield-ai-pricing-guide), [AI Photo Labs](https://aiphotolabs.com/news/higgsfieldai-x-fiasco), [BottleRocket](https://www.bottlerocketcontent.com/higgsfield-tos-controversy-explained/)
- R03: [regulamin Higgsfield](https://higgsfield.ai/terms-of-use-agreement), [API Higgsfield](https://higgsfield.ai/blog/higgsfield-api)
- R04: [help center, zwroty](https://higgsfield.ai/creator-hub/help-center/refunds/why-didnt-i-receive-a-refund-after-canceling-my-subscription), [MindStudio](https://www.mindstudio.ai/blog/higgsfield-subscription-cancellation-complaints), [HeyGen o cenach HF](https://www.heygen.com/blog/higgsfield-pricing), [Krea o cenach HF](https://www.krea.ai/blog/higgsfield-pricing-explained-2026-unlimited-credits-and-real-monthly-costs), [Freepik](https://www.renderahouse.com/blog/freepik-pricing), [Krea](https://www.renderahouse.com/blog/krea-ai-pricing), [OpenArt](https://voyager.so/blog/openart-pricing), [Leonardo](https://www.renderahouse.com/blog/leonardo-ai-pricing), [Runway](https://www.pixara.ai/blogs/runway-pricing), [Kling](https://kling.ai/app/membership/membership-plan?r=26), [porównanie cen wideo](https://aitoolsbakery.com/blog/ai-video-generator-pricing-compared/)
- R05: [licencja Remotion](https://www.remotion.dev/docs/license)

**Adresy do weryfikacji (niepobrane w tej sesji):** `github.com/fal-ai-community/video-starter-kit`, `github.com/haydenbleasel/tersa`, `github.com/Anil-matcha/Open-Higgsfield-AI`, `github.com/nextjs/saas-starter`, `github.com/KolbySisk/next-supabase-stripe-starter`, `github.com/usebasejump/basejump`, `github.com/useautumn/autumn`, `github.com/flexprice/flexprice`, `github.com/xyflow/xyflow`, `github.com/tldraw/tldraw`, `github.com/comfyanonymous/ComfyUI`, `github.com/runpod-workers/worker-comfyui`; oficjalne cenniki: Flora, Figma Weave, Comfy Cloud, Artlist, Invideo, LTX Studio, Google AI, Midjourney, Creatify, Arcads, HeyGen, Synthesia, Captions; raport RevenueCat "State of Subscription Apps 2026"; opinie o Higgsfield w Trustpilot.
