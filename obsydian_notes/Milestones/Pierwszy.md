siema tutaj zrobie ładny opis jak będę miała chwilkę ~ Olga

*listopad*
- konfiguracja projektu 
- 2 gracze mogą stworzyć/dołączyć do gry
- Każdy gracz widzi swoje 4 słowa
- Gracze na zmianę dają podpowiedzi
- react - prosta wizualizacja przebiegu rozgrywki


## implementacja java


##### 1.WebSocket Setup, komunikacja w czasie rzeczywistym

- System używa protokołu WebSocket do dwukierunkowej komunikacji między serwerem a klientami. Każdy gracz utrzymuje stałe połączenie z serwerem, co pozwala na natychmiastowe przesyłanie wydarzeń w grze. Każde połączenie WebSocket jest identyfikowane przez unikalny session ID. Serwer śledzi które połączenie należy do którego gracza i która gracza

- przewodnik: https://www.baeldung.com/java-websockets

- Struktura kanałów:
	- **Kanały broadcast** - wiadomości rozsyłane do wszystkich graczy w pokoju (np. zmiana stanu gry, dołączenie gracza)
	- **Kanały prywatne** - wiadomości kierowane do konkretnego gracza (np. błędy, prywatne informacje)
	- **Kanały komend** - endpointy do których klienci wysyłają akcje (np. stworzenie gry, wysłanie podpowiedzi)

##### 2.Tworzenie rozgrywki
![[Pasted image 20251030192712.png]]

- tworzenie kodu pokoju w celu dołączenia innych graczy do gry
- system automatyczne przygotwuje grę:
	- Losuje 8 unikalnych słów z puli słów (4 dla każdej drużyny)
	- Inicjalizuje struktury danych do śledzenia stanu gry
	- Ustawia początkowy status gry na "OCZEKIWANIE NA GRACZY"
	- Przygotuje system punktacji z zerowymi wartościami początkowym