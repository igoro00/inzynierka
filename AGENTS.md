# Podsumowanie projektu

## 1. Ogólna idea projektu

Celem pracy inżynierskiej jest zbadanie, w jaki sposób projekt aplikacji webowej wpływa na skuteczność działania przeglądarek agentowych oraz opracowanie praktycznych zasad tworzenia aplikacji bardziej dostępnych dla takich systemów.

Projekt składa się z trzech głównych elementów:

1. stworzenia przykładowej biznesowej aplikacji webowej,
2. testowania na niej przeglądarek agentowych dostępnych na rynku,
3. eksperymentalnego modyfikowania aplikacji tak, aby nawet słabsze agenty mogły skutecznie wykonywać zadania.

Kluczowa idea nie polega na ulepszaniu modelu AI ani na budowie własnego agenta. Badana jest druga strona interakcji, czyli sama aplikacja webowa.

Główne pytanie projektu:

> Jak projektować aplikacje webowe, aby istniejące przeglądarki agentowe mogły wykonywać na nich zadania możliwie skutecznie i niezawodnie?

## 2. Bardzo ważne założenie

W projekcie NIE powstaje własna przeglądarka agentowa.

Nie należy implementować rozwiązania typu:

Playwright → DOM/accessibility tree → LLM → decyzja → Playwright.

Tak działają między innymi klasyczne benchmarki akademickie, jednak nie jest to przedmiot tej pracy.

Projekt powinien korzystać z gotowych przeglądarek agentowych i produktów dostępnych na rynku.

Schemat interakcji jest zatem następujący:

```text
Gotowa przeglądarka agentowa
          |
          | normalna interakcja webowa
          v
Nasza aplikacja testowa
          |
          v
Backend
          |
          v
Baza danych
```

Backend aplikacji stanowi źródło prawdy pozwalające sprawdzić, czy agent faktycznie poprawnie wykonał zadanie.

## 3. Tematyka pracy

Preferowana krótka wersja: **Badanie dostępności aplikacji webowych dla przeglądarek agentowych**

Alternatywy rozważane wcześniej:

- Projekt i analiza aplikacji webowej dla przeglądarek agentowych
- Ocena wpływu interfejsu aplikacji na skuteczność przeglądarek agentowych
- Projektowanie aplikacji webowych przyjaznych przeglądarkom agentowym
- Metody zwiększania dostępności aplikacji webowych dla agentów AI
- Projekt aplikacji webowej do testowania przeglądarek agentowych

Temat ma mieścić się maksymalnie w 13 słowach.

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

Cel pracy:

> Zaprojektowanie i implementacja aplikacji webowej umożliwiającej testowanie przeglądarek agentowych oraz analizę wpływu struktury interfejsu użytkownika na skuteczność wykonywania zadań przez agentów.

Drugim istotnym rezultatem ma być stworzenie praktycznych rekomendacji projektowych wynikających z eksperymentów.

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

## 7.2. Projekt i implementacja aplikacji webowej

Należy stworzyć przykładową aplikację biznesową.

Powinna przypominać realistyczny system SaaS / biznesowy, a nie zestaw sztucznych komponentów.

Powinna zawierać między innymi:

- logowanie,
- nawigację,
- listy danych,
- wyszukiwanie,
- filtrowanie,
- formularze,
- tworzenie danych,
- edycję danych,
- usuwanie danych,
- zmianę statusów,
- operacje wieloetapowe,
- ewentualnie dashboard.

Aplikacja powinna posiadać frontend, backend oraz bazę danych.

## 7.3. Integracja z przeglądarkami agentowymi

Ten punkt został w rozmowie skorygowany.

Nie tworzymy własnego agenta.

Zakres obejmuje:

- wybór kilku przeglądarek agentowych dostępnych na rynku,
- przygotowanie aplikacji w taki sposób, aby mogły się z nią normalnie łączyć,
- uruchamianie identycznych scenariuszy w różnych przeglądarkach,
- zbieranie wyników,
- weryfikację skuteczności poprzez backend aplikacji.

Przeglądarki agentowe należy traktować jako zewnętrzne systemy typu black-box.

Interesuje nas ich zachowanie, a nie ich wewnętrzna implementacja.

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

- realistyczną aplikację biznesową,
- gotowe przeglądarki agentowe,
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
| Przeglądarki agentowe             |
| Agent Browser 1                   |
| Agent Browser 2                   |
| Agent Browser N                   |
+------------------+----------------+
                   |
                   | wykonanie zadania
                   v
+-----------------------------------+
| Aplikacja testowa web             |
|                                   |
| - interfejs użytkownika           |
| - warianty UI                     |
| - logika biznesowa frontend       |
+------------------+----------------+
                   |
                   v
+-----------------------------------+
| Backend                           |
|                                   |
| - API                             |
| - logika biznesowa                |
| - zarządzanie scenariuszami       |
| - walidacja wyników               |
+------------------+----------------+
                   |
                   v
+-----------------------------------+
| Baza danych                       |
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

## Aplikacja biznesowa

Główny system używany przez agentów.

## Backend

Zarządza danymi i logiką biznesową.

## Baza danych

Przechowuje rzeczywisty stan aplikacji.

## Scenariusze testowe

Opisują zadania, które mają wykonywać agenty.

## Moduł walidacji

Sprawdza stan backendu po wykonaniu zadania.

## Moduł wyników / benchmarku

Przechowuje:

- nazwę agenta,
- scenariusz,
- wariant UI,
- rezultat,
- czas,
- dodatkowe metryki.

## Moduł eksperymentów

Pozwala porównywać:

```text
agent × zadanie × wariant UI
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

Najlepiej nie tworzyć osobnych aplikacji dla każdego eksperymentu.

Lepsze podejście:

```text
jedna logika biznesowa
+
wiele wariantów frontendowych
```

Przykład:

```text
/customer/edit?variant=baseline
/customer/edit?variant=semantic
/customer/edit?variant=agent-friendly
```

Dzięki temu:

- backend pozostaje identyczny,
- dane pozostają identyczne,
- scenariusz pozostaje identyczny,
- jedyną zmienną eksperymentu jest UI.

To bardzo ważne z punktu widzenia poprawności metodologicznej.

## 21. Baseline i wersja agent-friendly

Warto zaprojektować przynajmniej dwa podstawowe warianty.

## Baseline

Typowa współczesna aplikacja webowa.

Może zawierać między innymi:

- ikony bez opisów,
- custom controls,
- niejednoznaczne etykiety,
- placeholdery zamiast label,
- dynamiczne komponenty,
- rozbudowane modale.

Nie powinna być celowo zepsuta. Ma być realistycznym UI.

## Agent-friendly

Ta sama funkcjonalność, ale zoptymalizowana na podstawie hipotez.

Przykładowo:

- semantyczny HTML,
- poprawne etykiety,
- jednoznaczne action labels,
- bardziej przewidywalna nawigacja,
- czytelne komunikaty o zmianie stanu,
- ograniczenie niestandardowych widgetów.

Opcjonalnie może powstać również trzeci wariant pośredni.

## 22. Hipotezy badawcze

Możliwe hipotezy:

### H1

Semantyczne elementy HTML zwiększają skuteczność przeglądarek agentowych względem wizualnie identycznych elementów niestandardowych.

### H2

Jednoznaczne etykiety elementów interaktywnych zwiększają skuteczność wykonywania zadań.

### H3

Poprawne wykorzystanie mechanizmów accessibility zwiększa skuteczność nie tylko agentów tekstowych, ale także produktów multimodalnych.

### H4

Uproszczenie niestandardowych komponentów i dynamicznych interakcji zmniejsza liczbę nieudanych zadań.

### H5

Wpływ zmian UI jest szczególnie zauważalny w przypadku słabszych agentów/modeli.

Ostatnia hipoteza jest szczególnie zgodna z pierwotnym założeniem projektu: aplikacja ma być na tyle dostępna, aby nawet słabsze modele mogły sobie z nią radzić.

## 23. Proponowany przebieg badania

Etap 1:

Implementacja aplikacji biznesowej.

Etap 2:

Przygotowanie zestawu scenariuszy.

Etap 3:

Implementacja backendowych validatorów.

Etap 4:

Testowanie baseline UI przy użyciu kilku przeglądarek agentowych.

Etap 5:

Analiza błędów.

Etap 6:

Opracowanie hipotez dotyczących zmian UI.

Etap 7:

Implementacja zmodyfikowanych wersji komponentów.

Etap 8:

Ponowne wykonanie identycznych scenariuszy.

Etap 9:

Porównanie wyników.

Etap 10:

Opracowanie rekomendacji agent-friendly web design.

## 24. Czego projekt NIE powinien robić

Aby nie rozszerzyć niepotrzebnie zakresu pracy:

- nie trenować własnych modeli językowych,
- nie fine-tunować LLM,
- nie budować własnej przeglądarki agentowej,
- nie implementować własnego systemu vision,
- nie konkurować z WebArena jako benchmark modeli,
- nie próbować formalizować pełnego standardu na skalę WCAG,
- nie badać całego Internetu.

Praca ma skupić się na:

> kontrolowanej aplikacji + gotowych agentach + modyfikacjach UI + pomiarze efektu.

## 25. Najważniejsza wartość projektu

Najbardziej interesujący rezultat nie brzmi:

> „Agent A uzyskał 80%, a agent B 75%”.

Znacznie wartościowszy rezultat brzmi:

> „Po zmianie sposobu implementacji formularzy skuteczność wszystkich testowanych agentów wzrosła średnio z 58% do 83%, a największy wzrost wystąpił w przypadku słabszego agenta.”

To pokazuje bezpośrednią wartość pracy.

## 26. Docelowy rezultat pracy inżynierskiej

Po zakończeniu projektu powinny istnieć:

1. działająca aplikacja biznesowa,
2. zestaw scenariuszy testowych,
3. mechanizm backendowej walidacji,
4. możliwość testowania wielu przeglądarek agentowych,
5. co najmniej dwa warianty interfejsu,
6. wyniki eksperymentów,
7. analiza błędów agentów,
8. porównanie skuteczności wariantów,
9. zestaw praktycznych rekomendacji dotyczących projektowania aplikacji przyjaznych agentom.

## 27. Jednozdaniowy opis projektu dla kolejnego agenta

> Należy zbudować kontrolowaną biznesową aplikację webową, testować na niej istniejące rynkowe przeglądarki agentowe, automatycznie weryfikować wykonywane przez nie zadania poprzez backend, eksperymentalnie modyfikować UI i semantykę aplikacji oraz na podstawie różnic w skuteczności opracować zasady projektowania aplikacji webowych przyjaznych agentom AI.
