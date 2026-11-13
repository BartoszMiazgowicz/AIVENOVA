# 08 - UX i architektura informacji (teardown agregatorów generacji AI)

Stan na 2026-11-13. Referencja główna: Higgsfield; porównanie: Krea, Freepik, OpenArt, Runway.

> **Metoda i ograniczenia (ważne).** Wspólny limit WebSearch tej sesji był już wyczerpany, a WebFetch do `higgsfield.ai` i `trustpilot.com` zablokowała polityka sieci. Nie wykonałem więc żadnego własnego wyszukiwania. Raport opiera się na trzech warstwach:
> 1. **MCP** - odczyt read-only konektora Higgsfield (definicje modeli, schematy narzędzi, wytyczne UX i design systemu dla aplikacji osadzanych w ich platformie). Zero generacji, zero zmian stanu.
> 2. **R01-R06** - raporty sąsiednie w tym katalogu wraz z ich źródłami WWW (linki przytaczam, ale sam ich nie otwierałem).
> 3. **Pamięć modelu** (stan wiedzy do ok. połowy 2026) - zawsze oznaczona [niepewne].
>
> Tagi: **[zweryfikowane]** = MCP z tej sesji albo źródło z raportu sąsiedniego; **[wnioskowanie]** = moja dedukcja; **[niepewne]** = pamięć modelu lub źródła sprzeczne. Cała sekcja o Krea/Freepik/OpenArt/Runway oraz opis górnej nawigacji WWW Higgsfield są [niepewne] i wymagają 1-2 h ręcznego przejścia z zrzutami ekranu (lista w sekcji 8). Nazwy własne Higgsfield służą wyłącznie jako odniesienie badawcze.

## TL;DR

- Higgsfield ma **trzy powtarzalne układy ekranu**: `studio` (sidebar projektów + dok promptu + feed), `preset` (szyna tworzenia + siatka presetów + zakładka Historia) i `app-detail` (landing jednego narzędzia). Wystarczą one na ok. 90% ekranów klona funkcjonalnego [zweryfikowane: MCP-A].
- **Composer jest generowany z definicji modelu**: role mediów (start/end frame, referencje obrazu, wideo, audio), tryb, proporcje, czas, rozdzielczość, audio, liczba wariantów. Koszt w kredytach stoi **wewnątrz przycisku Generuj** [zweryfikowane: MCP-B, MCP-E].
- Po przyjęciu zadania karta "pending" pojawia się w feedzie natychmiast, błąd zostaje jako karta z "ponów", a podgląd wyniku otwiera się w miejscu z nawigacją strzałkami i zachowaniem scrolla [zweryfikowane: MCP-A, MCP-C].
- Siatki wyników: `auto-fit`, prawdziwe proporcje każdej karty, bez przycinania; wideo odtwarzane z pliku źródłowego z miniaturą jako posterem [zweryfikowane: MCP-B, MCP-C].
- Tożsamość wizualna referencji jest bardzo charakterystyczna: wyłącznie ciemny motyw, limonkowe CTA z fazą 3D, Space Grotesk + Inter, ikony lucide, ikona "iskierek" przy kredytach [zweryfikowane: MCP-B]. To gotowa lista rzeczy, których **nie** powielać.
- Udokumentowane skargi dotyczą rozliczeń, nie generacji: domyślnie zaznaczony plan roczny, wąskie okno zwrotu, "unlimited" z terminami zakupu i kolejką 1 zadania [zweryfikowane: R04]. W UE to także ryzyko prawne [zweryfikowane: R06].
- Rekomendacja: MVP = 5 powierzchni (Obraz, Wideo, Presety, Biblioteka, Rozliczenia) na jednym komponencie composera; marketing/ads, postacie i audio w v1; reżyserka, storyboard, canvas i asystent w v2.

## 1. Teardown referencji

### 1.1 Powłoka i nawigacja

