# 06. Prawo, compliance i bezpieczeństwo treści (Trust & Safety)

> Research do planowania, nie porada prawna. Miejsca wymagające prawnika oznaczono **[PRAWNIK]**.

## Weryfikacja na żywo (2026-11-13)

Przebieg weryfikacyjny wykorzystał 24 zapytania WebSearch (cały przydzielony budżet). WebFetch nadal blokuje polityka sieci, więc potwierdzenia opierają się na wynikach wyszukiwania (strony urzędowe, kancelarie, prasa branżowa), a nie na lekturze pełnych tekstów aktów. Tag **[zweryfikowane]** z linkiem oznacza potwierdzenie w tym przebiegu.

**Potwierdzone**

- **AI Act:** art. 50 stosuje się od 2.08.2026. Digital Omnibus (AI) jest obowiązującym prawem: rozporządzenie (UE) 2026/1744, Dz.Urz. 24.07.2026, w mocy od 27.07.2026. Okres przejściowy dla art. 50(2) obejmuje tylko systemy sprzed 2.08.2026 i trwa do 2.12.2026. Od 2.12.2026 dwa nowe zakazy w art. 5 (intymne treści bez zgody, CSAM). High-risk z załącznika III od 2.12.2027.
- **Kodeks oznaczania treści AI:** wersja końcowa 10.06.2026, potwierdzenie adekwatności 8.07.2026, końcowe wytyczne KE do art. 50 z 20.07.2026, trzy gotowe ikony UE.
- **Polska:** ustawa o systemach sztucznej inteligencji (Dz.U. 2026 poz. 1003, organ: KRiBSI); pierwsza ustawa wdrażająca DSA podpisana we wrześniu 2026, koordynatorem jest Prezes UKE.
- **KSeF:** terminy 1.02.2026, 1.04.2026 i 1.01.2027; faktury konsumenckie dobrowolne.
- **TAKE IT DOWN Act:** obowiązki od 19.05.2026, 48 h, egzekwuje FTC, kara do 53 088 USD za naruszenie.
- **Stripe:** zakaz treści dla dorosłych obejmuje wprost treści generowane przez AI.
- **OpenAI Moderation:** bezpłatne; obraz oceniany tylko w 6 kategoriach, `sexual/minors` wyłącznie dla tekstu.
- **Spory:** MiniMax przegrał wniosek o odrzucenie pozwu studiów (05.2026); Getty ma zgodę na apelację; odwołanie ws. DPF (C-703/25 P) w toku, DPF obowiązuje.
- **UK:** Ofcom traktuje serwis genAI, w którym użytkownicy udostępniają sobie treści, jako usługę user-to-user.
- **Higgsfield:** spór o licencję na treści użytkowników z lipca 2026 i jej zawężenie.

**Skorygowane**

- Omnibus: z "wstępnego porozumienia [niepewne]" na przyjęty akt z numerem i datami.
- SynthID nie jest już wyłącznie w modelach Google: OpenAI osadza go obok C2PA w obrazach z API.
- Pliki z API Kling i Seedance nie miały manifestu C2PA w niezależnych testach, więc własne oznaczanie jest konieczne dla każdego modelu.
- Polska DSA: po wecie z 9.01.2026 powstały dwie ustawy; pierwsza została podpisana i ogłoszona.
- Funkcja odstąpienia: Polska nie wdrożyła dyrektywy 2023/2673 w terminie (projekt UC169 we wrześniu 2026 w konsultacjach).
- KSeF: dodano obowiązek odbierania faktur w KSeF od 1.02.2026 dla wszystkich przedsiębiorców.
- Midjourney: sprawa połączona z pozwem Warner Bros. Discovery; w 2026 mediacja i discovery, bez rozstrzygnięcia.
- Higgsfield: regulamin zakazuje używania outputów do trenowania, fine-tuningu i destylacji modeli.

**Nadal otwarte**

- Czy dostawca systemu opakowujący cudze modele może polegać na oznaczeniach dostawcy modelu (brak potwierdzenia w kodeksie i wytycznych) oraz dokładny skład warstw w sekcji 1 kodeksu.
- Data dla high-risk z załącznika I (2.08.2028 podaje jedno źródło wtórne) i ewentualne wyłączenie przy nowych zakazach z art. 5.
- Druga ustawa DSA (nakazy blokowania): podpis czy weto; czy KRiBSI już faktycznie działa.
- Wyłączenie faktur OSS z KSeF; warunki i cenniki PhotoDNA, Cloudflare, Google Content Safety API, Thorn Safer.
- Stosowanie TAKE IT DOWN Act do serwisów spoza USA; obowiązki małego serwisu zagranicznego w UK i skuteczność blokady geograficznej.
- Brzmienie klauzul Higgsfield o scrapingu, reverse engineeringu i produkcie konkurencyjnym.
- Pozew w sprawie Seedance (znaleziono tylko wezwania z 02.2026); GEMA v. OpenAI, umowa Disney-OpenAI, otwarte narzędzia znaków wodnych, postępowanie KE wobec X.

**Ograniczenie pierwotnej sesji.** Przy pisaniu raportu wspólny budżet WebSearch był wyczerpany (0 udanych wyszukiwań), a WebFetch blokowała polityka sieci (nie rozwiązują się m.in. `digital-strategy.ec.europa.eu`, `artificialintelligenceact.eu`, `www.congress.gov`, `ksef.podatki.gov.pl`). Twierdzenia bez tagu [zweryfikowane] nadal opierają się na wiedzy modelu (stan ok. połowy 2026) oraz na raportach równoległych 01, 03 i 04. Tagi:

- **[zweryfikowane]** + link - potwierdzone wynikiem wyszukiwania w przebiegu z 13.11.2026;
- **[zweryfikowane: R0x]** - potwierdzone źródłem na żywo w raporcie równoległym nr x;
- **[z pamięci]** - treść opublikowanego aktu lub orzeczenia znana modelowi; link wskazuje źródło pierwotne do sprawdzenia, ale nie został pobrany w tej sesji;
- **[wnioskowanie]** - moja ocena;
- **[niepewne]** - wymaga sprawdzenia; dotyczy zwłaszcza wszystkiego po maju 2026.

## TL;DR

- **Odpowiednik funkcjonalny jest legalny.** Idee, funkcje, zasady działania i ogólne wzorce UX nie podlegają ochronie. Ryzykowne lub bezprawne: znaki i podobne nazwy, kopiowanie wyglądu, tekstów, nazw presetów, promptów, mediów i kodu, scraping, używanie konta/API konkurenta jako zaplecza. Słowo "kopia" nie może pojawić się w marketingu.
- **AI Act:** firma wystawiająca system pod własną marką jest **dostawcą (provider) systemu AI**, a nie tylko deployerem. Art. 50 stosuje się od 2.08.2026; Digital Omnibus (rozporządzenie 2026/1744) dał czas do 2.12.2026 tylko systemom sprzed 2.08.2026, więc nowy produkt nie ma okresu przejściowego. Każdy output trzeba oznaczać maszynowo i umożliwić detekcję. Od 2.12.2026 obowiązuje też zakaz systemów generujących intymne treści bez zgody i CSAM (art. 5, kary z najwyższego progu). Kara do 15 mln EUR lub 3% obrotu (dla MŚP niższa z kwot).
- **RODO:** zdjęcia twarzy i próbki głosu użyte do treningu postaci lub klonowania traktuj jak dane biometryczne (art. 9): wyraźna zgoda, DPIA, osobna retencja. Najtrudniejszy transfer to trasy do producentów modeli z Chin.
- **DSA:** obowiązki hostingu od pierwszego dnia (art. 11-18). Publiczna galeria to "platforma internetowa", ale mikro i małe firmy są zwolnione z sekcji 3.
- **Treści:** zero NSFW (wymusza to Stripe), twardy zakaz CSAM i NCII (od 2.12.2026 także ustawowy zakaz z art. 5 AI Act), 48 h na usunięcie NCII (USA, egzekwowane przez FTC od 19.05.2026), 1 h na nakaz usunięcia treści terrorystycznych (UE).
- **Proweniencja:** wymagane jest oznaczenie maszynowe; rekomendowany zestaw to C2PA + niewidoczny znak wodny + rejestr odcisków + etykieta "AI" w galerii (ikona UE z kodeksu). Oznaczeń dostawców nie można zakładać: w testach z 2026 pliki z API Kling i Seedance nie miały C2PA.
- **IP:** output bez twórczego wkładu człowieka najpewniej nie ma ochrony autorskiej; agregatory nie dają indemnifikacji; galeria z cudzymi postaciami to bezpośrednia ekspozycja.
- **Konsument i firma:** funkcja odstąpienia online, zgoda na natychmiastowe rozpoczęcie świadczenia, najniższa cena z 30 dni, KSeF dla B2B, sp. z o.o. przed publicznym startem.

