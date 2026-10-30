# Podsumowanie projektu

> **Zasada dla agenta AI (ważne):**
> 1. Za każdym razem, gdy użytkownik zmienia założenia projektu, podejmuje nowe decyzje architektoniczne/technologiczne lub modyfikuje koncepcję, należy **od razu zaktualizować ten plik (`AGENTS.md`)**, tak aby zawsze stanowił aktualne źródło prawdy o projekcie.
> 2. W formalnych dokumentach pracy inżynierskiej (takich jak `zakres.md`) należy unikać zapożyczeń z języka angielskiego, anglicyzmów (np. *benchmark*, *webowy*, *walidacja*, *ewaluacja*) oraz kolokwializmów (np. *ułatwiają pracę*, *zawodzą*, *żmudne*) — stosować wyłącznie formalną polszczyznę akademicką (np. *zestaw testów porównawczych*, *internetowy*, *weryfikacja*, *ocena*).

## 1. Ogólna idea projektu

Celem pracy inżynierskiej jest zbadanie, w jaki sposób projekt aplikacji webowej wpływa na skuteczność działania przeglądarek agentowych oraz opracowanie praktycznych zasad tworzenia aplikacji bardziej dostępnych dla takich systemów.

Projekt składa się z trzech głównych elementów:

1. wykorzystania i adaptacji open-source'owych przykładów biurowych aplikacji webowych (w szczególności typu „admin dashboard”),
2. testowania na nich agenta przeglądarkowego w **Antigravity** (komenda `/browser`),
3. eksperymentalnego modyfikowania interfejsu aplikacji tak, aby agent (w tym przy użyciu słabszych modeli) mógł skutecznie i niezawodnie wykonywać zadania.

Kluczowa idea nie polega na ulepszaniu modelu AI ani na budowie własnego agenta. Badana jest druga strona interakcji, czyli sama aplikacja webowa.

Główne pytanie projektu:

> Jak projektować aplikacje webowe, aby istniejące przeglądarki agentowe mogły wykonywać na nich zadania możliwie skutecznie i niezawodnie?

## 2. Bardzo ważne założenie

W projekcie NIE powstaje własna przeglądarka agentowa ani nie piszemy aplikacji biurowej od zera.

Nie należy implementować rozwiązania typu:

Playwright → DOM/accessibility tree → LLM → decyzja → Playwright.

Tak działają między innymi klasyczne benchmarki akademickie, jednak nie jest to przedmiot tej pracy.

Projekt korzysta z **Antigravity (komenda `/browser`)** jako gotowego narzędzia agentowego oraz z istniejących, open-source'owych aplikacji biurowych / „admin dashboard”.

Schemat interakcji jest zatem następujący:

```text
Antigravity (/browser)
          |
          | normalna interakcja webowa
          v
Open-source'owa aplikacja biurowa / Admin Dashboard
          |
          v
Backend / warstwa danych
          |
          v
Baza danych / stan aplikacji
```

Backend / warstwa danych aplikacji stanowi źródło prawdy pozwalające sprawdzić, czy agent faktycznie poprawnie wykonał zadanie.

## 3. Tematyka pracy

**Zgłoszony, oficjalny temat pracy inżynierskiej (11 słów):**
> **Weryfikacja skuteczności agenta przeglądarkowego Google Antigravity przy realizacji zadań w systemach biurowych**

Wcześniej rozważane robocze warianty tytułu:

- **Weryfikacja skuteczności agenta przeglądarkowego podczas obsługi wybranych systemów biurowych** (9 słów)
- **Weryfikacja skuteczności agenta AI w obsłudze wybranych webowych systemów biurowych** (10 słów)
- **Weryfikacja skuteczności agenta przeglądarkowego przy realizacji zadań w wybranych systemach biurowych** (11 słów)
- **Weryfikacja skuteczności agenta Google Antigravity w obsłudze wybranych systemów biurowych** (10 słów)
- **Badanie skuteczności autonomicznego agenta AI podczas obsługi wybranych systemów biurowych** (10 słów)

Alternatywy rozważane wcześniej:

