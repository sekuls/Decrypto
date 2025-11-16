*Stan gry to jakieś DTO , które będzie podawane od klienta*

2 osoby odpowiedzialne za backend 
osoba A - architekt serwera i sieci (controller)
- Stworzyć serwer Spring Boot, który zarządza _jedną_ sesją gry i rozsyła stan gry przez WebSocket (czyli to co wpisuje klient do serwera)
- stwórz warstwę controller:
	- co AI proponuje hihu:
		- - **Obsługa Połączeń:** Implementacja logiki `@SubscribeMapping` lub `SessionConnectedEvent`, aby wykryć nowe połączenie.
    
		- **Przypisywanie Drużyn:** Implementacja logiki "pierwszy klient = BIAŁY, drugi = CZARNY". Musi też obsłużyć rozłączenie i ponowne połączenie.
		    
		- **Odbieranie Akcji:** Stworzenie metod `@MessageMapping` (np. `/app/submit-clues`, `/app/submit-guess`), które przyjmują JSON-y od klienta.
		    
		- **Rozgłaszanie Stanu:** Ta osoba tworzy mechanizm (np. `SimpMessagingTemplate`), który wysyła **cały stan gry** do _wszystkich_ podłączonych klientów (na temat `/topic/game`) po _każdej_ akcji.

osoba B - Logika i Stan Gry (Warstwy `Service`, `Model`, `Repository`)
- model - Stworzenie  klas do reprezentowania stanu: `GameSession`, `TeamState`, `Clue`, `Guess` (zgodnie z kontraktem API).
- **`Repository`:** Stworzenie `InMemoryGameRepository`. Będzie to prosta klasa (np. z adnotacją `@Repository` lub `@Component`), która trzyma w jednym, statycznym polu **jedną instancję** `GameSession` (wasz "notatnik").
- **Warstwa `Service`:** Stworzenie `GameService`. To jest serce aplikacji.
	- Implementuje metody, które woła Osoba A: `void submitClues(Team team, List<String> clues)`, `void submitGuess(Team team, int[] code)`.    
	- **Walidacja:** Implementuje "debiloodporność" po stronie serwera (czy na pewno podano 3 hasła? 

2 osoby odpowiedzialne za frontend 
Stworzyć aplikację React (`Vite`), która łączy się z WebSocketem, trzyma stan gry w głównym stanie (state) i renderuje komponenty.

Osoba C: Logika, Stan i Komunikacja (React "Container" Logic)
- ai ci radzi :
	- Nie buduje pięknych przycisków, ale sprawia, że one działają.
	- **Setup Projektu:** Inicjalizacja projektu React 
	- **Zarządzanie Stanem:** Stworzenie głównego stanu aplikacji, który będzie przechowywał stan gry otrzymany z serwera.
	    - Użycie `useState` w głównym komponencie `App.js`, jeśli jest prosty.
	    - (Zalecane) Użycie `createContext` (React Context API), aby satn gry był dostępny globalnie dla wszystkich komponentów.
	- **Komunikacja WebSocket:** Implementacja logiki połączenia (biblioteki `SockJS` i `Stomp.js` działają też w React).
	    - Stworzenie "serwisu" lub customowego hooka (np. `useGameSocket`), który łączy się z serwerem, subskrybuje temat `/topic/game` i aktualizuje globalny stan (`setGameState`) za każdym razem, gdy przychodzi nowa wiadomość.
	- **Funkcje Akcji:** Stworzenie funkcji do wysyłania danych (np. `sendClues(hasla)`, `sendGuess(kod)`). Te funkcje będą przekazywane jako _props_ do komponentów Osoby D.


Osoba D
ai ci prawde powie:
	Ta osoba tłumaczy wasz szkic z notatnika na komponenty React (JSX i CSS).
	- **Budowa Komponentów (JSX):** Stworzenie biblioteki "głupich" (presentational) komponentów, które tylko renderują dane otrzymane w `props`:
	    - `<Notepad team="white" data={gameState.druzynaBiala} />`
	    - `<Notepad team="black" data={gameState.druzynaCzarna} />`
	    - `<ClueInputPopup onSubmit={props.onClueSubmit} />` (komponent formularza/pop-upa)
	    - `<GuessForm round={1} onGuess={props.onGuessSubmit} />`
	- **Style (CSS):** Ostylowanie wszystkich komponentów. Możecie użyć:
	    - Zwykłego CSS (`App.css`).
	    - CSS Modules (np. `Notepad.module.css`) – polecane, by uniknąć konfliktów.
	- **Renderowanie Danych:** Osoba D nie martwi się _skąd_ biorą się dane. Po prostu bierze `props` (dostarczone przez Osobę C) i wyświetla je. Np. "jeśli `props.fazaGry` to `WPISYWANIE_HASLA`, pokaż komponent `<ClueInputPopup />`".
	- **Blokowanie UI:** Implementacja logiki `disabled` na przyciskach i polach na podstawie `props` (np. `fazaGry` lub `aktywnaDruzyna`).