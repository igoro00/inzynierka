# Kontekst sesji — przekazanie pracy do Claude Code

Ten plik zawiera pełny stan prac z poprzedniej sesji czatu, tak aby **Claude Code** mógł płynnie przejąć zadanie bez utraty kontekstu, ustaleń badawczych i reguł językowych.

---

## 1. Zadanie zlecone przez użytkownika

1. **Oficjalny, zgłoszony temat pracy inżynierskiej (FTIMS Politechnika Łódzka, Informatyka Stosowana):**
   > *Weryfikacja skuteczności agenta przeglądarkowego Google Antigravity przy realizacji zadań w systemach biurowych*

2. **Polecenie prowadzącego / cel bieżącego etapu:**
   > *„Przedstaw projekt własnego rozwiązania w kontekście innych istniejących rozwiązań i analizy literatury.”*

3. **Zadanie techniczne:**
   Rozpoczęcie uzupełniania oficjalnego wzorca pracy inżynierskiej w katalogu `formatka_inz_ftims_2024/` w oparciu o ustalenia projektowe zapisane w `AGENTS.md` oraz `zakres.md`.

---

## 2. Obowiązujące reguły projektowe i językowe (BARDZO WAŻNE)

Przed jakąkolwiek edycją przeczytaj w całości plik `AGENTS.md` oraz `zakres.md`. Obowiązują dwie nadrzędne zasady:

1. **Aktualizacja `AGENTS.md`:** Za każdym razem, gdy użytkownik zmienia założenia projektu, podejmuje nowe decyzje architektoniczne/technologiczne lub modyfikuje koncepcję, należy od razu zaktualizować `AGENTS.md`.
2. **Formalna polszczyzna akademicka (zakaz anglicyzmów i kolokwializmów w pracy):**
   W formalnych dokumentach pracy (`zakres.md` oraz wszystkich plikach `.tex` w `formatka_inz_ftims_2024/`) **nie wolno** używać:
   - anglicyzmów takich jak: *benchmark*, *webowy*, *walidacja*, *ewaluacja*, *dashboard*, *frontend*, *backend*, *framework*, *offline/online*, *pipeline*, *use case*, *feedback*,
   - kolokwializmów takich jak: *ułatwiają pracę*, *zawodzą*, *żmudne*.
   Stosuj wyłącznie polskie odpowiedniki akademickie: *zestaw testów porównawczych* / *środowisko badawcze*, *internetowy*, *weryfikacja*, *ocena*, *panel administracyjny*, *warstwa prezentacji / część kliencka*, *warstwa danych / część serwerowa*, *zapisane migawki*, *przebieg*, itd. Angielskie terminy podawaj wyłącznie w nawiasie przy pierwszym wprowadzeniu pojęcia jako `(ang. \textit{...})`.

Kluczowe założenia merytoryczne projektu (z `AGENTS.md`):
- **Nie budujemy własnego agenta** (żadnego własnego potoku Playwright → DOM → LLM → Playwright) ani **nie piszemy aplikacji biurowej od zera**.
- Testujemy wyłącznie gotowego agenta przeglądarkowego w środowisku **Google Antigravity** (wywoływanego poleceniem `/browser`), traktowanego jako „czarna skrzynka”, z możliwością zmiany modelu językowego.
- Badane aplikacje to istniejące, **otwartoźródłowe aplikacje biurowe typu panel administracyjny** (wstępnie wytypowane do pierwszego etapu: `react-admin` — *Posters Galore* oraz `refine` — *finefoods-antd*; rozważany dalej: `Twenty`).
- **Odwrócenie perspektywy badawczej:** zmienną eksperymentu jest **interfejs aplikacji** (wariant bazowy vs wariant przyjazny agentom / warianty pośrednie), przy identycznej warstwie danych, stanie początkowym i treści polecenia.
- **Obiektywna weryfikacja stanu po stronie serwera/bazy danych** ($S_0 \to S_1$) rozszerzona o kontrolę niezamierzonych skutków ubocznych oraz rejestrację fałszywych deklaracji sukcesu agenta.
- **Bezpieczny główny cel inżynierski:** zaprojektowanie i implementacja rzetelnego środowiska i zestawu testów porównawczych (niezależnie od tego, jak duży wzrost skuteczności przyniosą modyfikacje interfejsu).