- Badanie dostępności aplikacji webowych dla przeglądarek agentowych
- Projekt i analiza aplikacji webowej dla przeglądarek agentowych
- Ocena wpływu interfejsu aplikacji na skuteczność przeglądarek agentowych
- Projektowanie aplikacji webowych przyjaznych przeglądarkom agentowym
- Metody zwiększania dostępności aplikacji webowych dla agentów AI

Temat ma mieścić się maksymalnie w 13 słowach.

**Dane formalne:** autor — Igor Ordecha (nr albumu 251601), promotor — dr inż. Łukasz Chomątek; Politechnika Łódzka, Wydział FTIMS, kierunek Informatyka Stosowana, Instytut Informatyki I72; rok na stronie tytułowej: 2027.

## 4. Problem inżynierski

## Aktualny stan

Obecnie:

- dynamicznie rozwijają się przeglądarki agentowe i agenty wykorzystujące duże modele językowe oraz modele multimodalne,
- istnieją benchmarki służące do oceny skuteczności modeli i agentów w interakcji ze stronami internetowymi,
- skuteczność agentów zależy nie tylko od możliwości modelu, ale również od struktury, semantyki i sposobu zaprojektowania interfejsu aplikacji.

## Problem

Istniejące rozwiązania koncentrują się głównie na ulepszaniu i porównywaniu agentów.

Brakuje natomiast:

- metod oceny aplikacji internetowej z perspektywy dostępności dla agentów,
- badań wpływu konkretnych decyzji projektowych UI/HTML na skuteczność przeglądarek agentowych,
- środowiska umożliwiającego iteracyjne zmiany aplikacji i mierzenie wpływu tych zmian,
- praktycznych zasad projektowania aplikacji „agent-friendly”.

Problem można streścić następująco:

> Brakuje metod oraz narzędzi pozwalających projektować i oceniać aplikacje webowe pod kątem skutecznej obsługi przez istniejące przeglądarki agentowe.

## 5. Cel pracy

Główny, bezpieczny cel inżynierski (w pełni osiągalny i niezależny od tego, jak duże okażą się wzrosty skuteczności w eksperymentach):

> Zaprojektowanie i stworzenie rzetelnego benchmarku (środowiska testowego opartego na otwartoźródłowych aplikacjach biurowych i automatycznej walidacji stanu po stronie serwera) pozwalającego mierzyć skuteczność agenta przeglądarkowego Google Antigravity (`/browser`) w zadaniach biurowych.

Opracowany benchmark posłuży następnie do zbadania, czy i w jakim stopniu zmiany w budowie interfejsu aplikacji ułatwiają agentowi pracę, oraz do sformułowania wniosków i rekomendacji projektowych.

> **Ważna uwaga pragmatyczna:** Definiujemy główny cel jako **zaprojektowanie rzetelnego benchmarku**, aby uniknąć pułapki uzależnienia sukcesu pracy inżynierskiej od tego, czy modyfikacje UI zawsze przyniosą spektakularną poprawę wyników agenta. Sam rzetelny benchmark z powtarzalnymi scenariuszami i obiektywną walidacją stanowi główny produkt inżynierski.

## 6. Główny wkład autorski

Projekt nie powinien być jedynie kolejnym benchmarkiem agentów.

Autorski wkład polega na zmianie perspektywy:

```text
Typowe podejście:

Jak ulepszyć agenta,
aby poradził sobie z istniejącą stroną?


Podejście tej pracy:

Jak ulepszyć stronę,
aby istniejące agenty lepiej sobie z nią radziły?
```

Najważniejszym rezultatem powinno być ustalenie, które właściwości aplikacji pomagają agentom, a które powodują błędy.

## 7. Zakres pracy

## 7.1. Przegląd literatury i istniejących rozwiązań

Należy omówić:

- współczesne przeglądarki agentowe,
- sposób działania agentów webowych,
- różne reprezentacje strony używane przez agentów:
  - DOM,
  - accessibility tree,
  - screenshot / vision,
- istniejące benchmarki agentów,
- sposoby weryfikacji poprawności wykonania zadań.

Szczególną uwagę należy zwrócić na to, że większość istniejących rozwiązań ocenia agentów zamiast aplikacji.

## 7.2. Wybór i adaptacja open-source'owych aplikacji biurowych (typu „admin dashboard”)

