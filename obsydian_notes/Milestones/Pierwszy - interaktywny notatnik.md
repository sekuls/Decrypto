### 1. Założenia
- W Pierwszym milestonie zakładamy że gracze podzielą się na drużyny samodzielnie, siedzą razem w jednym pokoju i mają grę w fizycznej formie. 
 - Tworzymy interaktywną plansze która zastąpi graczom notatnik (eco friendly nie marnujemy papieru hehe)
 - **Forma:** aplikacja webowa.
	*Prosty serwer lokalny (np. na laptopie) i łączyć się przez Wi-Fi do adresu IP w sieci lokalnej (np. `192.168.x.x:8080`). SSH nie jest do tego potrzebne.*
 - 2 osoby w pokoju wchodzą (np. przez telefon) na naszą stronę, pierwsze urządzenie zostaje grupą białą drugie grupą czarną
 - Gracze postępują z telefonami jak z notatnikiem, przekazują go kolejnym szyfrującym którzy wpisują swoje hasła. Tak samo z odgadywaniem szyfru
 - **Różnica między notatnikiem a naszą stroną: gracze nie ingerują w plansze drużyny przeciwników poza strzeleniem kolejności. Strona powinna się przeładowywać i automatycznie wpisywać hasła przeciwników w odpowiednie miejsca**
 - Po wpisaniu przez szyfrującego prawidłowego szyfru, system powinien przeprowadzić ewaluacje poprawności i przydzielić punkty za poprawne/niepoprawne strzały


## 2. Szczegóły Implementacji

### Prostokół komunikacji
- format danych - json
- przykładowa struktura wiadomości do serwera:
```json
{
  "fazaGry": "WPISYWANIE_HASLA_BIALI", // lub "ZGADYWANIE_CZARNI", 
  "runda": 1,
  "druzynaBiala": {
    "punkty": 0,
    "zycia": 2,
    
  "druzynaCzarna": {
    "punkty": 1,
    "zycia": 1,
  }
}
```
### Technologia sieciowa
Spring Boot z WebSockets


### Frontend, UI
- *przykładowy UI (analogicznty do fizycznego notatnika)- ktoś zrobi ładniejszy - ale to potem na razie może być taki po chamsku ale żeby działał*
![[Pasted image 20251030192712.png]]
- Mało zhardcodowanych elementów, napisy powinny być odnośnikiem do jakiś elementów backendu (enum lub pola konkretnej klasy) - to ułatwi modyfikacje i rozrastanie aplikacji
- Kolorystyka rozróżniająca 2 zespoły - *nie musi być czarny/biały* - ułatwić dodawanie personalizowanych kolorystyk w przyszłości
- Najlepiej by szablon notatnika był osobnym HTML "wstrzykniętym" do głównej strony (łatwiej ogarnąć taki kod)
- Nie ma osobnego szablonu dla notatnika przeciwników, wg frontu jest to identyczny notatnik, różni się backendowymi polami
- Jakieś wyświetlanie żyć i punktów
**POLA SZYFRU**:
	1. Powinny być małymi formularzami. Przy uzupełnianiu ich powinien pojawiać się dynamicznie jakiś pop-up umożliwiający zapis i upload do notatnika przeciwników
	2. Na raz aktywne jest tylko jedno pole formularza (nie można wpisywać haseł drugiej tury dopóki nie skończy się pierwsza tura)
	3. Pola strzelania szyfru debilo-odporne (może jakiś enum z którego wybieramy wartości albo walidacja po stronie backendu) i są zablokowane dopóki nie wpiszemy hasła przy nich
	4. Po uploadzie formularza słowa wpisane są na stałe w swoich polach
- **Pola Haseł:**
	1. Tam nic nie piszemy ręcznie, przy uploadzie i walidacji kolejności pola powinny się automatycznie same uzupełniać


### Backend
- Używamy dobrodziejstw Javy i springa (dziedziczenie biblioteki itp)
- Architektura warstwowa:
	- `controller` – komunikacja z frontendem (REST API)
	- `service` – logika gry
	- `model` – klasy reprezentujące stan gry (np. `Player`, `Round`, `Clue`, `Guess`)
	- `repository` – ewentualnie proste przechowywanie danych (np. w pamięci na czas jednej sesji gry)
##### Serwer
- Aplikacja uruchamiana lokalnie (np. `localhost:8080` lub IP w LAN).  
    Może być to Spring Boot z prostym `WebSocket` lub `REST API + refresh`.
- Nie ma potrzeby rejestracji graczy — sesje rozpoznawane po kolejności wejść lub kodzie gry.

##### LOGIKA APLIKACJI


##### KOMUNIKACJA Z FRONTEM


[[podział tasków]]
