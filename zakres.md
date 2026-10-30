# Zakres pracy inżynierskiej

Przeglądarki agentowe to narzędzia wykorzystujące sztuczną inteligencję do samodzielnego poruszania się po stronach internetowych i wykonywania na nich operacji w imieniu użytkownika. Ich rozwój sprzyja automatyzacji powtarzalnych, rutynowych zadań biurowych, takich jak uzupełnianie formularzy czy zarządzanie danymi w panelach administracyjnych. Rozwiązania te często jednak popełniają błędy, ponieważ aplikacje internetowe projektowane są wyłącznie z myślą o obsłudze przez człowieka, a nie przez systemy automatyczne.

Celem pracy jest zaprojektowanie oraz implementacja środowiska i zestawu testów porównawczych umożliwiających rzetelny pomiar skuteczności agenta przeglądarkowego w zadaniach biurowych. Opracowane rozwiązanie posłuży następnie do zbadania, w jakim stopniu modyfikacje w strukturze interfejsu aplikacji wpływają na poprawność realizacji zadań przez agenta.

1. Przegląd literatury i analiza istniejących rozwiązań
   - Omówienie współczesnych podejść do budowy agentów przeglądarkowych opartych o duże modele językowe oraz modele multimodalne (w kontekście interakcji z interfejsami internetowymi).
   - Przedstawienie sposobów reprezentacji stron internetowych wykorzystywanych przez agentów (m.in. drzewo dokumentu DOM, drzewo dostępności, zrzuty ekranu) oraz ich ograniczeń.
   - Analiza istniejących zestawów testów porównawczych i środowisk badawczych (np. WebArena, WebVoyager, WebSuite) pod kątem możliwości oceny skuteczności agentów oraz wsparcia projektowania aplikacji przyjaznych agentom.

2. Wybór, adaptacja i modyfikacja aplikacji internetowych
    - Wybór i uruchomienie otwartoźródłowych aplikacji biurowych (np. paneli administracyjnych) zawierających typowe scenariusze interakcji użytkownika (formularze, nawigacja, filtrowanie, tworzenie, odczyt, edycja i usuwanie danych).
    - Opracowanie i implementacja różnych wariantów interfejsu użytkownika w badanych aplikacjach (np. modyfikacja struktury DOM, nazewnictwa elementów, poziomu semantyki HTML oraz atrybutów ARIA).
    - Przygotowanie mechanizmów umożliwiających weryfikację poprawności wykonania zadań przez agenta (np. sprawdzanie stanu aplikacji po stronie serwera oraz w bazie danych).

3. Integracja z agentem przeglądarkowym Google Antigravity
    - Konfiguracja agenta przeglądarkowego w środowisku Google Antigravity oraz przygotowanie kontrolowanego środowiska umożliwiającego wykonywanie zadań testowych na wybranych aplikacjach.
    - Opracowanie mechanizmów automatycznej weryfikacji poprawności wykonania zadań przez agenta na podstawie stanu aplikacji oraz danych po stronie serwera.
    - Przygotowanie procedury badawczej umożliwiającej porównanie skuteczności agenta Google Antigravity w zależności od struktury interfejsu użytkownika, zastosowanego modelu oraz poziomu dostępności aplikacji.

4. Definicja scenariuszy testowych i eksperymentów
    - Opracowanie zestawu zadań testowych odzwierciedlających realistyczne scenariusze użycia aplikacji biurowej oraz panelu administracyjnego (np. wyszukiwanie, tworzenie i edycja danych, zmiana statusów).
    - Przygotowanie środowiska eksperymentalnego umożliwiającego powtarzalne testowanie różnych modeli i konfiguracji w Google Antigravity.
    - Uwzględnienie różnych poziomów trudności zadań oraz wariantów interfejsu wpływających na dostępność dla agenta.

5. Analiza wpływu struktury aplikacji na skuteczność agenta
    - Przeprowadzenie eksperymentów porównujących skuteczność agenta Google Antigravity dla różnych wariantów interfejsu (np. oryginalny interfejs w porównaniu ze zmodyfikowanym semantycznym kodem HTML i ulepszonymi komponentami).
    - Identyfikacja czynników wpływających na powodzenie wykonania zadań (np. nazewnictwo elementów, struktura DOM, obecność atrybutów ARIA).
    - Analiza błędów popełnianych przez agenta oraz określenie typowych przypadków niepowodzeń.

6. Opracowanie zasad projektowania aplikacji przyjaznych agentom
    - Sformułowanie rekomendacji dotyczących projektowania interfejsów internetowych zwiększających skuteczność agentów przeglądarkowych (np. struktura HTML, jednoznaczność elementów interfejsu).
    - Porównanie uzyskanych wyników z istniejącymi standardami dostępności (np. podejście analogiczne do wytycznych WCAG).
    - Propozycja zestawu dobrych praktyk dotyczących tworzenia aplikacji przyjaznych agentom.

7. Ocena rozwiązania i wnioski
    - Ocena skuteczności agenta w zależności od zastosowanych wariantów aplikacji (np. wskaźnik skuteczności wykonania zadań, liczba kroków, czas wykonania zadania).
    - Analiza kosztów obliczeniowych oraz stabilności działania agenta przy różnych modelach.
    - Podsumowanie wyników oraz wskazanie ograniczeń zaproponowanego podejścia i kierunków dalszego rozwoju (np. zastosowanie w innych typach aplikacji, wsparcie dla nowych modeli i narzędzi agentowych).