Zamiast tworzyć sztuczną aplikację od zera, w pracy wykorzystane zostaną gotowe, open-source'owe przykłady aplikacji biurowych / **admin dashboard** (np. systemy CRM, panele administracyjne, back-office).

Wstępnie znalezione przykłady open-source (**lista ma charakter otwarty — nie zamykamy się wyłącznie na te 6 pozycji**):

1. **react-admin (demo — Poster Galore)**: https://github.com/marmelab/react-admin/tree/master/examples/demo
2. **refine (finefoods-antd)**: https://github.com/refinedev/refine/tree/main/examples/finefoods-antd
3. **Twenty CRM**: https://github.com/twentyhq/twenty
4. **Saleor Dashboard**: https://github.com/saleor/saleor-dashboard
5. **shadcn-admin**: https://github.com/satnaing/shadcn-admin
6. **TailAdmin (free-react-tailwind-admin-dashboard)**: https://github.com/TailAdmin/free-react-tailwind-admin-dashboard

Wybrane aplikacje reprezentują realistyczne systemy biurowe i obejmują typowe operacje:

- logowanie i nawigację,
- listy danych, wyszukiwanie i filtrowanie,
- formularze, tworzenie, edycję i usuwanie danych,
- zmianę statusów i operacje wieloetapowe,
- widoki dashboardowe.

## 7.3. Testowanie przy użyciu Antigravity (`/browser`)

Nie tworzymy własnego agenta ani nie testujemy wielu różnych przeglądarek zewnętrznych — **testujemy wyłącznie Antigravity (poprzez komendę `/browser`)**.

Zakres obejmuje:

- wykorzystanie wbudowanego agenta przeglądarkowego w Antigravity (`/browser`),
- lokalne uruchomienie wybranej aplikacji (lub zestawu aplikacji) open-source w kontrolowanym środowisku,
- uruchamianie powtarzalnych scenariuszy testowych w Antigravity (`/browser`),
- zbieranie wyników oraz weryfikację skuteczności (sprawdzenie stanu danych / backendu aplikacji).

Agenta przeglądarkowego Antigravity traktujemy jako system typu black-box — interesuje nas jego zachowanie i skuteczność w zależności od konstrukcji UI aplikacji.

## 8. Scenariusze testowe

Aplikacja powinna posiadać jawny i powtarzalny zestaw zadań.

Przykłady:

- zaloguj się na konto konkretnego użytkownika,
- znajdź klienta o określonym nazwisku,
- utwórz nowego klienta,
- zmień adres klienta,
- znajdź zamówienie o określonym numerze,
- zmień status zamówienia,
- dodaj produkt do zamówienia,
- usuń produkt,
- ustaw filtr,
- wyszukaj rekord spełniający kilka warunków,
- wykonaj sekwencję kilku operacji,
- sprawdź określoną informację i na jej podstawie wykonaj inną akcję.

Zadania powinny mieć różny poziom trudności.

## 9. Automatyczna walidacja

Bardzo ważnym elementem projektu jest to, że poprawność nie powinna być oceniana tylko na podstawie tego, co agent deklaruje.

Backend powinien sprawdzać rzeczywisty stan systemu.

Przykład:

Polecenie:

> Znajdź klienta Jan Kowalski i zmień jego status na VIP.

Po zakończeniu zadania backend może sprawdzić:

```text
customer.name == "Jan Kowalski"
customer.status == "VIP"
```

Dzięki temu wynik benchmarku jest obiektywny.

Walidacja może sprawdzać:

- stan rekordów w bazie,
- utworzenie obiektu,
- usunięcie obiektu,
- zmianę określonych pól,
- liczbę obiektów,
- powiązania między rekordami,
- sekwencję zmian.

## 10. Metryki

Podstawowa metryka: **Task Success Rate**

czyli procent poprawnie wykonanych zadań.

Możliwe dodatkowe metryki:

- czas wykonania zadania,
- liczba nieudanych prób,
- liczba błędnych akcji,
- liczba kroków,
- liczba przypadków wymagających interwencji człowieka,
- stabilność wyników przy wielokrotnym wykonaniu tego samego zadania.