---

## 3. Co zostało już wykonane w tej sesji

Sesja została przerwana tuż po wygenerowaniu i oczyszczeniu głównych rozdziałów, jeszcze przed napisaniem podsumowującej odpowiedzi dla użytkownika oraz przed uzupełnieniem `cel_i_zakres.tex` i wygenerowaniem finalnego `main.pdf`.

 Stan zmodyfikowanych plików:

1. **`AGENTS.md`**
   - Zaktualizowano sekcję `## 3. Tematyka pracy` o oficjalny, zgłoszony tytuł pracy (11 słów).

2. **`formatka_inz_ftims_2024/titlepage.tex`**
   - Wstawiono oficjalny tytuł pracy: *„Weryfikacja skuteczności agenta przeglądarkowego Google Antigravity przy realizacji zadań w~systemach biurowych”*.
   - Pozostałe pola strony tytułowej (`Imię i Nazwisko`, `Nr albumu`, `Promotor`, `ŁÓDŹ <tylko rok>`) czekają na dane od użytkownika.

3. **`formatka_inz_ftims_2024/main.tex`**
   - Dodano pakiety potrzebne do tabel i schematów: `xcolor`, `booktabs`, `array`, `tabularx`, `tikz` (`\usetikzlibrary{positioning,arrows.meta,fit,backgrounds}`).
   - Dodano mapowanie polskich znaków diakrytycznych UTF-8 (`literate`) w `\lstset`, dzięki czemu polskie znaki w otoczeniach `lstlisting` kompilują się w `pdflatex` bez błędów.
   - Uzupełniono sekcję `\section*{Wyjaśnienie skrótów używanych w pracy}` (API, ARIA, AWI, CRM, DOM, HTML, HTTP, LLM, MCP, TSR, W3C, WCAG).

4. **`formatka_inz_ftims_2024/rozdzial1.tex` — napisany w całości**
   - **Rozdział 1: „Przegląd literatury i istniejących rozwiązań”** (`\label{chap:pierwszy}`):
     - `1.1 Podstawowe pojęcia` — agent, LLM, model multimodalny, agent przeglądarkowy (pętla ReAct), przeglądarka agentowa, zadanie, TSR, dostępność cyfrowa i dostępność dla agentów.
     - `1.2 Agenci przeglądarkowi oparci na dużych modelach językowych` — rozwój badań (World of Bits / MiniWoB++, WebShop, Mind2Web, WebVoyager, SeeAct i problem ugruntowania, AgentOccam jako dowód znaczenia reprezentacji strony), komercyjne przeglądarki agentowe (Anthropic Computer Use, OpenAI Operator/CUA, Project Mariner, Gemini 2.5 Computer Use) oraz podrozdział `1.2.3 Agent przeglądarkowy w środowisku Google Antigravity` (architektura `/browser`, odrębny profil Chrome, rejestracja sesji, uzasadnienie traktowania jako czarna skrzynka).
     - `1.3 Reprezentacje strony internetowej wykorzystywane przez agentów` — drzewo DOM, drzewo dostępności (rola, dostępna nazwa, stan, wartość; WCAG/WAI-ARIA/AccName), zrzuty ekranu i Set-of-Mark, reprezentacje hybrydowe (BrowserGym) + tabela porównawcza `tab:reprezentacje`.
     - `1.4 Dostępność cyfrowa a dostępność dla agentów` — kryteria WCAG 2.2 (1.3.1, 2.4.6, 3.3.2, 4.1.2, 4.1.3), WAI-ARIA 1.2, statystyki WebAIM Million 2025 (94,8% stron z błędami, średnio 1257 elementów DOM na stronę), Europejski Akt o Dostępności (dyrektywa UE 2019/882), związek z automatycznym testowaniem (Testing Library, Playwright), koncepcja AWI (*„Build the web for agents, not agents for the web”*, Lù i in. 2025) oraz propozycja W3C WebMCP i MCP.
     - `1.5 Istniejące zestawy testów porównawczych i środowiska badawcze` — krytyczna analiza MiniWoB++, WebShop, Mind2Web i Online-Mind2Web (*„An Illusion of Progress?”*), WebArena i VisualWebArena, WorkArena i BrowserGym, WebVoyager, WebSuite, BrowseComp i BrowseComp-Plus, OSWorld.
     - `1.6 Metody weryfikacji poprawności wykonania zadań` — 4 metody oceny i problem rozbieżności między deklaracją agenta a rzeczywistym stanem danych.
     - `1.7 Zestawienie istniejących rozwiązań i luka badawcza` — przekrojowa tabela porównawcza `tab:porownanie` (zestawiająca 9 rozwiązań z rozwiązaniem proponowanym) oraz 5 wniosków definiujących lukę badawczą.
   - Tekst zweryfikowany pod kątem braku anglicyzmów.