| Element | Ustalenie | Status |
|---|---|---|
| Chrome globalny | Nagłówek hosta trzyma saldo kredytów i konto; narzędzia nie mają własnego nagłówka, nawigacja lokalna to `Sidebar` lub zakładki | [zweryfikowane: MCP-B, MCP-D] |
| Ekran pierwszy | "Powierzchnia produktu jest ekranem nr 1": prompt box na środku, ustawienia w prompt boxie, po pierwszej generacji widok wyników z galerią | [zweryfikowane: MCP-B] |
| Układy | `studio`, `preset`, `app-detail`; kontener `max-w-7xl`, wyjątek: pełnoekranowy workspace studia filmowego | [zweryfikowane: MCP-A, MCP-D] |
| Breakpointy | 768 / 1280 / 1920 px; poniżej desktopu sidebar chowa się w zakładki lub bottom sheet; test na 375 px; cele dotyku min. 44x44 px | [zweryfikowane: MCP-B] |
| Górne menu WWW | Explore, Image, Video, Edit, Character, Cinema Studio, Apps, Assets, Community + pasek promocji; mega-menu z listą modeli | [niepewne: pamięć modelu] |
| Mobile | Brak aplikacji natywnej; redesign mobilnego WWW 24.09.2026 | [zweryfikowane: R01, [help center](https://higgsfield.ai/creator-hub/help-center/getting-started/official-higgsfield-platforms)] |
| Paleta poleceń | Design system zawiera komponent `Command` (cmdk); użycie w głównym produkcie | [zweryfikowane: istnienie; niepewne: użycie] |

### 1.2 Composer obrazu i wideo

| Kontrolka | Jak działa w referencji | Status |
|---|---|---|
| Wybór modelu | Lista z tagami zdolności w definicji modelu (`text-rendering`, `4k`, `keyframes`, `video-edit`, `unlim`); router "Auto" i narzędzie rekomendacji | [zweryfikowane: MCP-E, R02] |
| Tryb | Przełącznik `t2v / omni_reference / video_edit / video_extension` (Seedance 2.5, studio filmowe) albo `text / image / reference / video-edit` (Kling 4.0); zmiana trybu zmienia widoczne sloty | [zweryfikowane: MCP-E] |
| Sloty referencji | Role: `start_image`, `end_image`, `image_references`, `video_references`, `audio_references`. Limity różne per model: 30 obrazów + 10 wideo + 10 audio (Seedance 2.5), 14 obrazów (Nano Banana Pro), 10 obrazów i 5 wideo (Kling 4.0) | [zweryfikowane: MCP-E, R02] |
| Keyframes | Kling 4.0: uporządkowane klatki pośrednie między start a end | [zweryfikowane: MCP-E] |
| Elementy | Wielokrotnego użytku: `character / environment / prop`, klasyfikacja `auto`, nazwa do 32 znaków; w prompcie jako wzmianka `@nazwa`; statusy `processing / ip_checking / failed / nsfw / completed`; działają tylko w wybranych modelach | [zweryfikowane: MCP-F] |
| Proporcje | `auto, 21:9, 16:9, 4:3, 1:1, 3:4, 9:16`; obraz dodatkowo 3:2, 2:3, 4:5, 5:4 | [zweryfikowane: MCP-E, R02] |
| Czas / rozdzielczość | Suwak 4-30 s (Seedance 2.5), 3-30 s (Kling 4.0); 480p-4k; obraz 1k/2k/4k | [zweryfikowane: MCP-E, R02] |
| Audio | Przełącznik `generate_audio`, domyślnie włączony | [zweryfikowane: MCP-E] |
| Warianty | 1-4 na zgłoszenie; tryb unlimited wymusza 1 | [zweryfikowane: MCP-F] |
| Seed | Tylko 11 ze 140 definicji modeli ma `seed` | [zweryfikowane: R02] |
| Negative prompt | Nie ma go wśród 8 najczęstszych parametrów katalogu; traktować jako opcję zaawansowaną per model | [wnioskowanie z R02] |
| Szkic | Seedance 2.5: tani draft 480p, finalizacja do 7 dni | [zweryfikowane: R02] |
| Koszt | W przycisku: `{etykieta} {ikona} {kredyty}`; osobne zapytanie o koszt przed wysyłką. Aplikacje zewnętrzne muszą dodatkowo pokazać modal potwierdzenia (model + ustawienia + koszt) | [zweryfikowane: MCP-B, MCP-C, MCP-D] |
| Źródło płatności | Użytkownik wybiera: kredyty czy pula unlimited; odrzucony wybór nie jest po cichu zamieniany na obciążenie | [zweryfikowane: MCP-F] |
| Ulepszanie promptu | Studio filmowe ma "automatic prompt direction"; ogólny przełącznik "enhance" | [zweryfikowane: MCP-E; niepewne: przełącznik] |
| Folder docelowy | `folder_id` per generacja + preferencja "twórz projekt automatycznie" | [zweryfikowane: MCP-F] |

### 1.3 Kolejka, historia, podgląd wyniku

- **Statusy zadań:** `pending → in_progress → completed | failed | nsfw | ip_detected | canceled`; automatyczny zwrot kredytów po błędzie w 5 s-4 min [zweryfikowane: R02].
- **Natychmiastowa widoczność:** przyjęte zadanie trafia do feedu jako karta oczekująca i jest odpytywane w miejscu. Błąd walidacji zostaje na formularzu; błąd po wysyłce zostaje w wynikach jako karta z "ponów". Stan composera i wybrany preset są zachowane [zweryfikowane: MCP-A].
- **Karta:** prompt, model, status, czas, powód błędu; obraz = zoptymalizowany podgląd + oryginał do pobrania; wideo = plik źródłowy + miniatura jako poster; "ukończone bez URL" ma jawny stan "podgląd niedostępny" [zweryfikowane: MCP-C].
- **Podgląd w miejscu:** Poprzedni/Następny + strzałki po aktualnie przefiltrowanej liście; zamknięcie przywraca zakładkę, filtry i pozycję scrolla; zmiana elementu nie przeładowuje feedu [zweryfikowane: MCP-A, MCP-C].
- **Filtry:** typ (image/video/audio/3d), tylko ukończone; w projekcie: model, polubione, rodzaj wyjścia, źródło (generacja albo upload), status, sortowanie po dacie utworzenia, dodania lub polubienia [zweryfikowane: MCP-F].
- **Akcje na wyniku** (osobne operacje backendu): upscale, outpaint, reframe, usuwanie tła, relight, inpaint, animuj obraz (wynik jako wejście kolejnego zadania), przedłuż wideo w przód lub w tył, edycja wideo, analiza wiralowości, publikacja na TikTok z deklaracją treści AI [zweryfikowane: MCP-E, MCP-F, R01].
- **Równoległość:** 2 wideo + 4 obrazy (Starter) do 8 + 8 (Ultra); kolejka unlimited: 1 zadanie na typ [zweryfikowane: R01, R02, R04].

### 1.4 Biblioteka, udostępnianie, społeczność

- Hierarchia: workspace → projekt → foldery → assety; archiwizacja; wyszukiwanie folderów [zweryfikowane: MCP-F, R02].
- Udostępnianie projektu e-mailem z rolami `view / collaborate / admin`, do 10 adresów na zaproszenie [zweryfikowane: MCP-F].
- Publikacja ma **trzy jawne przełączniki**: pokaż prompty, pokaż canvas, wykrywalność w feedzie (wyłączona nadal zostawia publiczny link). Do tego okładka, tagi, typ (film/seria/karuzela) i moderacja ze stanem "wymaga decyzji autora" [zweryfikowane: MCP-F].
- Feed społeczności, konkursy, marketplace aplikacji [zweryfikowane: R01]. Profile, obserwowanie, komentarze: [niepewne].
- Powiadomienia: brak dowodów poza toastami (3-5 s, bez kradzieży fokusu) [zweryfikowane: MCP-B; reszta niepewne].

### 1.5 Postać i tożsamość

| Ścieżka | Przebieg | Status |
|---|---|---|
| Trenowana tożsamość | Nazwa + zdjęcia jednej osoby, trening w tle z odpytywaniem; jedna tożsamość na generację; tylko modele własne. Liczby sprzeczne: 5-20 zdjęć i ok. 10 min (MCP), 20-80 zdjęć, 3-5 min, 25 kredytów ([help](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-create-and-use-a-soul-id-character)), 1-100 (SDK) | [zweryfikowane istnienie; niepewne liczby] |
| Element (natychmiast) | 1 obraz, wiele podmiotów w kadrze, wiele modeli obrazu i wideo | [zweryfikowane: MCP-F] |
| Kreator postaci z menu | 18 grup cech; krok "prepare" zwraca projekt i cenę przed generacją; wynik to arkusz postaci, potem propozycja animacji | [zweryfikowane: R02, instrukcje MCP] |
| Głos | Okno z zakładkami Nagraj / Wgraj + nazwa; przy braku kredytów paywall pojawia się wewnątrz okna | [zweryfikowane: MCP-F] |

Wzorzec wart skopiowania: jawny rozjazd "trenuj (wierniej, wolniej, 1 osoba)" kontra "zapisz jako element (od razu)" [wnioskowanie].

### 1.6 Kontrolki filmowe i mapowanie na prompt

Studio filmowe 4.0 to model bazowy plus identyfikatory słownikowe: epoka, korpus kamery, obiektyw, przysłona, tempo montażu, gatunek, światło, paleta barw. Światło ma trzy źródła: preset, zapisany preset użytkownika albo **własny rig**: lista lamp (pierwsza = kluczowa), każda z kierunkiem (26 pozycji wokół sceny), kolorem, jasnością i rozproszeniem [zweryfikowane: MCP-E]. Wniosek: panel reżysera to formularz wybierający wpisy słownika, a serwer składa z nich prompt [wnioskowanie]. Sceny multi-shot do 30 s i do 50 referencji [niepewne: R01, [blog](https://higgsfield.ai/blog/cinema-studio-4-0)]. Storyboard do 8 spójnych klatek jako wejście do studia [zweryfikowane: R01, [help](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-use-popcorn)]. Konkretne nazwy korpusów i obiektywów (marki realnych producentów) oraz galeria kilkudziesięciu ruchów kamery: [niepewne: pamięć modelu].

Proponowany model danych: tabela `director_options {group, label_pl, label_en, prompt_fragment_en, thumbnail, compatible_models[], conflicts[]}`. Kolejność składania: typ ujęcia i ruch → prompt użytkownika → obiektyw, ogniskowa, przysłona (głębia ostrości) → światło → epoka, gatunek, paleta. Zawsze pokazywać edytowalny "prompt końcowy". Gdy model ma natywny parametr kamery, mapować na parametr, nie na tekst [wnioskowanie].

### 1.7 Presety i aplikacje jednego kliknięcia

Rekord listy: `id, name, description, kind, thumbnail_url, preview_url, preview_type (image|video)`, kategorie, paginacja kursorem. Szczegół zwraca schemat wejść (sloty mediów, pola tekstowe, wybory rozdzielczości i proporcji), gotowość (`readiness`) i koszt; przycisk "Recreate" uruchamia generację [zweryfikowane: R02, MCP-F]. Samo przeglądanie i wypełnianie niczego nie uruchamia. Po wysyłce układ `preset` przełącza się na Historię [zweryfikowane: MCP-A].

### 1.8 Marketing i reklamy

- **Formaty wideo:** UGC, link do produktu (scraping strony), reklama referencyjna (analiza cudzej reklamy → koncept), wideo aplikacji (zrzuty ekranu + urządzenie), motion dla SaaS (URL marki + do 9 obrazów), 2D motion, hypermotion, mixed media. Do 6 zdjęć produktu, 1 awatar, 1-4 warianty [zweryfikowane: MCP-E].
- **Awatary:** rekord `{id, name, preview_url, type: preset|user, gender}`, wyszukiwarka, osobne kursory dla gotowych i własnych [zweryfikowane: MCP-G].
- **Statyczne kreacje:** marka z URL (kilka minut: produkty, paleta, logo, ton, odbiorcy) → wycena → jawna akceptacja kosztu → generacja z kluczem idempotencji. Alokacja per produkt (do 10 kreacji, do 24 produktów), format 1:1 / 9:16 / 16:9 / 3:4, cel kampanii; wynik = koncepty z nagłówkiem, tekstem, CTA i URL [zweryfikowane: MCP-F, R02].

### 1.9 Canvas i agent

Canvas węzłowy oraz agent czatowy istnieją [zweryfikowane: R01, [canvas](https://higgsfield.ai/canvas-intro)]. Konwencje agenta widoczne w instrukcjach: najpierw krótki plan, jedno pytanie na starcie, raport postępu po każdym kroku, wycena i jawna zgoda przed każdym wydatkiem, brak automatycznego ponawiania po timeoucie [zweryfikowane: MCP-D, MCP-F].

### 1.10 Onboarding, paywall, upsell

| Wzorzec | Dowód | Ocena |
|---|---|---|
| Free = 0 kredytów, znak wodny, bez wideo | [niepewne: R04, [Krea](https://www.krea.ai/blog/what-is-higgsfield-ai-pricing-free-plan-and-alternatives-in-2026)] | Twardy paywall przed pierwszą wartością |
| Modele zablokowane na niższym planie | [zweryfikowane: R01] | Uczciwe, jeśli kłódka i cena są widoczne przed kliknięciem |
| Równoległość jako poziom planu | [zweryfikowane: R01, R02] | Do przejęcia |
| "Unlimited" jako okna 7/365 dni z terminem zakupu ("Buy until"), tylko w WWW, kolejka 1 zadania | [zweryfikowane: R04, [aliteq](https://aliteq.com/higgsfield-unlimited-explained), [blog](https://higgsfield.ai/blog/credits-vs-unlimited-ai-video-generation)] | Mylące; unikać |
| Stałe promocje do -60%, ceny przekreślone, okresy 18 i 24 mies. | [zweryfikowane: R02, R04] | W PL wymaga najniższej ceny z 30 dni [R06] |
| Plan roczny zaznaczony domyślnie; zwrot tylko przy pierwszym zakupie, krótkie okno, bez zużytych kredytów | [zweryfikowane: R04, [help](https://higgsfield.ai/creator-hub/help-center/refunds/why-didnt-i-receive-a-refund-after-canceling-my-subscription), [mindstudio](https://www.mindstudio.ai/blog/higgsfield-subscription-cancellation-complaints)] | Główne źródło skarg; nie kopiować |
| Paywall wewnątrz narzędzia przy braku kredytów | [zweryfikowane: MCP-F] | Do przejęcia, bez utraty wpisanych danych |
| Trial z auto-odnowieniem; anulowanie kartą z dwoma przyciskami, dostęp zostaje do końca triala | [zweryfikowane: MCP-F] | Do przejęcia |
| Licencja "perpetual, irrevocable" na treści użytkowników | [zweryfikowane: R01, [BottleRocket](https://www.bottlerocketcontent.com/higgsfield-tos-controversy-explained/)] | Ryzyko reputacyjne; własny regulamin węższy |
| Obciążenia za nieudane generacje, liczniki odliczające, utrudnione anulowanie | [niepewne: pamięć modelu, opinie z forów] | Do weryfikacji na Trustpilot/Reddit |

### 1.11 Ustawienia, rozliczenia, zespół

Typy workspace: `individual / team_owner / team_member`; portfel; plany; doładowania jednorazowe; auto-refill z progiem 300 kredytów; lista transakcji `{nazwa, kredyty, spend|refund, data}` bez identyfikatora zadania [zweryfikowane: R02]. Zespoły: miejsca, wspólna pula, SSO od wyższych planów [zweryfikowane: R01].

## 2. Porównanie z Krea, Freepik, OpenArt, Runway

Cała tabela to **[niepewne: pamięć modelu, stan sprzed ok. połowy 2026]**. Służy do wyboru wzorców, nie jako opis stanu obecnego.

| Produkt | Układ composera | Wyróżnik UX | Co rozważyć |
|---|---|---|---|
| Krea | Dok na dole, płótno i feed nad nim; osobne narzędzia Realtime, Enhancer, Edit, Train, Nodes | Generacja na żywo podczas rysowania; lekki, szybki interfejs | Podgląd na żywo dla tanich modeli; dok jako układ domyślny |
| Freepik | Lewa kolumna ustawień, wyniki po prawej; lewy sidebar narzędzi; "Spaces" (canvas węzłowy) | Integracja ze stockiem i edytorem; unlimited w wyższych planach | Układ "szyna" dla narzędzi z wieloma parametrami |
| OpenArt | Formularz po lewej; produkt zorganizowany wokół postaci i historii | Postać z 1 obrazu, wielu zdjęć lub opisu; "story" jednym kliknięciem | Kreator postaci z trzema wejściami |
| Runway | Sesje i projekty; tryb czatu; koszt na przycisku | Workspace per projekt, biblioteka assetów, tryb Explore w planie Unlimited | Sesja jako jednostka pracy; tryb relaxed nazwany wprost |

Wniosek [wnioskowanie]: rynek ustabilizował się na dwóch układach, **dok** (prompt na dole, feed nad nim) i **szyna** (ustawienia z boku, wyniki obok). Higgsfield używa obu. Jeden komponent composera z dwoma wariantami układu pokryje wszystkie powierzchnie.

## 3. (a) Sitemapa i inwentarz ekranów

Założenia: Next.js App Router, segment `[locale]` (pl, en) [R05]; strefa publiczna indeksowalna, `/app/*` za logowaniem. Podgląd wyniku jako trasa przechwytywana (modal nad feedem z własnym URL).

### Publiczne

| Trasa | Cel | Kluczowe komponenty | Faza |
|---|---|---|---|
| `/` | Landing: wartość, przykłady, CTA | Hero z działającym mini-composerem, siatka przykładów, cennik w skrócie | MVP |
| `/pricing` | Plany, koszt per generacja | PlanCard, kalkulator "ile to generacji", FAQ, najniższa cena z 30 dni | MVP |
| `/login`, `/signup`, `/auth/callback`, `/auth/reset` | Uwierzytelnianie | Magic link, OAuth, zgody, bramka 18+ | MVP |
| `/legal/{terms,privacy,content-policy,withdrawal,report}` | Regulamin, odstąpienie online, zgłoszenie treści | Formularze, wersjonowanie dokumentów | MVP |
| `/s/[token]` | Niepubliczny link do pracy | MediaViewer tylko do odczytu, etykieta AI, "Zgłoś" | MVP |
| `/explore` | Galeria publiczna | MediaGrid, filtry, etykieta AI | v1 |
| `/p/[id]` | Permalink pracy | Viewer, prompt (jeśli autor pozwolił), "Użyj ustawień" | v1 |
| `/u/[handle]` | Profil twórcy | Nagłówek profilu, siatka prac | v1 |
| `/tools/[slug]` | Landing jednego presetu lub narzędzia (SEO) | Układ `app-detail`: generator + "jak to działa" | v1 |
| `/models`, `/models/[slug]` | Katalog modeli: zdolności, ceny, przykłady | ModelCard, tabela zdolności | v1 |
| `/help`, `/changelog` | Pomoc, lista zmian | MDX | v1 |

### Aplikacja

| Trasa | Cel | Kluczowe komponenty | Faza |
|---|---|---|---|
| `/app` | Start: wróć do pracy, nowości, polecane presety | Ostatnie generacje, skróty, ChangelogCard | MVP |
| `/app/image` | Studio obrazu | Composer (dok), ModelPicker, ReferenceSlots, feed, QueueDrawer | MVP |
| `/app/video` | Studio wideo | Composer + Start/EndFrame, DurationSlider, AudioToggle | MVP |
| `/app/g/[id]` | Podgląd wyniku | MediaViewer, ActionBar, MetadataPanel, Prev/Next | MVP |
| `/app/presets`, `/app/presets/[slug]` | Galeria i szczegół presetu | PresetCard, CreationRail, zakładka Historia | MVP (10-20 presetów) |
| `/app/edit/[tool]` | Upscale, usuwanie tła; potem inpaint, outpaint, reframe, relight | UploadField, BeforeAfter, MaskCanvas | MVP (2 narzędzia), v1 reszta |
| `/app/library`, `/app/library/folders/[id]` | Wszystkie assety i uploady | MediaGrid wirtualizowany, FolderTree, wyszukiwarka, akcje zbiorcze | MVP |
| `/app/upgrade` | Plany i doładowania w aplikacji | PlanCard, TopUpPicker, podsumowanie przed zapłatą | MVP |
| `/app/projects`, `/app/projects/[id]` | Projekty z udostępnianiem | ShareDialog (role), aktywność | v1 |
| `/app/characters`, `/new`, `/[id]` | Postacie i elementy | Kreator 4 kroków: zgoda → zdjęcia → kontrola jakości → trening | v1 (MVP: zapisane referencje) |
| `/app/audio`, `/app/voices` | TTS, muzyka, klon głosu | ScriptEditor, VoicePicker, rejestrator ze zgodą | v1 |
| `/app/lipsync` | Mówiące wideo | Sloty portret + audio, podgląd synchronizacji | v1 |
| `/app/ads`, `/brands/[id]`, `/products/[id]`, `/new`, `/runs/[id]` | Reklamy: import URL, brand kit, kreator, wyniki | UrlImport, BrandKitEditor, FormatPicker, AvatarPicker, ScriptEditor, CostReview | v1 (lite), v2 (pełne) |
| `/app/notifications` | Centrum powiadomień | Lista, preferencje kanałów | v1 |
| `/app/director` | Studio filmowe | DirectorPanel, LightRig, ShotList, podgląd promptu końcowego | v2 |
| `/app/storyboard/[id]` | Sekwencja klatek i oś czasu | FrameStrip, Timeline, eksport | v2 |
| `/app/assistant` | Agent czatowy | Chat, PlanCard, CostApproval, osadzone karty zadań | v2 |
| `/app/canvas/[id]` | Graf węzłów | Edytor węzłów | v2+ (pominąć) |

### Ustawienia i administracja

| Trasa | Cel | Faza |
|---|---|---|
| `/app/settings/profile`, `/account` | Dane, bezpieczeństwo, eksport i usunięcie konta | MVP |
| `/app/settings/preferences` | Język, motyw, domyślna widoczność, autoodtwarzanie, powiadomienia | MVP |
| `/app/settings/billing` | Plan, rejestr kredytów z linkiem do zadania, faktury, anulowanie jednym kliknięciem, odstąpienie | MVP |
| `/app/settings/privacy` | Zgody (w tym biometryczna), opublikowane prace | v1 |
| `/app/settings/team`, `/api-keys` | Członkowie, role, limity wydatków; klucze API | v2 |
| `/admin/{models,presets,moderation,users,refunds}` | Rejestr modeli, CMS presetów, kolejka moderacji, zwroty | MVP (minimum) |

Mobile WWW: dolny pasek 5 zakładek (Start, Twórz, Biblioteka, Odkrywaj, Konto); composer jako bottom sheet; ustawienia drugorzędne za "Więcej"; przycisk Generuj przypięty z uwzględnieniem safe area. Aplikacja natywna dopiero po PWA [R05].

## 4. (b) Inwentarz komponentów design systemu

| Grupa | Komponenty | Stany i uwagi |
|---|---|---|
| Powłoka | AppShell, Sidebar, TopBar, BottomTabBar, CommandPalette, WorkspaceSwitcher, LocaleSwitcher | Aktywna pozycja widoczna niezależnie od hover |
| Composer | PromptInput (wzmianki `@element`, licznik znaków), ModeTabs, ModelPicker, ReferenceSlot (rola, limit), FramePair (start/end), KeyframeStrip, AspectRatioPicker, DurationSlider, ResolutionSelect, AudioToggle, VariantStepper, SeedField, NegativePromptField, PromptEnhanceToggle, AdvancedDrawer, GenerateButton | Formularz budowany z definicji modelu; GenerateButton: gotowy / liczy koszt / brak środków / wysyłanie / zablokowany planem |
| Model | ModelCard, CapabilityBadge, ModelCompareTable, LockedBadge | Plakietki: wejścia, maks. czas, maks. rozdzielczość, audio, cena od, licencja komercyjna |
| Media | MediaTile (obraz, wideo, audio), MediaGrid, VirtualGrid, MediaViewer, VideoPlayer, AudioWaveform, BeforeAfterSlider, MaskCanvas, AiLabel | Proporcje z metadanych; poster; placeholder rozmyty; zaznaczanie wielokrotne |
| Zadania | JobTile, QueueDrawer, QueueBadge, ProgressRing, EtaLabel | `reserving → queued (pozycja) → running → ingesting → succeeded`; `failed` (powód, "zwrócono X", ponów); `blocked` (moderacja, bez ponowienia tego samego promptu); `canceled`; `expired` |
| Kredyty | CreditMeter, CostChip, CostBreakdownPopover, LowBalanceBanner, PaywallModal, PlanCard, TopUpPicker, LedgerTable, RefundBadge | Koszt przed akcją; rejestr z identyfikatorem zadania |
| Akcje wyniku | ActionBar: warianty, upscale, animuj, przedłuż, edytuj, użyj ustawień, pobierz, udostępnij, publikuj, usuń; ShareDialog; PublishDialog (3 przełączniki widoczności) | Usuwanie przez toast z "Cofnij" |
| Presety | PresetCard (podgląd wideo po najechaniu), CategoryChips, CreationRail, SlotChecklist, RecreateButton | Schemat wejść z CMS |
| Postacie | CharacterCard, ElementChip, PhotoDropzone z oceną jakości, ConsentStep, TrainingProgress, TraitPicker | Statusy: trening, gotowa, błąd, zablokowana |
| Reżyserka | DirectorPanel, OptionWheel, LightRig, ShotCard, FinalPromptPreview | Słowniki z bazy |
| Reklamy | UrlImportField, BrandKitEditor, ProductCard, AvatarPicker, FormatPicker, ScriptEditor, CostReview, RunBoard | Kreator z cofaniem |
| Społeczność | FeedCard, LikeButton, RemixButton, ProfileHeader, ReportDialog | Etykieta AI obowiązkowa [R06] |
| System | Toast, EmptyState, ErrorState, Skeleton, ConfirmDialog, ConsentCheckbox, ShortcutSheet, NotificationItem | Każda lista ma stan pusty, ładowania i błędu |

## 5. (c) Zasady UX

### Przejąć (wzorce funkcjonalne)

1. Composer sterowany definicją modelu; zmiana modelu zachowuje prompt i zgodne ustawienia, a niezgodne oznacza ("ten model nie obsługuje klatki końcowej") [wnioskowanie na MCP-E].
2. Koszt przed kliknięciem i optymistyczna karta zadania od razu w feedzie [zweryfikowane: MCP-A, MCP-B].
3. Podgląd w miejscu z klawiaturą i zachowaniem scrolla [zweryfikowane: MCP-A].
4. Siatka bez przycinania, proporcje z metadanych [zweryfikowane: MCP-B].
5. Automatyczny zwrot przy błędzie, widoczny na karcie [R02].
6. Dwie ścieżki postaci: szybki element i trening [MCP-F].
7. Jawna zgoda na koszt w przepływach wieloetapowych (reklamy, agent) [MCP-F].
8. Rzemiosło interakcji: walidacja przy blur lub submit, błąd pod polem z poprawką, Esc zamyka jedną warstwę, fokus wraca do wyzwalacza, ruch 150-300 ms tylko `transform` i `opacity`, `prefers-reduced-motion` [zweryfikowane: MCP-B].

### Zrobić inaczej

| Wzorzec rynkowy | Nasza wersja |
|---|---|
| Free bez kredytów | Kilka darmowych obrazów dziennie na najtańszym modelu, bez karty [R04] |
| Plan roczny domyślny | Miesięczny domyślny; roczny jako jawny wybór z kwotą łączną |
| "Unlimited" z ukrytymi limitami | Nazwa "tryb wolny" z limitem i czasem oczekiwania podanymi liczbą |
| Liczniki i stałe promocje | Bez liczników; promocje z prawdziwą datą i najniższą ceną z 30 dni [R06] |
| Rejestr bez powiązania z zadaniem | Każdy wpis linkuje do generacji; zwroty oznaczone |
| Anulowanie w kilku krokach | Jeden ekran, bez ankiety blokującej; funkcja odstąpienia online [R06] |
| Tylko ciemny motyw | Jasny i ciemny; jasny przydatny przy ocenie packshotów |
| Limity ról zapisane tekstem | Limity strukturalne w rejestrze modeli, widoczne jako licznik "3/14" [R02] |
| Kredyty jako abstrakcja | Przelicznik na PLN w podpowiedzi kosztu |
| Nazwy realnych kamer | Opisy generyczne ("kamera kinowa pełnoklatkowa", "taśma 16 mm") |
| Szeroka licencja na treści | Licencja ograniczona do świadczenia usługi; publikacja zawsze opt-in |

### Dostępność

Cel: WCAG 2.2 AA mimo zwolnienia mikroprzedsiębiorstw z EAA [R06]. Minimum: widoczny fokus; siatka nawigowalna strzałkami (roving tabindex); `aria-live="polite"` dla zmian statusu zadań; automatyczny `alt` z promptu z możliwością edycji; brak autoodtwarzania dźwięku; pauza dla zapętlonych podglądów; stan nigdy samym kolorem; cele dotyku 44 px [zweryfikowane jako praktyka referencji: MCP-B].

### Skróty klawiaturowe (propozycja)

| Skrót | Akcja |
|---|---|
| `Ctrl/Cmd+Enter` | Generuj |
| `Ctrl/Cmd+K` | Paleta poleceń |
| `/` | Fokus na prompt |
| `@` | Wstaw element lub postać |
| `←` `→`, `Esc` | Poprzedni, następny, zamknij podgląd |
| `Spacja`, `M` | Odtwarzaj lub pauza, wycisz |
| `D`, `L`, `R`, `U`, `V` | Pobierz, polub, użyj ustawień, upscale, warianty |
| `?` | Lista skrótów |

### Budżety wydajności dla siatek mediów

| Obszar | Budżet lub reguła | Status |
|---|---|---|
| Core Web Vitals | LCP ≤ 2,5 s, INP ≤ 200 ms, CLS ≤ 0,1 na 75. percentylu mobile | [niepewne: progi z pamięci, [web.dev](https://web.dev/articles/vitals)] |
| CLS | Każdy kafel ma `aspect-ratio` z wymiarów zapisanych w bazie | [wnioskowanie; zgodne z MCP-B] |
| Wirtualizacja | Od ok. 60-100 kafli okno renderowania; paginacja kursorem po 24-48 | [wnioskowanie; referencja ma `VirtualGrid`: MCP-B] |
| Miniatury | 2-3 stałe warianty WebP/AVIF tworzone przy ingest (np. 320, 640, 1280 px), nie transformacje w locie | [zweryfikowane kosztowo: R05; formaty: [Vercel](https://vercel.com/docs/project-configuration/vercel-json)] |
| Obrazy | `loading="lazy"`, `decoding="async"`; wysoki priorytet tylko dla pierwszego rzędu; placeholder blurhash | [wnioskowanie] |
| Wideo w siatce | Tylko poster, `preload="none"`; odtwarzanie po najechaniu (opóźnienie ok. 150 ms) lub w kadrze na mobile; maks. 1-2 naraz; `muted playsinline`; pauza poza ekranem | [wnioskowanie] |
| Podgląd wideo | Osobny lekki plik podglądu (np. 480p, 3-5 s) zamiast mastera; master MP4 z `faststart` dopiero w viewerze | [wnioskowanie; faststart: R05] |
| JS | Powłoka aplikacji do ok. 200 kB gzip; edytor maski, oś czasu i canvas ładowane leniwie | [wnioskowanie] |
| Status zadań | Realtime + awaryjny polling co 3-5 s tylko przy aktywnych zadaniach | [zweryfikowane: R05] |

### i18n (PL/EN)

- `next-intl`, segment `[locale]`, ICU [R05]. Polska liczba mnoga ma trzy formy: 1 kredyt, 2 kredyty, 5 kredytów.
- Formaty: przecinek dziesiętny, PLN brutto, daty `13.11.2026`.
- Polskie teksty są zwykle o 20-30% dłuższe od angielskich: przyciski elastyczne, bez sztywnych szerokości [wnioskowanie].
- Prompt po polsku: ulepszacz tłumaczy na angielski i **pokazuje** wynik; użytkownik może go edytować lub wyłączyć [wnioskowanie].
- Nazwy i opisy presetów w tabeli tłumaczeń [R05]; miniatury presetów bez tekstu.
- Font z pełnym zestawem polskich znaków (ą ć ę ł ń ó ś ź ż) we wszystkich grubościach.

## 6. (d) Własna tożsamość wizualna

Znaki rozpoznawcze referencji, których należy unikać w zestawie [zweryfikowane: MCP-B, MCP-D]: stały ciemny motyw bez trybu jasnego; limonkowe CTA z fazą 3D; biały przycisk drugorzędny i "szklany" trzeciorzędny; Space Grotesk w nagłówkach + Inter w tekście; ikony lucide; ikona iskierek przy kredytach. Pojedyncze elementy (ciemny motyw, Inter, koszt w przycisku) są powszechne; ryzykowne jest powielenie **kombinacji** oraz nazw i treści [wnioskowanie; ramy prawne: R06].

Wytyczne:

1. **Trzy atrybuty marki przed kolorem**, np. "spokojna, przejrzysta, warsztatowa" jako kontra do estetyki "hype".
2. **Kolor:** akcent spoza żółto-zielonych; neutralne tło, które nie zabarwia ocenianych mediów; oba motywy.
3. **Typografia:** inna para krojów z pełnym polskim zestawem znaków; cyfry tabularyczne dla kosztów i liczników.
4. **Własny znak jednostki rozliczeniowej** i własna jej nazwa; bez iskierek.
5. **Ikony:** inny zestaw lub własna grubość linii, konsekwentnie.
6. **Nazewnictwo funkcjonalne po polsku i angielsku** ("Postacie", "Reżyserka", "Presety"). Żadnych nazw własnych referencji ani nazw jej presetów.
7. **Sygnatura układu:** np. stały "paragon" kosztu obok przycisku (rozbicie: model × czas × rozdzielczość × warianty, kwota w PLN) zamiast samej liczby.
8. **Treści własne:** miniatury i przykłady generowane samodzielnie; nigdy media, opisy ani prompty z galerii referencji.
9. **Tokeny w trzech warstwach** (prymitywy → semantyczne → komponentowe) od pierwszego dnia.
10. **Test pomyłki:** zrzuty obu produktów obok siebie w skali szarości i w kolorze; jeśli osoba z zewnątrz myli produkty, zmienić kombinację.

## 7. Ryzyka

- Raport nie zawiera żywego teardownu WWW; układ górnego menu i ekranów konkurentów może być nieaktualny.
- Wytyczne z MCP dotyczą aplikacji osadzanych w platformie referencji. Deklarują one zgodność z jej własnymi produktami, ale główny interfejs może odbiegać w szczegółach [wnioskowanie].
- Regulamin referencji może ograniczać wykorzystanie konta do budowy produktu konkurencyjnego [niepewne; do sprawdzenia przez prawnika, R06].
- Zakres v1 i v2 jest duży dla jednej osoby; bez dyscypliny "jeden composer, trzy układy" liczba ekranów wymknie się spod kontroli.

## 8. Do zweryfikowania ręcznie (1-2 h, zrzuty ekranu)

1. Górne menu i mega-menu referencji; ekran startowy po zalogowaniu.
2. Composer obrazu i wideo: kolejność kontrolek, wygląd listy modeli i plakietek, miejsce przełącznika unlimited i ulepszania promptu.
3. Modal braku kredytów, checkout (domyślny okres, liczniki), ścieżka anulowania.
4. Panel reżysera: liczba i nazwy opcji, sposób prezentacji ruchów kamery.
5. Ten sam zestaw dla Krea, Freepik, OpenArt i Runway.
6. Trustpilot i Reddit: 20 najnowszych skarg, pogrupowanych.

## Źródła

**MCP (odczyt read-only konektora Higgsfield, 2026-11-13):**
- **MCP-A** `get_workflow_bundle_file`: `website-builder-flow/references/app-layouts.md`
- **MCP-B** `.../references/quanta-design.md`
- **MCP-C** `.../references/fnf-react.md`
- **MCP-D** `.../references/app-flow.md`
- **MCP-E** `models_explore get`: `cinematic_studio_video_4_0`, `marketing_studio_v2_video`, `kling4_0`, `soul_2`
- **MCP-F** opisy i schematy narzędzi: `manage_reference_elements`, `show_characters`, `show_generations`, `list_project_assets`, `share_project`, `publish_project`, `tiktok_prepare_publish`, `create_voice`, `ads_studio_create_brand`, `ads_studio_generate`, `generate_image`, `generate_video`, `get_presets`, `cancel_trial_auto_renewal`, `get_preferences`
- **MCP-G** `ads_studio_list_avatars` (3 rekordy, tylko kształt danych)
- Dokumentacja Vercel (narzędzie `search_vercel_documentation`): [Image Optimization quickstart](https://vercel.com/docs/image-optimization/quickstart), [vercel.json images](https://vercel.com/docs/project-configuration/vercel-json)

**Raporty sąsiednie (źródła WWW zweryfikowane przez ich autorów):**
- **R01** `01-mapa-produktu-higgsfield.md`, **R02** `02-katalog-modeli-i-presetow.md`, **R04** `04-ekonomia-cennik-platnosci.md`, **R05** `05-architektura-i-stack.md`, **R06** `06-prawo-compliance-bezpieczenstwo-tresci.md`

**Adresy przytoczone za raportami sąsiednimi (nieotwierane w tej sesji):**
- Higgsfield: [oficjalne platformy](https://higgsfield.ai/creator-hub/help-center/getting-started/official-higgsfield-platforms), [postać: help](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-create-and-use-a-soul-id-character), [storyboard: help](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-use-popcorn), [studio filmowe 4.0](https://higgsfield.ai/blog/cinema-studio-4-0), [canvas](https://higgsfield.ai/canvas-intro), [kredyty a unlimited](https://higgsfield.ai/blog/credits-vs-unlimited-ai-video-generation), [zwroty: help](https://higgsfield.ai/creator-hub/help-center/refunds/why-didnt-i-receive-a-refund-after-canceling-my-subscription), [changelog](https://higgsfield.ai/creator-hub/changelog)
- Strony trzecie: [Krea o planie Free](https://www.krea.ai/blog/what-is-higgsfield-ai-pricing-free-plan-and-alternatives-in-2026), [aliteq o unlimited](https://aliteq.com/higgsfield-unlimited-explained), [MindStudio o skargach](https://www.mindstudio.ai/blog/higgsfield-subscription-cancellation-complaints), [BottleRocket o ToS](https://www.bottlerocketcontent.com/higgsfield-tos-controversy-explained/)

**Do weryfikacji (nieotwierane, podstawa twierdzeń [niepewne]):** [web.dev: Web Vitals](https://web.dev/articles/vitals), [WCAG 2.2](https://www.w3.org/TR/WCAG22/), [krea.ai](https://www.krea.ai), [freepik.com](https://www.freepik.com), [openart.ai](https://openart.ai), [runwayml.com](https://runwayml.com), [Trustpilot: higgsfield.ai](https://www.trustpilot.com/review/higgsfield.ai)