Jeżeli dana przeglądarka nie udostępnia wszystkich informacji o liczbie kroków, task success rate pozostaje wspólną metryką możliwą do zastosowania dla wszystkich produktów.

## 11. Warianty interfejsu

Jednym z najważniejszych elementów eksperymentu jest możliwość tworzenia różnych wersji tego samego interfejsu.

Przykładowo:

## Wariant A — problematyczny dla agentów

```html
<div onclick="submit()">OK</div>
```

## Wariant B — semantyczny

```html
<button type="submit">Zapisz zamówienie</button>
```

Oba interfejsy mogą wyglądać identycznie dla człowieka, ale agent może mieć zupełnie inną skuteczność.

## 12. Czynniki, które warto badać

Eksperymenty powinny dotyczyć między innymi:

## Semantycznego HTML

Porównanie:

- `div onclick`
- `button`
- poprawne `label`
- `input`
- `select`
- tabele semantyczne.

## Nazewnictwa elementów

Porównanie:

- „OK”
- „Dalej”
- „Zapisz”
- „Zapisz klienta”
- „Usuń zamówienie”

Hipoteza: jednoznaczne nazwy pomagają agentom.

## ARIA

Badanie wpływu:

- `aria-label`,
- `aria-labelledby`,
- `aria-describedby`,
- `role`.

## Struktury formularzy

Porównanie:

- placeholder bez labela,
- poprawny label,
- pola o niejednoznacznych nazwach,
- logiczne grupowanie formularzy.

## Nawigacji

Porównanie:

- czytelnej nawigacji,
- hamburger menu,
- dropdownów,
- ikon bez tekstu,
- zagnieżdżonych menu.

## Stanów aplikacji

Porównanie:

- jednoznacznych komunikatów sukcesu,
- zmian widocznych tylko wizualnie,
- toastów,
- modali,
- optimistic UI.

## Komponentów interaktywnych

Badanie:

- checkboxów,
- custom checkboxów,
- radio buttonów,
- toggle switchów,
- dropdownów,
- autocomplete,
- date pickerów,
- drag-and-drop,
- modali.

## 13. Eksperymentalny charakter projektu

Projekt powinien umożliwiać wykonanie eksperymentu:

```text
UI v1
↓
test agentów
↓
wyniki

UI v2
↓
ta sama grupa zadań
↓
test agentów
↓
wyniki

UI v3
↓
...
```

Przykład:

```text
Atlas:
v1 → 55%
v2 → 78%
v3 → 92%

Agent B:
v1 → 40%
v2 → 70%
v3 → 86%
```

Najważniejsze jest mierzenie różnicy wynikającej ze zmian po stronie aplikacji.

## 14. Docelowy rezultat badawczy

Na podstawie eksperymentów powinien powstać katalog praktycznych zaleceń.

Można go traktować jako zalążek: **Agent Accessibility Guidelines**

lub: **Agent-Friendly Web Design Guidelines**

Koncepcyjnie przypominałoby to WCAG, ale dotyczyłoby dostępności aplikacji dla agentów AI.

Nie chodzi o stworzenie formalnego standardu, lecz o zestaw empirycznie sprawdzonych rekomendacji.

Przykładowy rezultat:

```text
AG-01:
Element wykonujący akcję powinien posiadać jednoznaczną
semantyczną rolę oraz nazwę opisującą wykonywaną operację.

Wpływ:
+23 pp task success rate

Przetestowano:
3 przeglądarki
20 scenariuszy
```

## 15. Analizowane istniejące rozwiązania

W rozmowie analizowano następujące projekty:

## OpenAI BrowseComp

Zalety:

- duży i zróżnicowany zbiór zadań,
- możliwość porównywania wyników modeli z ludźmi,
- jednoznaczna ewaluacja odpowiedzi.

Wady z perspektywy tej pracy:

- skupia się przede wszystkim na wyszukiwaniu informacji,
- nie bada typowych interakcji z aplikacjami biznesowymi,
- dostosowywany jest agent/model do istniejącego internetu zamiast aplikacji do agentów.

## BrowseComp-Plus

Zalety:

- jawniejszy i bardziej reprodukowalny benchmark,
- kontrolowane dane,
- dobra porównywalność eksperymentów.

Wady:

- skupienie na retrievalu i wyszukiwaniu informacji,
- brak realistycznej interakcji z UI,
- nie bada wpływu konstrukcji interfejsu aplikacji.

## WebArena

To jeden z najbliższych projektów pod względem ogólnej idei testowania zadań na aplikacjach.

Zalety:

- realistyczne aplikacje testowe,
- zadania przypominające rzeczywiste operacje,
- możliwość weryfikacji poprawności na podstawie stanu systemu,
- obsługa agentów tekstowych i multimodalnych.

Ważne rozróżnienie:

WebArena nie testuje bezpośrednio gotowych komercyjnych przeglądarek agentowych.

Typowa architektura wygląda tam w uproszczeniu następująco:

```text
Playwright
↓
DOM / accessibility tree / screenshot
↓
LLM
↓
akcja
↓
Playwright
```

W tej pracy tego pipeline'u NIE implementujemy.

Wady z perspektywy projektu:

- testuje przede wszystkim agentów/model,
- nie odzwierciedla dokładnie doświadczenia użytkownika gotowej przeglądarki agentowej,
- brak nacisku na ulepszanie samej aplikacji,
- brak rekomendacji dotyczących agent accessibility.

## WebSuite

Projekt istotny, ponieważ bada bardziej bezpośrednio wpływ komponentów UI na działanie agentów.

Zalety:

- testowanie konkretnych interakcji,
- analiza błędów na poziomie komponentów,
- wnioski związane z dostępnością.

Wady:

- skupienie na izolowanych komponentach,
- ograniczona reprezentatywność dla kompletnej aplikacji biznesowej,
- starszy lub niszowy stos agentowy,
- brak dużych scenariuszy end-to-end.

To ważna inspiracja dla części eksperymentalnej pracy.

## WebVoyager

Zalety:

- interakcje z realnymi stronami,
- pełne wieloetapowe zadania,
- podejście bliższe rzeczywistemu browsingowi.

Wady:

- jest przede wszystkim prototypem agenta,
- testowane strony nie znajdują się pod kontrolą autora benchmarku,
- zmiany zewnętrznych stron zmniejszają reprodukowalność,
- brak mechanizmu iteracyjnego ulepszania badanej aplikacji.

## 16. Luka badawcza wynikająca z analizy

Istniejące rozwiązania przede wszystkim odpowiadają na pytania:

- który model jest lepszy?
- który agent skuteczniej używa stron?
- jak agent powinien interpretować stronę?
- jak poprawić reasoning agenta?

Projekt odpowiada na inne pytanie:

> Jak zmienić aplikację, aby różne istniejące agenty lepiej sobie z nią radziły?

Brakuje obecnie podejścia łączącego jednocześnie:

- realistyczną aplikację biurową (typu admin dashboard),
- gotowego agenta przeglądarkowego (Antigravity `/browser`),
- kontrolowane zadania,
- backendową walidację,
- warianty tego samego UI,
- eksperymentalne porównanie,
- opracowanie rekomendacji dla twórców aplikacji.

## 17. Ogólna architektura systemu

Projekt powinien być przedstawiany bardziej jako architektura modułowa niż diagram klas.

Ogólny UML / diagram komponentów:

```text
+-----------------------------------+
| Przeglądarka agentowa             |
| Antigravity (komenda /browser)    |
+------------------+----------------+
                   |
                   | wykonanie zadania
                   v
+-----------------------------------+
| Aplikacja biurowa web             |
| (Open-source Admin Dashboard)     |
|                                   |
| - interfejs użytkownika           |
| - warianty UI                     |
| - logika aplikacji frontend       |
+------------------+----------------+
                   |
                   v
+-----------------------------------+
| Backend / warstwa danych          |
|                                   |
| - API / data provider             |
| - logika aplikacji                |
| - zarządzanie scenariuszami       |
| - walidacja wyników               |
+------------------+----------------+
                   |
                   v
+-----------------------------------+
| Baza danych / stan aplikacji      |
+-----------------------------------+

          ^
          |
+-----------------------------------+
| Moduł ewaluacji                   |
|                                   |
| - scenariusze testowe             |
| - wyniki                          |
| - metryki                         |
| - porównanie eksperymentów        |
+-----------------------------------+

          ^
          |
+-----------------------------------+
| Moduł analizy                     |
|                                   |
| - analiza błędów                  |
| - porównanie wariantów UI         |
| - rekomendacje accessibility      |
+-----------------------------------+
```