5. **`formatka_inz_ftims_2024/rozdzial2.tex` — napisany w całości (część projektowa)**
   - **Rozdział 2: „Projekt środowiska badawczego”** (`\label{chap:drugi}`), odpowiadający wprost na polecenie prowadzącego:
     - `2.1 Założenia projektowe na tle istniejących rozwiązań` — odwrócenie perspektywy, decyzje ograniczające oraz tabela `tab:inspiracje` pokazująca, które elementy przejęto i zaadaptowano z WebArena, WorkArena, WebSuite, BrowseComp-Plus, WCAG/WAI-ARIA oraz AWI.
     - `2.2 Wymagania` — wymagania funkcjonalne `WF-01`..`WF-06` i niefunkcjonalne `WN-01`..`WN-06` (w tym `WN-03`: nieujawnianie wariantu agentowi w URL ani tytule strony oraz `WN-06`: wierność wariantu bazowego bez sztucznego psucia).
     - `2.3 Architektura rozwiązania` — diagram komponentów w TikZ (`fig:architektura`) dzielący architekturę na elementy widoczne dla agenta i elementy wspierające badanie, opis modułów, konteneryzacja (Docker).
     - `2.4 Wybór aplikacji biurowych` — 6 kryteriów wyboru, tabela porównawcza 6 projektów otwartoźródłowych (`tab:aplikacje`: `react-admin`, `refine`, `Twenty`, `Saleor Dashboard`, `shadcn-admin`, `TailAdmin`) oraz uzasadnienie wyboru `react-admin` (Material UI) i `refine` (Ant Design) z wymiennym modułem dostępu do danych.
     - `2.5 Warianty interfejsu` — wariant bazowy, przyjazny agentom i warianty pośrednie, neutralne porty lokalne, tabela badanych czynników powiązana z kryteriami WCAG i hipotezami (`tab:czynniki`) oraz listing porównawczy HTML (`lst:wariant`).
     - `2.6 Scenariusze testowe` — struktura definicji scenariusza, przykładowy scenariusz `RA-07` (`lst:scenariusz`) oraz podział na 3 poziomy trudności.
     - `2.7 Mechanizm weryfikacji stanu` — algorytm porównania migawek $S_0$ i $S_1$, warunki poprawności, detekcja niezamierzonych skutków ubocznych oraz wykrywanie fałszywych deklaracji sukcesu.
     - `2.8 Procedura badawcza i metryki` — przebieg pojedynczego zadania, diagram iteracyjnego cyklu eksperymentalnego w TikZ (`fig:cykl`), formalne wzory na $\mathrm{TSR}(a,v)$ (`eq:tsr`) i $\Delta(a)$ (`eq:delta`) podpięte pod spis równań `\myequations{...}`, wielokrotne powtórzenia ($K \ge 3$), test McNemara, metryki uzupełniające, 7-kategorialna klasyfikacja błędów oraz model danych wyników (`tab:model`).
     - `2.9 Hipotezy badawcze` — hipotezy `H1`..`H5` (w tym `H5` dotycząca większego zysku dla słabszych modeli).
     - `2.10 Podsumowanie projektu` — syntetyczna klamra łącząca projekt z literaturą z rozdziału 1.