## 1. Granice budowy odpowiednika funkcjonalnego

Podstawy: ochrona autorska obejmuje sposób wyrażenia, nie idee, procedury i zasady działania ([pr. aut.][pa] art. 1 ust. 2(1)) [z pamięci]. TSUE w C-406/10 SAS Institute uznał, że funkcjonalność programu, język programowania i format plików nie są chronione prawem autorskim ([C-406/10][sas]) [z pamięci]. Interfejs graficzny może być jednak utworem, jeśli jest oryginalny (C-393/09 BSA) [z pamięci]. Naśladowanie cech funkcjonalnych produktu nie jest czynem nieuczciwej konkurencji ([UZNK][uznk] art. 13 ust. 2) [z pamięci].

| Obszar | Wolno | Nie wolno / ryzyko | Podstawa |
|---|---|---|---|
| Funkcje i architektura | Studio obrazu/wideo/audio, presety, kredyty, feed, spójność postaci | - | pr. aut. art. 1 ust. 2(1); C-406/10 |
| Marka | Własna nazwa, logo, domena po badaniu w EUIPO/TMview/USPTO (klasy 9, 41, 42) | Nazwa, domena lub logo podobne do konkurenta; jego nazwy produktów i presetów | [EUTMR][eutmr] art. 9; UZNK art. 5 i 10 |
| Wygląd | Powszechne wzorce (siatka, panel promptu, karty modeli) | Odwzorowanie układu, palety, ikon, animacji 1:1; niezarejestrowany wzór UE chroni 3 lata przed kopiowaniem | UZNK art. 3 i 13; C-393/09 |
| Treść | Własne teksty, miniatury, prompty, dema | Kopiowanie opisów, master promptów, plików `SKILL.md`, miniatur, wideo demo, struktury katalogu 1:1 | pr. aut.; UZNK art. 3 ("pasożytnictwo") i art. 11 (tajemnica przedsiębiorstwa) |
| Konto konkurenta | Obserwacja publicznego produktu jako użytkownik | Ekstrakcja katalogu/promptów w celu odtworzenia, scraping galerii, odsprzedaż jego usługi lub API | Regulamin Higgsfield: redystrybucja "Developer Access" to istotne naruszenie [zweryfikowane: R03]. Sekcja 5 ("User Content and Certain Restrictions") ogranicza komercyjną eksploatację samej usługi (5.2(i)) i zakazuje używania outputów do trenowania, fine-tuningu lub destylacji modeli AI (5.1(iii), 5.2(iv)) [zweryfikowane] ([pomoc Higgsfield](https://higgsfield.ai/creator-hub/help-center/account-and-privacy/who-owns-my-generations-and-can-i-use-them-commercially)). Brzmienie klauzul o scrapingu, reverse engineeringu i produkcie konkurencyjnym [niepewne: wyszukiwarka nie zwróciła tekstu sekcji 5; przeczytać [regulamin](https://higgsfield.ai/terms-of-use-agreement), wersja z 23.10.2026] |
| Reklama | "Alternatywa dla X" z obiektywnym, sprawdzalnym porównaniem cech i cen | "Klon/kopia X", wykorzystanie renomy, przedstawianie usługi jako imitacji usługi z chronionym znakiem | UZNK art. 16 ust. 3 pkt 7-8; [dyrektywa 2006/114][dir114] art. 4 |
| Słowa kluczowe | Reklama na frazę z marką konkurenta, jeśli reklama nie myli co do pochodzenia | Marka konkurenta w treści reklamy w sposób sugerujący powiązanie | TSUE C-236/08, C-323/09 [z pamięci] |
| Nazwy modeli | "Kling", "Veo" itd. opisowo, zgodnie z wytycznymi marek | Sugerowanie partnerstwa, cudze logotypy bez zgody | [wnioskowanie] |
| Kod | Własny kod, open source zgodnie z licencją | Dekompilacja lub kopiowanie bundli JS konkurenta | pr. aut. art. 74 |

Uwagi praktyczne [wnioskowanie]:

- Raport 02 opisuje treści pozyskane z konta i konektora MCP konkurenta (`SKILL.md`, master prompty, nazwy presetów). Traktować je wyłącznie jako opis architektury. Do repo nie trafia żaden ich tekst ani plik.
- Prowadzić dowody niezależnej twórczości: historia git, pliki projektowe, autorstwo promptów, własne nazewnictwo.
- Outputy z konta Higgsfield nie mogą służyć do trenowania ani dostrajania własnych modeli (LoRA, klasyfikatory, zbiory ewaluacyjne): zakazuje tego ich regulamin (wiersz "Konto konkurenta").
- Lekcja z rynku: w lipcu 2026 nowa wersja regulaminu Higgsfield przyznawała firmie wieczystą, nieodwołalną i sublicencjonowalną licencję na uploady i outputy, także do promocji. Po krytyce twórców zapis wycofano (ok. 26.07.2026); wersja obowiązująca od 27.08.2026 ogranicza licencję do czasu przechowywania treści i kończy ją usunięcie konta, a treści prywatne wymagają zgody na użycie w marketingu [zweryfikowane] ([Higgsfield](https://higgsfield.ai/blog/terms-of-use-privacy-policy-update), [Stork](https://www.stork.ai/blog/higgsfields-ai-terms-trap)). Niezależna analiza twierdzi, że zgoda na trening na treściach użytkowników pozostała bez zmian, a jedynym opt-outem jest usunięcie treści ([MindStudio](https://mindstudio.ai/blog/higgsfield-terms-of-service-backlash)) [sporne, nie sprawdzone w tekście regulaminu]. Dla własnego regulaminu: wąska licencja (wyłącznie świadczenie usługi, do usunięcia treści), marketing i trening tylko opt-in [wnioskowanie].
- Roszczenia z UZNK art. 18 (zaniechanie, odszkodowanie, wydanie korzyści) pozywający kieruje do sądu w Polsce, więc ryzyko jest realne także wobec firmy z USA jako powoda. **[PRAWNIK]**: badanie znaku przez rzecznika patentowego przed zakupem domeny i startem.

## 2. EU AI Act

**Kalendarz** ([rozporządzenie 2024/1689][aia] art. 113) [z pamięci]: wejście w życie 1.08.2024; zakazy i AI literacy od 2.02.2025; obowiązki GPAI od 2.08.2025; stosowanie ogólne, w tym **art. 50, od 2.08.2026** [zweryfikowane] ([KE](https://digital-strategy.ec.europa.eu/en/news/commission-publishes-code-practice-marking-and-labelling-ai-generated-content)); terminy high-risk zmienił Omnibus (niżej).

**Digital Omnibus (AI)** jest przyjęty i obowiązuje jako **rozporządzenie (UE) 2026/1744** (wniosek Komisji z 19.11.2025, [KE][omnibus]). Parlament głosował 16.06.2026, Rada zatwierdziła akt 29.06.2026, podpisano go 8.07.2026, opublikowano w Dz.Urz. 24.07.2026, wszedł w życie 27.07.2026 [zweryfikowane] ([White & Case](https://www.whitecase.com/insight-alert/eu-ai-omnibus-enters-force-amending-ai-act), [Lewis Silkin](https://www.lewissilkin.com/insights/2026/07/27/the-digital-omnibus-on-ai-enters-into-force-today-102nedo), [Addleshaw Goddard](https://www.addleshawgoddard.com/en/insights/insights-briefings/2026/technology/eu-ai-act-ai-omnibus-formally-adopted/)). Zmiany istotne dla produktu, potwierdzone omówieniami aktu ([Cuatrecasas](https://www.cuatrecasas.com/en/global/intellectual-property/art/digital-omnibus-ai-has-been-published), [EY](https://www.ey.com/en_gr/technical/tax/tax-alerts/regulation-eu-2026-1744-digital-omnibus-on-ai), [Usercentrics](https://usercentrics.com/knowledge-hub/eu-ai-act-high-risk-delay-article-50-transparency-consent/)); pełnego tekstu z Dz.Urz. nie czytałem:

- **Art. 50(2):** nowy art. 111(4) daje czas do **2.12.2026** wyłącznie dostawcom systemów generatywnych wprowadzonych do obrotu przed 2.08.2026 i tylko w zakresie oznaczania maszynowego. Komisja proponowała 6 miesięcy, Parlament 3, przyjęto 4. Pozostałe obowiązki z art. 50 nie są odroczone [zweryfikowane].
- **Nowe zakazy w art. 5, stosowane od 2.12.2026:** systemy AI generujące realistyczne intymne lub seksualne obrazy, wideo albo audio możliwej do zidentyfikowania osoby bez jej zgody oraz systemy generujące CSAM [zweryfikowane]. Jedno źródło opisuje wyłączenie dla systemów ze skutecznymi zabezpieczeniami zapobiegawczymi [niepewne: nie potwierdzone tekstem aktu]. Naruszenie zakazu z art. 5 to najwyższy próg kar (do 35 mln EUR / 7%).
- **High-risk:** załącznik III od 2.12.2027 [zweryfikowane]; załącznik I od 2.08.2028 [jedno źródło wtórne; sprawdzić w Dz.Urz.].

Skutek dla tego produktu [wnioskowanie]: okres przejściowy go nie dotyczy (system powstaje po 2.08.2026, a ulga i tak wygasa 2.12.2026). Polityka "zero NSFW" oraz blokady treści intymnych z realnymi osobami i CSAM przestają być tylko wymogiem operatora płatności: od 2.12.2026 są warunkiem legalności systemu w UE, więc zabezpieczenia trzeba zaprojektować i udokumentować (testy, logi blokad, opis warstw z sekcji 5.3). **[PRAWNIK]**: brzmienie nowych liter art. 5 i zakres ewentualnego wyłączenia.

**Kim jest firma opakowująca cudze modele** [wnioskowanie z art. 3(3)-(4), 25, 50]:

| Rola | Kiedy | Obowiązek |
|---|---|---|
| Dostawca systemu AI | Udostępnia system pod własną nazwą, nawet zbudowany na cudzych modelach | Art. 50(1): informacja o interakcji z AI (asystent, agent). Art. 50(2): outputy oznaczone w formacie maszynowym i wykrywalne jako sztuczne; rozwiązanie skuteczne, interoperacyjne, odporne. Wyjątek: funkcje pomocnicze przy standardowej edycji (np. upscale, usuwanie tła) |
| Deployer | Firma sama publikuje treści (marketing, wyróżnione prace) | Art. 50(4): ujawnienie deepfake'a; dla dzieł ewidentnie artystycznych lub satyrycznych w formie niezakłócającej odbioru |
| Użytkownik-profesjonalista | Marketer publikujący wygenerowaną reklamę | Sam jest deployerem z art. 50(4); platforma powinna dać mu etykietę i instrukcję. Użytek czysto osobisty wyłączony (art. 2(10)) |
| Dostawca modelu GPAI | Tylko przy istotnej modyfikacji modelu | Trening LoRA postaci jest daleko poniżej progu z wytycznych KE (ok. 1/3 mocy obliczeniowej treningu bazowego) [z pamięci + wnioskowanie] |

- Poleganie wyłącznie na oznaczeniach dostawcy modelu nie wystarcza: odpowiedzialność z art. 50(2) zostaje przy dostawcy systemu [wnioskowanie; w przebiegu z 13.11.2026 nie znalazłem w omówieniach kodeksu ani wytycznych potwierdzenia, że dostawca systemu może się powołać na oznaczenie dostawcy modelu, więc pytanie zostaje dla **[PRAWNIK]**]. W praktyce nie ma też na czym polegać: w niezależnych testach z 2026 pliki z API Kling i Seedance nie miały manifestu C2PA (sekcja 6).
- **Kodeks postępowania ws. oznaczania i etykietowania treści AI** ([KE][cop]): wersja końcowa opublikowana **10.06.2026** [zweryfikowane] ([KE](https://digital-strategy.ec.europa.eu/en/news/commission-publishes-code-practice-marking-and-labelling-ai-generated-content), [Jones Day](https://www.jonesday.com/en/insights/2026/06/european-commission-publishes-final-code-of-practice-on-marking-and-labelling-aigenerated-content)). Komisja potwierdziła jego adekwatność 8.07.2026, a **20.07.2026** wydała końcowe wytyczne do art. 50 [zweryfikowane] ([Reed Smith](https://www.reedsmith.com/our-insights/blogs/viewpoints/102nbz0/transparency-obligations-for-ai-generated-content-the-code-of-practice-adequacy/), [Orrick](https://www.orrick.com/en/Insights/2026/08/EU-AI-Act-Transparency-Obligations-for-AI-Generated-Content-Article-50)). Kodeks jest dobrowolny, nie zastępuje AI Act ani wytycznych i nie nakłada obowiązków ponad akt ([FAQ KE](https://digital-strategy.ec.europa.eu/en/faqs/code-practice-transparency-ai-generated-content)). Sekcja 1 jest dla dostawców systemów generatywnych (art. 50(2): oznaczanie i wykrywanie), sekcja 2 dla deployerów (art. 50(4): deepfake'i i teksty w sprawach publicznych). Co wynika z omówień [zweryfikowane] ([Freshfields](https://www.freshfields.com/en/our-thinking/blogs/technology-quotient/eu-ai-act-unpacked-33-the-final-code-of-practice-on-transparency-of-ai-generate-102n4yx), [DLA Piper](https://www.dlapiper.com/en-us/insights/publications/2026/07/what-the-eus-new-code-of-practice-means), [Paul Weiss](https://www.paulweiss.com/insights/client-memos/eu-finalises-transparency-rules-for-ai-generated-content)):
  - kodeks nie narzuca jednej techniki, bo żadna pojedyncza nie spełnia łącznie wymogów skuteczności, interoperacyjności, odporności i niezawodności; według jednej z analiz zwróconych przez wyszukiwarkę potrzebne są co najmniej dwie warstwy oznaczenia maszynowego;
  - oznaczenie ma przetrwać ścieżki eksportu oferowane przez system (pobranie, udostępnienie);
  - dostawca udostępnia mechanizm wykrywania treści; interfejs lub narzędzie ma być hostowane w UE albo możliwe do uruchomienia lokalnie i zgodne z RODO;
  - dla deployerów są trzy gotowe ikony UE: treść w pełni wygenerowana, treść zmodyfikowana oraz ikona podstawowa z interaktywną drugą warstwą;
  - wytyczne wymagają od deployerów w złożonych łańcuchach dystrybucji proporcjonalnych środków, w tym postanowień umownych z partnerami, aby etykieta pozostała widoczna dalej.

  Dokładny skład warstw (podpisane metadane, niewidoczny znak wodny, odciski/logi) i zakaz usuwania oznaczeń znam z projektów z 12.2025 i 03.2026 [z pamięci]; brzmienia końcowego nie potwierdziłem. Podpisanie sekcji 1 pozostaje najprostszym sposobem wykazania zgodności ([zasady podpisywania](https://digital-strategy.ec.europa.eu/en/faqs/signing-code-practice-transparency-ai-generated-content)).
- System nie jest high-risk, o ile nie wykonuje identyfikacji biometrycznej, kategoryzacji biometrycznej ani rozpoznawania emocji. Weryfikacja 1:1 ("czy to ta sama osoba") nie jest zdalną identyfikacją [z pamięci]. Art. 5(1)(e) zakazuje budowy baz rozpoznawania twarzy przez nieukierunkowany scraping, więc własna baza twarzy celebrytów ze scrapingu odpada.
- **Kary** (art. 99): do 35 mln EUR / 7% za praktyki zakazane; do 15 mln EUR / 3% m.in. za art. 50; do 7,5 mln EUR / 1% za błędne informacje; dla MŚP i startupów niższa z dwóch kwot [z pamięci].
- **Polska:** ustawa z 3.07.2026 o systemach sztucznej inteligencji ([Dz.U. 2026 poz. 1003](https://eli.gov.pl/eli/DU/2026/1003)), ogłoszona 27.07.2026, weszła w życie 11.08.2026; art. 8-18 oraz rozdziały 3-5, 8 i 9 obowiązują od 28.10.2026. Organem nadzoru rynku jest **Komisja Rozwoju i Bezpieczeństwa Sztucznej Inteligencji (KRiBSI)**: kontrole, postępowania, skargi i administracyjne kary pieniężne [zweryfikowane] ([Bankier](https://www.bankier.pl/wiadomosc/Polska-wdraza-AI-Act-Powstal-nowy-organ-nadzoru-nad-sztuczna-inteligencja-9149707.html), [Forsal](https://forsal.pl/biznes/technologie/artykuly/11274552,polska-powoluje-nowy-organ-do-kontroli-ai-bedzie-przyjmowal-skargi-i-nakladal-kary.html)). Czy Komisja jest już obsadzona i prowadzi postępowania: [niepewne].

## 3. RODO

| Temat | Ustalenie | Status |
|---|---|---|
| Podstawy prawne | Konto, generacje, płatności: art. 6(1)(b). Bezpieczeństwo, anty-fraud, moderacja: art. 6(1)(f) z testem równowagi. Marketing i cookies: zgoda ([PKE][pke] art. 398-399). Księgowość: art. 6(1)(c) | [z pamięci] |
| Twarz i głos | Zdjęcie samo w sobie nie jest daną biometryczną (motyw 51). Staje się nią przy przetwarzaniu technicznym służącym jednoznacznej identyfikacji (art. 4(14), art. 9). Embedding tożsamości, LoRA postaci, model głosu i weryfikacja mówcy: przyjąć reżim art. 9 i **wyraźną zgodę** (art. 9(2)(a)), odrębną od regulaminu, odwoływalną | Kwalifikacja sporna [niepewne]; podejście ostrożne [wnioskowanie] **[PRAWNIK]** |
| Osoby trzecie na zdjęciach | Platforma nie ma ich zgody. Minimum: oświadczenie użytkownika o prawach i zgodzie, zakaz w regulaminie, kanał sprzeciwu i usunięcia dla osoby przedstawionej (art. 17, 21). Polskie prawo dodatkowo: zgoda na rozpowszechnianie wizerunku ([pr. aut.][pa] art. 81), wizerunek i głos jako dobra osobiste (k.c. art. 23-24) | [z pamięci] |
| DPIA | Wymagana przed funkcjami wizerunku/głosu: dane biometryczne + innowacyjna technologia są w wykazie Prezesa UODO ([M.P. 2019 poz. 666][dpia]) | [z pamięci] |
| Powierzenie | Umowy art. 28 z: Supabase, Vercel, agregatorem modeli, dostawcą moderacji, e-mail, analityką. Publiczna lista podprocesorów. Rejestr czynności (art. 30) obowiązuje mimo małej skali, bo przetwarzanie nie jest sporadyczne | [z pamięci] |
| Transfery do USA | Dostawca na liście [Data Privacy Framework][dpf] albo SCC + ocena transferu. Sąd UE oddalił skargę Latombe'a na DPF 3.09.2025. Odwołanie z 31.10.2025 (sprawa C-703/25 P) jest w toku przed TSUE; w 06.2026 Microsoft przystąpił po stronie Komisji. Nie znalazłem terminu rozprawy, opinii rzecznika ani wyroku, więc DPF nadal obowiązuje | [zweryfikowane] ([WilmerHale](https://www.wilmerhale.com/en/insights/blogs/wilmerhale-privacy-and-cybersecurity-law/20251201-european-court-of-justice-to-review-challenge-to-eu-us-data-privacy-framework), [IEU Monitoring](https://ieu-monitoring.com/editorial/microsoft-backs-eu-commission-in-eu-court-case-on-transatlantic-data-flows-and-privacy/1244467/)); SCC w umowach jako plan awaryjny [wnioskowanie] |
| Transfery do Chin | Brak decyzji o adekwatności; SCC + TIA trudne do obrony. Irlandzki organ ukarał TikTok kwotą 530 mln EUR (05.2025) za transfery do Chin. Endpointy Kling i ByteDance mają siedzibę dostawcy "CN"; fal nie zapewnia rezydencji danych w UE | [z pamięci]; [zweryfikowane: R03] |
| Retencja | Referencje wejściowe: krótko (np. 30 dni) lub do usunięcia przez użytkownika. Modele postaci/głosu: do wycofania zgody. Logi bezpieczeństwa: 6-12 mies. Dokumenty księgowe: 5 lat podatkowych. Usunięcie konta kasuje dane także u podprocesorów | [wnioskowanie] |
| Małoletni | Zgoda dziecka na usługi online w Polsce od 16 lat (art. 8). Rekomendacja: usługa 18+ w regulaminie, bez profilowania wieku biometrią | [z pamięci]; [wnioskowanie] |
| USA | Illinois BIPA: pisemna zgoda i polityka retencji dla geometrii twarzy i odcisku głosu, prywatne powództwo z odszkodowaniem ustawowym ([BIPA][bipa]) | [z pamięci] **[PRAWNIK US]** |

Decyzja architektoniczna [wnioskowanie]: funkcje z twarzą realnej osoby kierować wyłącznie do tras z DPA i transferem do USA/UE, a trasy "CN" zostawić dla generacji bez danych osobowych albo opisać je wprost w zgodzie. Nie trenować modeli na danych użytkowników i ustawiać flagi no-training u dostawców. Kary RODO: do 20 mln EUR lub 4% obrotu.

## 4. Digital Services Act

[Rozporządzenie 2022/2065][dsa] stosuje się bezpośrednio od 17.02.2024 [z pamięci]. Obowiązki z rozporządzenia nie zależą od ustaw krajowych.

**Polska (stan na 13.11.2026).** Pierwotną ustawę wdrożeniową Prezydent zawetował 9.01.2026 ([MC](https://www.gov.pl/web/cyfryzacja/weto-prezydenta-oslabia-prawa-uzytkownikow-internetu)). Ministerstwo Cyfryzacji rozdzieliło materię na dwie ustawy:

- **Pierwsza:** ustawa z 4.09.2026 o zmianie ustawy o świadczeniu usług drogą elektroniczną oraz niektórych innych ustaw (Dz.U. 2026 poz. 1296), podpisana przez Prezydenta we wrześniu 2026. Wyznacza **Prezesa UKE na koordynatora ds. usług cyfrowych**; projekt przewidywał też kompetencje Prezesa UOKiK i Przewodniczącego KRRiT [zweryfikowane] ([Lege Artis](https://czasopismo.legeartis.org/2026/10/koordynator-spraw-uslug-cyfrowych-urzad-komunikacji-elektronicznej-rozporzadzenie-dsa/), [XYZ](https://xyz.pl/?p=254266), [Telepolis](https://www.telepolis.pl/wiadomosci/akt-o-uslugach-cyfrowych-ustawa-podpis-prezydenta), [Bankier](https://www.bankier.pl/wiadomosc/Prezes-UKE-pokieruje-nadzorem-nad-internetem-w-Polsce-Rzad-przyjal-przepisy-wdrazajace-unijne-DSA-9144676.html)). Jedno źródło podaje wejście w życie 6.11.2026 ([Money.pl](https://www.money.pl/gospodarka/polska-wprowadza-kluczowe-prawo-jest-podpis-prezydenta-7333268630714592a.html)) [niepewne co do daty].
- **Druga:** procedura nakazów blokowania treści nielegalnych, z odwołaniem i kontrolą sądową. Sejm przyjął poprawki Senatu i ustawa czekała na decyzję Prezydenta ([Tabletowo](https://www.tabletowo.pl/?p=1085620)). Podpis czy weto: [niepewne; wyniki wyszukiwania są sprzeczne].

Skutek praktyczny: organem, do którego użytkownik złoży skargę na platformę i który może prowadzić postępowanie, jest Prezes UKE; procedurę nakazów usunięcia treści trzeba będzie doprecyzować po rozstrzygnięciu losu drugiej ustawy.

| Poziom | Kiedy | Obowiązki | Zwolnienie mikro/małych |
|---|---|---|---|
| Każdy pośrednik | Od startu | Art. 11-12: punkty kontaktowe dla organów i użytkowników (nie wyłącznie bot). Art. 14: regulamin opisuje ograniczenia, moderację, użycie algorytmów, procedurę skarg. Art. 15: raport roczny | Tylko art. 15 |
| Hosting | Przechowujesz uploady i outputy | Art. 16: elektroniczny mechanizm zgłoszeń, potwierdzenie i decyzja. Art. 17: uzasadnienie każdej restrykcji (usunięcie, ograniczenie widoczności, zawieszenie konta). Art. 18: zawiadomienie organów o podejrzeniu przestępstwa zagrażającego życiu lub bezpieczeństwu | Brak |
| Platforma internetowa | Publiczna galeria, profile, feed | Art. 20-28: wewnętrzne odwołania, spory pozasądowe, zaufane podmioty sygnalizujące, zakaz dark patterns, przejrzystość rekomendacji, ochrona małoletnich | **Tak, art. 19** (poniżej 50 osób i 10 mln EUR obrotu), poza art. 24(3) |

- Wyłączenie odpowiedzialności hostingu (art. 6) chroni przy treściach "dostarczonych przez odbiorcę". Dla outputu wygenerowanego przez własny system ochrona jest wątpliwa, więc notice-and-takedown nie zastąpi moderacji proaktywnej [wnioskowanie] **[PRAWNIK]**. Dobrowolna moderacja nie odbiera ochrony (art. 7).
- [Rozporządzenie 2021/784][tco]: usunięcie treści terrorystycznych w ciągu 1 godziny od nakazu organu, bez progu wielkości firmy [z pamięci].
- Kary DSA: do 6% światowego obrotu.

## 5. Polityka treści i egzekwowanie

### 5.1 Obowiązki twarde

| Kategoria | Reguła | Wymagane działanie |
|---|---|---|
| CSAM | [K.k.][kk] art. 202, w tym § 4b: wytworzony albo przetworzony wizerunek małoletniego (do 2 lat). Posiadanie też jest przestępstwem | Blokada na wejściu i wyjściu, kwarantanna bez wglądu zespołu, zgłoszenie: Policja i [Dyżurnet.pl][dyzurnet]; dla USA [NCMEC CyberTipline][ncmec] ([18 U.S.C. 2258A][2258a]). Procedurę obsługi dowodów ustalić z karnistą **[PRAWNIK]** |
| NCII i seksualne deepfake'i | USA: [TAKE IT DOWN Act][tida] (podpisany 19.05.2025): usunięcie w **48 h** od ważnego zgłoszenia, także kopii; wymogi notice-and-removal obowiązują od 19.05.2026; egzekwuje FTC (naruszenie traktowane jak naruszenie reguły FTC, kara cywilna do 53 088 USD za naruszenie, portal skarg TakeItDown.ftc.gov, listy ostrzegawcze do platform w 05.2026; formalnej sprawy egzekucyjnej nie znalazłem) [zweryfikowane] ([FTC](https://www.ftc.gov/news-events/news/press-releases/2026/05/ftc-begins-enforcing-take-it-down-act), [Inside Privacy](https://www.insideprivacy.com/united-states/federal-trade-commission/the-take-it-down-acts-notice-and-removal-requirements-enter-into-effect/), [Orrick](https://www.orrick.com/en/Insights/2026/06/Nonconsensual-Intimate-Images-Online-Take-It-Down-Act-Enforcement-In-Full-Swing)). UE: od 2.12.2026 zakaz systemów AI generujących intymne treści bez zgody (AI Act art. 5 po Omnibusie, sekcja 2); [dyrektywa 2024/1385][vaw], transpozycja do 14.06.2027. UK: [Online Safety Act][osa] (kary do 18 mln GBP / 10%) i przestępstwo tworzenia intymnych deepfake'ów | Formularz NCII, kolejka z SLA 48 h, blokada re-uploadu po hashu. Stosowanie ustawy do firmy spoza USA obsługującej użytkowników z USA [wnioskowanie; wyszukiwanie z 13.11.2026 nie dało źródła, które to rozstrzyga] **[PRAWNIK US]** |
| Wizerunek osób | Pr. aut. art. 81, k.c. art. 23-24, k.k. art. 190a § 2 (podszywanie się); USA: stanowe prawa do wizerunku i głosu (np. ELVIS Act) | Tryby: "to ja" z weryfikacją, "mam zgodę" z oświadczeniem, blokada osób publicznych i małoletnich |
| Polityczne deepfake'i | AI Act art. 50(4); [rozporządzenie 2024/900][polad] o reklamie politycznej | Zakaz wprowadzających w błąd treści z realnymi politykami |
| Naruszenia IP | DSA art. 16; USA: DMCA § 512 (zarejestrowany agent, polityka recydywy) | Formularz IP, blokada promptów z nazwami postaci i marek w galerii |
| Klonowanie głosu | Dobra osobiste, RODO art. 9, regulaminy dostawców: wymagana świadoma zgoda osoby [zweryfikowane: R03] | Nagranie zgody z losową frazą + zgodność mówcy z próbką + log audytowy |

Kontekst egzekucyjny: po aferze Grok/X ze stycznia 2026 (masowe seksualizowane przeróbki zdjęć) Ofcom wszczął 12.01.2026 formalne dochodzenie wobec X, a 9.09.2026 uruchomił program egzekucyjny dotyczący NCII; seksualne deepfake'i AI są wśród jego priorytetów na 2026-27 [zweryfikowane] ([SCL](https://www.scl.org/ofcom-launches-investigation-into-x-over-grok-sexualised-imagery/), [Fieldfisher](https://www.fieldfisher.com/en/services/regulatory/public-regulatory-law-blog/intimate-image-abuse-ofcom-s-new-enforcement-programme-and-what-it-means-for-providers)). Postępowanie Komisji z DSA wobec X [z pamięci; nie sprawdzone]. W USA FTC rozesłała listy ostrzegawcze tuż po wejściu obowiązków TAKE IT DOWN, a UE dopisała generatory intymnych treści bez zgody do praktyk zakazanych. Regulatorzy traktują ten obszar priorytetowo.

### 5.2 Narzędzia

| Warstwa | Opcje | Uwagi |
|---|---|---|
| Filtry dostawców | Parametry typu `personGeneration`, `safety_tolerance`, `enable_safety_checker`; Veo w UE dopuszcza tylko dorosłych [zweryfikowane: R03] | Pierwsza linia, nie jedyna. Mapować błędy na statusy i automatyczny zwrot kredytów |
| Tekst promptu | [OpenAI Moderation][oaimod] (`omni-moderation-latest`, bezpłatne; tekst i obraz), [Azure AI Content Safety][azure], Llama Guard, ShieldGemma | OpenAI: obraz (URL lub base64, do 20 MB) jest oceniany tylko w 6 kategoriach: `violence`, `violence/graphic`, `self-harm`, `self-harm/intent`, `self-harm/instructions`, `sexual`. Pozostałe, w tym `sexual/minors`, działają wyłącznie dla tekstu i przy samym obrazie zwracają 0. Model jest bezpłatny; zmiany listy kategorii w 2026 nie znalazłem [zweryfikowane] ([OpenAI](https://community.openai.com/t/upgrading-the-moderation-api-with-a-new-multimodal-moderation-model/958187), [dokumentacja](https://developers.openai.com/api/docs/guides/moderation)). Nie jest to więc detektor CSAM w obrazie |
| Klasyfikator polityki | Tani LLM z rubryką: realna osoba z nazwiska, małoletni, seksualność, polityka, marka/postać | Zwraca etykiety strukturalne; decyzję podejmuje reguła, nie model |
| Obraz i wideo | [AWS Rekognition][rekog], [Hive][hive], [Sightengine][sight] (nagość, przemoc, detekcja małoletnich, symbole) | Wideo: próbkowanie klatek. Cenniki [niepewne], sprawdzić przed wyborem |
| CSAM | Potwierdzone w przebiegu z 13.11.2026 ([Thorn](https://www.thorn.org/solutions/for-platforms/), [Tech Coalition](https://technologycoalition.org/news/understanding-csam-detection/)): IWF Image Intercept (dopasowanie hashy dla kwalifikujących się małych firm i startupów, prosta integracja); [Thorn Safer][safer] w wariantach Safer Match (hashe) i Safer Enterprise (hashe + klasyfikator nowego CSAM w obrazie i wideo), dostępny także przez integrację z Hive; bezpłatny program Thorn Pathways dla startupów; [wytyczne CSAM OpenAI dla deweloperów](https://developers.openai.com/api/docs/guides/csam-guidance). Bez potwierdzenia [z pamięci]: [PhotoDNA Cloud][photodna] (bezpłatne dla zakwalifikowanych), [Cloudflare CSAM Scanning Tool][cfcsam], Google Content Safety API | Hashe wykrywają tylko znany materiał w uploadach; branża łączy je z klasyfikatorami [zweryfikowane]. Dla nowych generacji potrzebny klasyfikator nagość + wiek oraz twarda reguła promptu. Cennik Safer i warunki dostępu do PhotoDNA, Cloudflare i Google [niepewne]: zapytać dostawców przed wyborem |
| Głos | Weryfikacja zgody u dostawcy (np. [ElevenLabs][elsafety]) lub własna: fraza losowa + porównanie mówcy | Porównanie mówcy to biometria: wyraźna zgoda |

Nie budować własnego rozpoznawania twarzy osób publicznych: to przetwarzanie biometryczne osób, które nie wyraziły zgody. Blokować po nazwiskach w prompcie i polegać na filtrach dostawców [wnioskowanie].

### 5.3 Pipeline warstwowy [wnioskowanie]

1. **Bramka konta:** 18+, weryfikacja e-mail, limity, odcisk karty przed funkcjami wizerunku i głosu.
2. **Prompt:** lista blokad, moderacja tekstu, klasyfikator polityki. Wynik: allow / block / allow-private (zakaz publikacji).
3. **Media wejściowe:** hash CSAM, klasyfikator NSFW i wieku, detekcja obecności twarzy uruchamiająca ścieżkę zgody.
4. **Dostawca:** jego filtry; status `blocked_stage` i zwrot kredytów.
5. **Output:** klasyfikator obrazu/klatek; dla audio transkrypcja i moderacja tekstu.
6. **Publikacja w galerii:** ostrzejsze progi, obowiązkowa etykieta AI, kolejka ręczna dla flag. Na starcie pre-moderacja zamiast post-moderacji.
7. **Po publikacji:** przycisk zgłoszenia (DSA art. 16), osobne formularze NCII, IP i wizerunku, SLA 48 h.
8. **Egzekwowanie:** system ostrzeżeń, uzasadnienie decyzji (art. 17), odwołanie do człowieka (także RODO art. 22), dziennik audytowy.

### 5.4 Operatorzy płatności i sklepy z aplikacjami

- Stripe: lista [restricted businesses](https://stripe.com/legal/restricted-businesses) zakazuje pornografii i innych treści dla dorosłych "zaprojektowanych w celu gratyfikacji seksualnej" i wprost obejmuje "wszelkie treści generowane przez sztuczną inteligencję", które spełniają te kryteria [zweryfikowane na podstawie kopii listy] ([ConductAtlas](https://conductatlas.com/platform/stripe/stripe-restricted-businesses-list/provision/CA-P-065458/ai-generated-adult-content-prohibited/)). Osobnego zapisu o "nudify", deepfake'ach lub treściach bez zgody wyszukiwarka w liście Stripe nie znalazła [niepewne]. Egzekwowanie bywa nierówne: 404 Media opisywało obsługę płatności dla serwisów z generowaną pornografią mimo zakazu ([404 Media](https://www.404media.co/stripe-forbids-sex-work-but-profits-from-non-consensual-porn/)); nie zmienia to ryzyka zamknięcia konta.
- Paddle, Polar i Creem dodatkowo zakazują face swap, deepfake'ów i klonowania głosu [zweryfikowane: R04]. Jedno źródło wtórne podaje, że Paddle zakazuje wprost generatorów obrazów AI ([Freemius](https://freemius.com/blog/payment-platform-restrictions-ai-apps/)) [niepewne; to samo źródło myli się co do Stripe, więc sprawdzić aktualną politykę Paddle przed wyborem operatora].
- Polityka "zero NSFW" jest warunkiem istnienia rachunku płatniczego.
- [Apple App Store][apple] (wytyczne 1.1 i 1.2: filtr, zgłaszanie, blokowanie, kontakt dla aplikacji z UGC) i [Google Play][gplay] (polityka treści generowanych przez AI: zgłaszanie w aplikacji, zakaz deepfake'ów seksualnych i wprowadzających w błąd) [z pamięci]. Dotyczy dopiero aplikacji mobilnej.

## 6. Proweniencja

| Warstwa | Status prawny | Realizacja |
|---|---|---|
| Oznaczenie maszynowe outputu | **Wymagane** (AI Act art. 50(2)) | Manifest [C2PA][c2pa] z `digitalSourceType = trainedAlgorithmicMedia`, biblioteki [CAI][cai]; pole IPTC w XMP |
| Niewidoczny znak wodny | Kodeks nie narzuca techniki, ale według omówień jedna warstwa nie wystarczy (sekcja 2 tego raportu) [zweryfikowane co do zasady] | Otwarte: [TrustMark][trustmark] (obraz), [Video Seal][videoseal] (wideo), [AudioSeal][audioseal] (audio) [z pamięci; bez weryfikacji 13.11.2026]. [SynthID][synthid] osadzają dostawcy we własnych outputach: Google, a od 2026 także OpenAI w obrazach z ChatGPT i API, obok C2PA [zweryfikowane] ([OpenAI](https://developers.openai.com/api/docs/guides/content-provenance), [C2PA Viewer](https://c2paviewer.com/articles/openai-google-c2pa-synthid-2026)). Nie da się go nałożyć na cudze treści [z pamięci] |
| Odciski i logi | Oczekiwane jako uzupełnienie | Hash percepcyjny + rekord generacji; publiczny endpoint "czy to powstało u nas" jako narzędzie detekcji |
| Widoczna etykieta | **Wymagana** dla deepfake'ów przy publikacji (deployer, art. 50(4)) | Znaczek "AI" na każdej pracy w galerii i w podglądzie udostępniania. Kodeks z 10.06.2026 daje trzy gotowe ikony UE (w pełni wygenerowane, zmodyfikowane, podstawowa z interaktywną drugą warstwą) [zweryfikowane; źródła w sekcji 2 tego raportu]: użyć ich zamiast własnego znaczka |
| Widoczny znak wodny na planie free | Niewymagany | Decyzja handlowa |

Pułapki [wnioskowanie]: transkodowanie (`ffmpeg`, `sharp`) domyślnie usuwa metadane, więc C2PA od dostawcy (np. OpenAI, Google) trzeba zachować albo podpisać ponownie. Manifest podpisany certyfikatem spoza listy zaufania C2PA wyświetli się jako "nieznane źródło". Kalifornijska [SB 942][sb942] (od 2.08.2026) obejmuje dostawców z ponad 1 mln użytkowników miesięcznie i wymaga ukrytego oznaczenia oraz darmowego detektora [z pamięci].

**Co faktycznie przychodzi w plikach od dostawców** (testy niezależne z 2026; źródła wtórne, sprawdzić własnym testem przed startem) [zweryfikowane] ([Leaxor](https://leaxor.com/blog/ai-content-labels-study-2026), [Layer3 Labs](https://www.layer3labs.io/comparisons/which-ai-models-watermark-their-output), [OpenAI](https://developers.openai.com/api/docs/guides/content-provenance)):

| Dostawca | Stan oznaczeń w outputach z API |
|---|---|
| OpenAI (obrazy) | C2PA + SynthID; OpenAI udostępnia też sprawdzanie proweniencji (C2PA w obrazach, SynthID w obrazach i audio) |
| OpenAI Sora | W standardowych pobraniach manifesty C2PA bywały nieobecne lub nieczytelne |
| Google Veo | SynthID w całym wideo; pliki Veo 3.1 i 3.1 Fast dostarczone przez fal miały manifest C2PA podpisany przez Google |
| Kling (v3, v3 Pro, O3 Pro, 2.6 Pro, 1.6 Elements) | Brak manifestu C2PA; benchmark z 04.2026 ocenił Kling jako niezgodny (brak opublikowanego oznaczenia maszynowego) |
| ByteDance Seedance | Pliki z API bez etykiety C2PA; ByteDance deklaruje C2PA dla outputów tworzonych w CapCut |

W jednym z testów bezstratne skopiowanie pliku bez zmiany pikseli usunęło obecne etykiety. Wniosek [wnioskowanie]: oznaczenie nakładamy sami na wyjściu własnego pipeline'u, jednolicie dla każdego modelu (manifest C2PA + niewidoczny znak wodny + rekord w rejestrze), a oznaczenia dostawcy traktujemy jako dodatek, nie podstawę zgodności.

## 7. IP w outputach i ryzyko upstream

- **Ochrona outputów.** USA: wymóg ludzkiego autorstwa; sam prompt nie wystarcza (raport [US Copyright Office][usco] z 29.01.2025; Thaler v. Perlmutter, D.C. Cir. 03.2025) [z pamięci]. UE i Polska: utwór wymaga twórczości człowieka; brak rozstrzygnięcia TSUE [z pamięci]. Regulamin może przenieść na użytkownika "wszelkie prawa, jakie przysługują", ale nie może gwarantować praw autorskich ani wyłączności [wnioskowanie].
- **Prawa komercyjne** zależą od modelu i planu; fal zastrzega, że output jest "na wyłączne ryzyko klienta", Replicate odsyła do licencji modelu, ElevenLabs dopuszcza użycie komercyjne na planach płatnych [zweryfikowane: R03]. Potrzebna macierz "model → dozwolone użycie", pokazywana użytkownikowi.
- **Indemnifikacje** (OpenAI Copyright Shield, [Google Cloud][gindem], Microsoft, Adobe) obowiązują przy umowach bezpośrednich i pod warunkami; przez agregator zwykle nie przechodzą. Kling nie daje indemnifikacji [zweryfikowane: R03]. Reseller jest pierwszym pozwanym [wnioskowanie].
- **Spory** (stan na 13.11.2026):
  - **Disney i Universal v. Midjourney** (C.D. Cal., 06.2025): w 11.2025 połączona z pozwem Warner Bros. Discovery z 09.2025. W 2026 trwa discovery (m.in. żądanie Midjourney, by studia ujawniły własne użycie AI, 07.2026); mediacja miała się zakończyć do 19.08.2026, posiedzenie statusowe 31.08.2026 [jedno źródło]. Nie znalazłem wyroku, summary judgment ani terminu rozprawy; Midjourney broni się fair use [zweryfikowane] ([Graphic Policy](https://graphicpolicy.com/2026/05/11/disney-warner-bros-universal-and-midjourney-discovery-dispute/), [The Art Newspaper](https://www.theartnewspaper.com/2026/07/09/midjourney-demands-hollywood-AI-secrets)).
  - **Disney, Universal i Warner Bros. Discovery v. MiniMax (Hailuo)**, C.D. Cal. nr 2:25-cv-08768 (pozew 09.2025; zarzuty obejmują także wyświetlanie outputów w galerii serwisu [z pamięci]): sąd **oddalił wniosek MiniMax o odrzucenie pozwu** (Reuters, 26.05.2026). Uznał jurysdykcję, bo aplikacja Hailuo jest oferowana w USA, i stwierdził, że pozew "wyraźnie przedstawia wiarygodne zarzuty" naruszenia; sprawa przeszła do discovery [zweryfikowane] ([Let's Data Science](https://letsdatascience.com/news/minimax-loses-bid-to-dismiss-disney-copyright-suit-755f915a), [MLex](https://www.mlex.com/mlex/artificial-intelligence/articles/2464661/minimax-nanonoble-move-to-dismiss-studios-us-copyright-case)).
  - **Getty v. Stability AI** (High Court, 4.11.2025: Getty przegrało w głównej części): 16.12.2025 Getty uzyskało zgodę na apelację w zakresie wtórnego naruszenia (czy model AI może być "infringing copy"). Apelacja w toku; wyroku Court of Appeal nie znalazłem [zweryfikowane] ([Taylor Wessing](https://www.taylorwessing.com/de/insights-and-events/insights/2026/01/next-steps-for-getty-v-stability-why-has-permission-to-appeal-been-granted), [IPKat](https://ipkitten.blogspot.com/2026/01/permission-to-appeal-granted-in-getty.html?m=0)).
  - **Seedance 2.0 (ByteDance):** wezwania do zaniechania od Disneya i Paramount (15.02.2026) oraz stanowisko MPA (12.02.2026) o masowym nieuprawnionym użyciu utworów. Pozwu nie znalazłem [zweryfikowane co do wezwań; stan po 02.2026 niepewny] ([TheWrap](https://thewrap.com/industry-news/public-policy-legal/disney-bytedance-seedance-cease-and-desist/)).
  - Bez weryfikacji [z pamięci]: GEMA v. OpenAI (LG München I, 11.11.2025: zapamiętanie tekstów w modelu to zwielokrotnienie); umowa licencyjna Disney-OpenAI (12.2025).
  - Wniosek z orzeczenia w sprawie MiniMax [wnioskowanie]: siedziba poza USA nie chroni przed jurysdykcją sądu amerykańskiego, jeśli usługa jest oferowana użytkownikom w USA. Dotyczy to także polskiego resellera.
- **Skutki dla resellera** [wnioskowanie]: (1) model może zniknąć lub zaostrzyć filtry z dnia na dzień, więc warstwa abstrakcji dostawców i klauzula o zmianie katalogu są obowiązkowe; (2) galeria nie może eksponować cudzych postaci, logo ani celebrytów; (3) presety nie mogą nosić nazw artystów ani marek; (4) regulamin: oświadczenia użytkownika, indemnifikacja przez użytkownika B2B, limit odpowiedzialności w granicach prawa konsumenckiego.

## 8. Prawo konsumenckie i gospodarcze (Polska / UE)

| Temat | Wymóg | Status |
|---|---|---|
| Regulamin | Obowiązkowy, udostępniony przed zawarciem umowy: zakres usług, wymagania techniczne, zakaz treści bezprawnych, zawarcie i rozwiązanie umowy, reklamacje ([UŚUDE][usude] art. 8) + elementy DSA art. 14 | [z pamięci] |
| Checkout | Informacje przedumowne (art. 12), przycisk "zamówienie z obowiązkiem zapłaty" (art. 17 [ustawy o prawach konsumenta][upk]), potwierdzenie na trwałym nośniku | [z pamięci] |
| Odstąpienie 14 dni | Generator SaaS to raczej "usługa cyfrowa" niż "treść cyfrowa". Zebrać niezaznaczony domyślnie checkbox z żądaniem natychmiastowego rozpoczęcia. Przy odstąpieniu konsument płaci proporcjonalnie za wykorzystaną część (art. 35); bez żądania nie płaci nic (art. 36). Utrata prawa dopiero po pełnym wykonaniu (art. 38 ust. 1 pkt 1; pkt 13 dla treści cyfrowych). Dotyczy też JDG "na prawach konsumenta" (art. 7aa) | Kwalifikacja kredytów [wnioskowanie] **[PRAWNIK]** |
| Funkcja odstąpienia online | [Dyrektywa 2023/2673][dir2673] dodaje art. 11a: łatwo dostępna funkcja odstąpienia w interfejsie, stosowana od 19.06.2026 | [z pamięci]; polska transpozycja [niepewne] |
| Zmiany usługi i cen | Zmiana usługi cyfrowej tylko z przyczyn wskazanych w umowie, z uprzedzeniem i prawem wypowiedzenia (rozdz. 5b, wdrożenie [dyrektywy 2019/770][dir770]). UOKiK kwestionuje podwyżki subskrypcji bez wyraźnej zgody. Anulowanie tak łatwe jak zakup | [z pamięci]; praktyka UOKiK [niepewne] |
| Promocje | Przy każdej obniżce pokazać najniższą cenę z 30 dni przed obniżką; dotyczy też usług ([ustawa o cenach][ceny] art. 4). Ceny dla konsumentów brutto. "Unlimited" z limitem fair use i fałszywe liczniki to nieuczciwe praktyki | [z pamięci] |
| Inne | Platforma ODR zamknięta 20.07.2025 (nie linkować). Zakaz dyskryminacji klientów z UE ([geoblocking][geo]). Wymogi dostępności (EAA) nie obejmują mikroprzedsiębiorstw usługowych | [z pamięci] |
| VAT | OSS powyżej 10 000 EUR sprzedaży B2C do UE; UK poza OSS; status czynnego podatnika od początku [zweryfikowane: R04]. Dwa dowody lokalizacji klienta; B2B UE z walidacją VIES | [z pamięci] |
| KSeF | Obowiązkowy od 1.02.2026 (duzi) i 1.04.2026 (pozostali), najmniejsi od 1.01.2027; faktury konsumenckie dobrowolne; faktury w procedurze OSS poza KSeF ([KSeF][ksef]) | [z pamięci]; stan na 11.2026 [niepewne], potwierdzić z księgowym |
| Forma prawna | JDG: odpowiedzialność całym majątkiem osobistym. Sp. z o.o. ([k.s.h.][ksh]): kapitał 5 000 zł, rejestracja S24, pełna księgowość, CIT 9% dla małych podatników; zarząd odpowiada osobiście w przypadkach z art. 299 k.s.h. i art. 116 Ordynacji podatkowej; jedyny wspólnik płaci ZUS | [z pamięci]; podatki **[doradca podatkowy]** |

Rekomendacja [wnioskowanie]: prototyp i zamknięta beta mogą działać na JDG; przed publicznym startem z płatnościami i galerią przenieść działalność do sp. z o.o. i wykupić ubezpieczenie OC (cyber + media/IP). Profil ryzyka (deepfake'i, IP, RODO, roszczenia z USA) nie pasuje do odpowiedzialności osobistej.

## 9. Compliance checklist

**A. Przed publicznym startem**

1. Badanie znaku i domeny; przegląd "czystości" repo (zero cudzych tekstów, mediów, promptów, nazw).
2. Spółka, status VAT czynny, OSS, księgowość z KSeF dla faktur B2B.
3. Regulamin (UŚUDE art. 8 + DSA art. 14), polityka treści, polityka prywatności, baner cookies.
4. Checkout: przycisk z obowiązkiem zapłaty, checkbox natychmiastowego świadczenia, potwierdzenie e-mail, funkcja odstąpienia, anulowanie subskrypcji online, logika najniższej ceny z 30 dni.
5. Umowy powierzenia i lista podprocesorów, rejestr czynności, procedura naruszeń (72 h), realizacja praw osób, harmonogram retencji.
6. Moderacja: warstwy 1-5 z sekcji 5.3, zero NSFW, twarde reguły dla małoletnich, mapowanie błędów dostawców i zwroty.
7. Art. 50 AI Act: oznaczenie maszynowe każdego outputu (C2PA + znak wodny), rejestr generacji, informacja o AI w interfejsie.
8. DSA hosting: punkty kontaktowe, formularz zgłoszeń, szablon uzasadnienia decyzji, kontakt alarmowy dla nakazów (1 h).
9. Procedura CSAM uzgodniona z prawnikiem; formularz NCII z SLA 48 h (nawet bez galerii, jeśli są linki udostępniania).
10. Macierz praw do outputu per model; usługa 18+.

**B. Przed funkcjami społeczności (galeria, profile, feed)**

1. Pre-moderacja publikacji i kolejka ręczna; etykieta AI na każdej pracy.
2. Zgłaszanie w każdym widoku, blokowanie użytkowników, system ostrzeżeń, odwołania.
3. Formularze IP (w tym agent DMCA) i wizerunku; blokada postaci, marek, celebrytów i polityków w treściach publicznych.
4. Decyzja o UK: blokada geograficzna albo ocena ryzyka wymagana przez Online Safety Act.
5. Monitorowanie progu "małego przedsiębiorstwa" (po jego przekroczeniu sekcja 3 DSA); przejrzystość rankingu feedu.

**C. Przed klonowaniem głosu lub wizerunku**

1. DPIA i opinia prawnika o art. 9 RODO.
2. Osobny ekran wyraźnej zgody biometrycznej, wycofanie zgody kasujące model, polityka retencji biometrii (także pod BIPA).
3. Weryfikacja: głos przez frazę losową i zgodność mówcy; wizerunek w trybie "to ja" przez selfie na żywo albo oświadczenie o zgodzie z logiem.
4. Trasy wyłącznie do dostawców z DPA i transferem do USA/UE; żadnych tras "CN" dla twarzy bez wyraźnej informacji.
5. Blokada osób publicznych i małoletnich; kanał dla osób przedstawionych bez konta.
6. Tylko konta płatne z historią; dzienne limity; pełny dziennik audytowy.
7. Ponowne sprawdzenie regulaminu operatora płatności.

**D. Później**

Certyfikat z listy zaufania C2PA i przystąpienie do kodeksu postępowania; raporty przejrzystości i pełna sekcja 3 DSA po wyjściu z progu; IOD (DPO); przedstawiciel w UK; aplikacje mobilne i zasady sklepów; umowy bezpośrednie z indemnifikacją; śledzenie: Digital Omnibus (część RODO), Digital Fairness Act, rozporządzenie CSAM, przekształcona dyrektywa o wykorzystywaniu dzieci, NO FAKES Act [wszystko niepewne co do stanu].

## 10. Gdzie potrzebny prawnik

Regulamin i ścieżki konsumenckie (PL); zgody biometryczne i DPIA; kwalifikacja z art. 50 i art. 6 DSA dla outputów; procedura CSAM (karnista); badanie znaku (rzecznik patentowy); ekspozycja w USA: TAKE IT DOWN, BIPA, DMCA, klauzula arbitrażowa (prawnik US); VAT, KSeF i forma prawna (doradca podatkowy).

## Źródła

Źródła pierwotne poniżej **nie zostały pobrane w tej sesji** (blokada sieci). Są to adresy, pod którymi należy zweryfikować twierdzenia oznaczone [z pamięci] i [niepewne]. Twierdzenia [zweryfikowane: R0x] mają źródła w raportach `01-mapa-produktu-higgsfield.md`, `03-dostawcy-modeli-i-api.md`, `04-ekonomia-cennik-platnosci.md`.

- UE: [AI Act 2024/1689][aia], [Digital Omnibus AI][omnibus], [kodeks oznaczania treści AI][cop], [RODO 2016/679][gdpr], [DSA 2022/2065][dsa], [TCO 2021/784][tco], [dyrektywa 2006/114][dir114], [EUTMR 2017/1001][eutmr], [dyrektywa 2019/770][dir770], [dyrektywa 2023/2673][dir2673], [dyrektywa 2024/1385][vaw], [rozporządzenie 2024/900][polad], [geoblocking 2018/302][geo], [C-406/10][sas], [Data Privacy Framework][dpf]
- Polska: [UZNK][uznk], [prawo autorskie][pa], [kodeks karny][kk], [ustawa o prawach konsumenta][upk], [UŚUDE][usude], [ustawa o informowaniu o cenach][ceny], [PKE][pke], [k.s.h.][ksh], [wykaz DPIA UODO][dpia], [KSeF][ksef], [Dyżurnet.pl][dyzurnet]
- USA / UK: [TAKE IT DOWN Act][tida], [18 U.S.C. 2258A][2258a], [NCMEC][ncmec], [BIPA][bipa], [SB 942][sb942], [US Copyright Office - AI][usco], [Online Safety Act][osa]
- Narzędzia: [OpenAI Moderation][oaimod], [Azure AI Content Safety][azure], [AWS Rekognition][rekog], [Hive][hive], [Sightengine][sight], [PhotoDNA][photodna], [Cloudflare CSAM Scanning][cfcsam], [Thorn Safer][safer], [ElevenLabs Safety][elsafety], [C2PA][c2pa], [CAI open source][cai], [TrustMark][trustmark], [Video Seal][videoseal], [AudioSeal][audioseal], [SynthID][synthid], [Google indemnified services][gindem], [Apple Review Guidelines][apple], [Google Play Policy][gplay]

[aia]: https://eur-lex.europa.eu/eli/reg/2024/1689/oj
[omnibus]: https://digital-strategy.ec.europa.eu/en/library/digital-omnibus-ai-regulation-proposal
[cop]: https://digital-strategy.ec.europa.eu/en/policies/code-practice-ai-generated-content
[gdpr]: https://eur-lex.europa.eu/eli/reg/2016/679/oj
[dsa]: https://eur-lex.europa.eu/eli/reg/2022/2065/oj
[tco]: https://eur-lex.europa.eu/eli/reg/2021/784/oj
[dir114]: https://eur-lex.europa.eu/eli/dir/2006/114/oj
[eutmr]: https://eur-lex.europa.eu/eli/reg/2017/1001/oj
[dir770]: https://eur-lex.europa.eu/eli/dir/2019/770/oj
[dir2673]: https://eur-lex.europa.eu/eli/dir/2023/2673/oj
[vaw]: https://eur-lex.europa.eu/eli/dir/2024/1385/oj
[polad]: https://eur-lex.europa.eu/eli/reg/2024/900/oj
[geo]: https://eur-lex.europa.eu/eli/reg/2018/302/oj
[sas]: https://curia.europa.eu/juris/liste.jsf?num=C-406/10
[dpf]: https://www.dataprivacyframework.gov/
[uznk]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU19930470211
[pa]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU19940240083
[kk]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU19970880553
[upk]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU20140000827
[usude]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU20021441204
[ceny]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU20140000915
[pke]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU20240001221
[ksh]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WDU20000941037
[dpia]: https://isap.sejm.gov.pl/isap.nsf/DocDetails.xsp?id=WMP20190000666
[ksef]: https://ksef.podatki.gov.pl/
[dyzurnet]: https://dyzurnet.pl/
[tida]: https://www.congress.gov/bill/119th-congress/senate-bill/146
[2258a]: https://www.law.cornell.edu/uscode/text/18/2258A
[ncmec]: https://www.missingkids.org/gethelpnow/cybertipline
[bipa]: https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=3004
[sb942]: https://leginfo.legislature.ca.gov/faces/billNavClient.xhtml?bill_id=202320240SB942
[usco]: https://www.copyright.gov/ai/
[osa]: https://www.legislation.gov.uk/ukpga/2023/50
[oaimod]: https://platform.openai.com/docs/guides/moderation
[azure]: https://learn.microsoft.com/azure/ai-services/content-safety/
[rekog]: https://docs.aws.amazon.com/rekognition/latest/dg/moderation.html
[hive]: https://thehive.ai/
[sight]: https://sightengine.com/
[photodna]: https://www.microsoft.com/en-us/photodna
[cfcsam]: https://developers.cloudflare.com/cache/reference/csam-scanning/
[safer]: https://safer.io/
[elsafety]: https://elevenlabs.io/safety
[c2pa]: https://c2pa.org/
[cai]: https://opensource.contentauthenticity.org/
[trustmark]: https://github.com/adobe/trustmark
[videoseal]: https://github.com/facebookresearch/videoseal
[audioseal]: https://github.com/facebookresearch/audioseal
[synthid]: https://deepmind.google/technologies/synthid/
[gindem]: https://cloud.google.com/terms/generative-ai-indemnified-services
[apple]: https://developer.apple.com/app-store/review/guidelines/
[gplay]: https://play.google/developer-content-policy/