## 18. Moduły systemu

## Aplikacja biurowa (Open-source Admin Dashboard)

Główny system używany przez agenta.

## Backend / warstwa danych

Zarządza danymi i logiką aplikacji.

## Baza danych

Przechowuje rzeczywisty stan aplikacji.

## Scenariusze testowe

Opisują zadania, które ma wykonywać agent.

## Moduł walidacji

Sprawdza stan backendu / danych po wykonaniu zadania.

## Moduł wyników / benchmarku

Przechowuje:

- konfigurację agenta (Antigravity `/browser` + użyty model),
- scenariusz,
- aplikację / wariant UI,
- rezultat,
- czas,
- dodatkowe metryki.

## Moduł eksperymentów

Pozwala porównywać:

```text
model/konfiguracja Antigravity × zadanie × wariant UI
```

## Moduł analizy

Na podstawie wyników pozwala określić, które zmiany poprawiły skuteczność.

## 19. Potencjalny model danych benchmarku

W implementacji warto rozważyć encje typu:

```text
Agent
- id
- name
- version

Scenario
- id
- name
- description
- difficulty

UIVariant
- id
- name
- description

TestRun
- id
- agent_id
- scenario_id
- ui_variant_id
- started_at
- finished_at
- success
- notes

ValidationResult
- id
- test_run_id
- validator
- expected
- actual
- success
```

Nie jest to ustalona architektura klas, lecz propozycja modelu danych.

## 20. Istotna decyzja implementacyjna

Najlepiej opierać eksperymenty na kontrolowanych wariantach tych samych widoków / komponentów w wybranej aplikacji biurowej (dashboardzie) open-source:

```text
jedna logika aplikacji (ten sam dashboard open-source)
+
wiele wariantów frontendowych (baseline vs zmodyfikowany UI)
```

Przykład:

```text
/customer/edit?variant=baseline
/customer/edit?variant=semantic
/customer/edit?variant=agent-friendly
```

(lub osobne branche / flagi konfiguracyjne w wybranej aplikacji open-source).

Dzięki temu:

- backend / dane początkowe pozostają identyczne,
- scenariusz pozostaje identyczny,
- jedyną zmienną eksperymentu jest UI.

To bardzo ważne z punktu widzenia poprawności metodologicznej.

## 21. Baseline i wersja agent-friendly

Warto zaprojektować przynajmniej dwa podstawowe warianty.

## Baseline

Oryginalna wersja wybranej aplikacji biurowej open-source typu admin dashboard (lub jej standardowe komponenty).

Może zawierać między innymi:

- ikony bez opisów,
- custom controls z bibliotek UI (np. Ant Design, MUI, Radix/shadcn),
- niejednoznaczne etykiety,
- placeholdery zamiast label,
- dynamiczne komponenty,
- rozbudowane modale.

Nie powinna być celowo zepsuta. Ma być realistycznym UI pochodzącym z prawdziwego projektu open-source.

## Agent-friendly

Ta sama funkcjonalność w tym samym dashboardzie, ale zoptymalizowana na podstawie hipotez.

Przykładowo:

- semantyczny HTML,
- poprawne etykiety i atrybuty ARIA,
- jednoznaczne action labels,
- bardziej przewidywalna nawigacja,
- czytelne komunikaty o zmianie stanu,
- uproszczenie lub ulepszenie dostępności niestandardowych widgetów.

Opcjonalnie może powstać również trzeci wariant pośredni.

## 22. Hipotezy badawcze

Możliwe hipotezy:

### H1

Semantyczne elementy HTML zwiększają skuteczność przeglądarki agentowej względem wizualnie identycznych elementów niestandardowych.

### H2

Jednoznaczne etykiety elementów interaktywnych zwiększają skuteczność wykonywania zadań.

### H3