6. **`formatka_inz_ftims_2024/literatura.bib` — napisany w całości**
   - 38 zweryfikowanych wpisów bibliograficznych (wszystkie cytowane klucze z rozdziałów 1 i 2 mają pokrycie w `literatura.bib`).

---

## 4. Diagnostyka LaTeX i stan środowiska kompilacji

- Zainstalowane narzędzia: `/usr/bin/pdflatex`, `/usr/bin/latexmk`, `/usr/bin/bibtex`.
- Zainstalowane i działające pakiety użyte w pracy: `tikz`, `booktabs`, `tabularx`, `xcolor`, `listings`, `amsmath`, `babel` (polish).
- **Jedyny brakujący pakiet do pełnej kompilacji `main.pdf`:** w systemowej instalacji TeX Live brakuje pliku **`biblatex.sty`** (wymaganego oryginalnie przez formatkę wydziałową w linii 77 `main.tex`: `\usepackage[backend=bibtex,style=authoryear,natbib]{biblatex}`).
  - **Zweryfikowano składnię:** w teście próbnym z tymczasowym zaślepieniem makr `biblatex` polecenie `pdflatex -interaction=nonstopmode main.tex` przechodzi z kodem **`exit=0`** (zero błędów składniowych w `main.tex`, `titlepage.tex`, `rozdzial1.tex` i `rozdzial2.tex`).
  - Aby zbudować kompletny `main.pdf` z wykazem literatury, należy doinstalować w systemie pakiet dostarczający `biblatex` (np. `texlive-bibtexextra` w dystrybucjach Arch/pochodnych lub `texlive-bibtex-extra` w Debian/Ubuntu; zauważ, że szablon używa `backend=bibtex`, więc `/usr/bin/bibtex` już jest dostępny i `biber` nie jest wymagany).
- Plik `formatka_inz_ftims_2024/main.pdf` znajdujący się obecnie na dysku to nadal stary plik PDF z oryginalnego szablonu z grudnia 2024 r. — nie został jeszcze przebudowany z powodu braku `biblatex.sty`.

---

## 5. Sugerowane kolejne kroki po wznowieniu w Claude Code

1. **Przedstawienie użytkownikowi wykonanej pracy i zebranie uwag** do `rozdzial1.tex` i `rozdzial2.tex` (w obu plikach oznaczono komentarzami `% TODO (autor): ...` 4 miejsca wymagające potwierdzenia, np. numeru wersji Antigravity lub ostatecznego wyboru aplikacji z promotorem).
2. **Uzupełnienie `formatka_inz_ftims_2024/cel_i_zakres.tex`** — obecnie plik ten nadal zawiera instrukcję wzorcową z przykładami o blockchainie i grafice komputerowej, podczas gdy w `zakres.md` znajduje się już gotowy, napisany formalną polszczyzną cel i 7-punktowy zakres pracy, który można przenieść i rozwinąć w `cel_i_zakres.tex`.
3. **Ustalenie z użytkownikiem, co zrobić z pozostałymi plikami szablonu** na obecne oddanie części projektowo-literaturowej:
   - `wstep.tex` (napisać wstęp teraz czy zostawić po eksperymentach),
   - `streszczenieislowakluczowe.tex`, `rozdzial3.tex`, `podsumowanie.tex`, `wykazy.tex` (obecnie zawierają teksty instruktażowe z formatki FTIMS — przy generowaniu częściowego PDF na seminarium warto je tymczasowo zakomentować w `main.tex` lub zastąpić krótkimi informacjami o planowanej zawartości, żeby w PDF nie zostały przykłady o Ninjago i blockchainie; przy okazji w `rozdzial1.tex` usunięto już referencje do obrazków `Figures/1.jpg`, `2.png`, `3.png`).