Poprawne wykorzystanie mechanizmów accessibility zwiększa skuteczność również w przypadku agenta multimodalnego (Antigravity `/browser`).

### H4

Uproszczenie niestandardowych komponentów i dynamicznych interakcji zmniejsza liczbę nieudanych zadań.

### H5

Wpływ zmian UI jest szczególnie zauważalny w przypadku słabszych modeli używanych przez agenta.

Ostatnia hipoteza jest szczególnie zgodna z pierwotnym założeniem projektu: aplikacja ma być na tyle dostępna, aby nawet słabsze modele mogły sobie z nią radzić.

## 23. Proponowany przebieg badania

Etap 1:

Wybór i uruchomienie open-source'owych aplikacji biurowych (typu „admin dashboard”).

Etap 2:

Przygotowanie zestawu scenariuszy testowych.

Etap 3:

Implementacja mechanizmu walidacji stanu po wykonaniu zadania.

Etap 4:

Testowanie baseline UI przy użyciu Antigravity (komenda `/browser`).

Etap 5:

Analiza błędów popełnianych przez agenta.

Etap 6:

Opracowanie hipotez dotyczących zmian UI.

Etap 7:

Implementacja zmodyfikowanych wersji komponentów (wariant agent-friendly) w badanych aplikacjach.

Etap 8:

Ponowne wykonanie identycznych scenariuszy w Antigravity (`/browser`).

Etap 9:

Porównanie wyników.

Etap 10:

Opracowanie rekomendacji agent-friendly web design.

## 24. Czego projekt NIE powinien robić

Aby nie rozszerzyć niepotrzebnie zakresu pracy:

- nie pisać całej aplikacji biurowej od zera (korzystamy z gotowych projektów open-source typu admin dashboard, nie zamykając się na stałą listę przykładów),
- nie testować wielu różnych przeglądarek agentowych (skupiamy się wyłącznie na Antigravity `/browser`),
- nie trenować własnych modeli językowych,
- nie fine-tunować LLM,
- nie budować własnej przeglądarki agentowej,
- nie implementować własnego systemu vision,
- nie konkurować z WebArena jako benchmark modeli,
- nie próbować formalizować pełnego standardu na skalę WCAG,
- nie badać całego Internetu.

Praca ma skupić się na:

> open-source'owych aplikacjach biurowych (admin dashboard) + agencie Antigravity (`/browser`) + modyfikacjach UI + pomiarze efektu.

## 25. Najważniejsza wartość projektu

Najbardziej interesujący rezultat nie brzmi:

> „Agent A uzyskał 80%, a agent B 75%”.

Znacznie wartościowszy rezultat brzmi:

> „Po zmianie sposobu implementacji formularzy i tabel w badanej aplikacji biurowej open-source skuteczność agenta Antigravity (`/browser`) wzrosła z 58% do 83%, a największy wzrost wystąpił przy zastosowaniu słabszego modelu.”

To pokazuje bezpośrednią wartość pracy.

## 26. Docelowy rezultat pracy inżynierskiej

Po zakończeniu projektu powinny istnieć:

1. skonfigurowane środowisko oparte na open-source'owych aplikacjach biurowych (typu admin dashboard),
2. zestaw scenariuszy testowych,
3. mechanizm walidacji stanu aplikacji / backendu,
4. procedura testowania w Antigravity (`/browser`),
5. co najmniej dwa warianty interfejsu (baseline z projektu open-source oraz wariant agent-friendly),
6. wyniki eksperymentów,
7. analiza błędów agenta,
8. porównanie skuteczności wariantów,
9. zestaw praktycznych rekomendacji dotyczących projektowania aplikacji przyjaznych agentom.

## 27. Jednozdaniowy opis projektu dla kolejnego agenta

> Należy wykorzystać open-source'owe aplikacje biurowe (typu „admin dashboard”), testować na nich agenta przeglądarkowego Antigravity (komenda `/browser`), automatycznie weryfikować wykonywane przez niego zadania na podstawie stanu danych/backendu, eksperymentalnie modyfikować UI i semantykę tych aplikacji oraz na podstawie różnic w skuteczności opracować zasady projektowania aplikacji webowych przyjaznych agentom AI.