4. **Doinstalowanie `biblatex.sty` i kompilacja `main.pdf`** (`latexmk -pdf main.tex`), a następnie wizualne sprawdzenie łamania tabel `tabularx` oraz rysunków TikZ (`fig:architektura`, `fig:cykl`).

---

## 6. Sesja 2 (Claude Code, 30.10.2026) — wykonane

1. **`cel_i_zakres.tex` — napisany w całości** (zastąpiono tekst wzorcowy formatki): uzasadnienie podjęcia tematu, cel główny (środowisko + zestaw testów porównawczych jako bezpieczny cel inżynierski), cele szczegółowe `C1`..`C7`, kryteria oceny (TSR i miary uzupełniające, odwołanie do `sec:procedura`), 7-punktowy zakres pracy (z odwołaniami do `chap:pierwszy` i `chap:drugi`) oraz ograniczenia zakresu (zgodne z sekcją 24 `AGENTS.md`).
2. **`main.tex`:** tymczasowo zakomentowano `\input` plików z tekstem wzorcowym (`streszczenieislowakluczowe`, `wstep`, `rozdzial3`, `podsumowanie`, `wykazy`) — wersja częściowa PDF zawiera teraz: cel i zakres, rozdział 1, rozdział 2, skróty, bibliografię i spisy. Dodano bibliotekę TikZ `calc`.
3. **`rozdzial2.tex`:** przerysowano `fig:architektura` (strzałki „polecenie” i „przywrócenie stanu” prowadzone ortogonalnie w odstępie między kolumnami, „odczyt stanu” z serwera danych do modułu weryfikacji — zgodnie z opisem punktu końcowego w tekście) oraz `fig:cykl` (bez nakładania się bloków i etykiet).
4. **`main.pdf` przebudowany** (42 strony, 0 błędów). Ponieważ w systemie nadal brakuje `biblatex.sty` (instalacja wymaga `sudo`), kompilację wykonano w kopii katalogu z lokalnie pobranymi z CTAN pakietami `biblatex` i `logreq` (zmienne `TEXINPUTS`/`BSTINPUTS`). Docelowo: `sudo pacman -S texlive-bibtexextra`, potem `latexmk -pdf main.tex`.
5. Pozostałe ostrzeżenia LaTeX są kosmetyczne: brak `csquotes` (zalecany przez biblatex przy babel), 3 drobne `Overfull \hbox` (< 5 pt).

## 7. Otwarte kwestie po sesji 2

- 4 komentarze `% TODO (autor)` w `rozdzial1.tex` / `rozdzial2.tex` (wersja Antigravity, licencje, ostateczny wybór aplikacji z promotorem, automatyzacja uruchamiania agenta).
- Strona tytułowa: uzupełniono autora (Igor Ordecha, 251601) i promotora (dr inż. Łukasz Chomątek) oraz rok 2027 — kompletna.
- Wstęp, streszczenie i słowa kluczowe — do napisania (zwykle po eksperymentach); rozdział 3 (testy i wyniki, aspekty prawne) i podsumowanie — po realizacji środowiska.
- Kolejny etap części praktycznej: implementacja środowiska (uruchomienie react-admin *Posters Galore* z lokalnym serwerem danych, mechanizm migawek $S_0$/$S_1$, pierwsze scenariusze).
