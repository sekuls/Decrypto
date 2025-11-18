### User Stories jako tryby gry:
1. [[Pierwszy - interaktywny notatnik|Gracze są fizycznie koło siebie korzystają z aplikacji jako z notatnika]]
	Pierwszy user story to jednocześnie pierwszy milestone. Grupa znajomych chce miło razem pospędzać czas i zagrać w decrypto. Okazało się że notatnik dostarczony w pudełku się zgubił. Gracze nie chcą marnować papieru na notatnik więc otwierają naszą aplikacje.
	
	Aplikacja nie bierze udziału w przydzielaniu osób do drużyn ani w losowaniu pytań. 2 graczy łączy się z serwerem przez telefon/laptopa który następnie jest sobie przekazywany w zależności od tego kto jest szyfrującym w tej rundzie. Notatnik nie monitoruje przestrzegani
	a zasad ani ról graczy. Monitoruje natomiast przebieg gry, punktacje i kiedy się ona zakończy.

---
Rozpoczęcie gry
	 Jako gospodarz gry, chcę rozpocząć nową grę, podzielić graczy na drużyny i rozdać im tajne słowa, aby obie drużyny były gotowe na rozpoczęcie gry.
	 Symulacja:
	  - klikam "nowa gra" i czekam na graczy.
	  - klikam rozpocznij
	  - System musi automatycznie wylosować 4 unikalne słowa-klucze dla drużyn
	  - Ekran gry wyświetla panel drużyny "Białych" z ich 4 słowami i panel drużyny "Czarnych" z ich 4 słowami.
	  - Słowa drużyny "Białych" są widoczne _tylko_ dla graczy z tej drużyny (na ich ekranie/panelu). Słowa drużyny "Czarnych" są dla nich ukryte (i vice versa)

---
 Otrzymanie Kodu i Tworzenie Wskazówek - koder
	Jako Koder w swojej turze, chcę zobaczyć tajny 3-cyfrowy kod i mieć możliwość wpisania trzech publicznych wskazówek, aby naprowadzić moją drużynę na właściwą kolejność.
	Symulacja:
	- Jest pierwsza runda i rozpoczęła się moja tura bycia koderem drużyny "Białych". Mam 4 tajne słowa, które **widzę ja wraz z moją drużyną** np. ako, paa, aisd, swim
	- System losuje i wyświetla **tylko dla mnie** tajny kod, np. "2 - 4 - 1".
	- Moi kamraci z drużyny "Białych" **nie widzą** tego kodu. Drużyna "Czarnych" również go nie widzi.
	- Patrząc na kod (2-paa,4-swim,1-ako), wpisuję trzy wskazówki w publiczne pola tekstowe np." killer 2, arduino ,killer 1"
	- Klikam przycisk "zatwierdź wskazówki".
	- Wskazówki "killer 2, arduino ,killer 1" stają się widoczne dla **wszystkich** graczy (obu drużyn).
	- Moja rola jako kodera w tej turze się kończy (nie mogę już nic zmieniać), a system przechodzi do fazy zgadywania.
	- W następnej rundzie "białych" rolę kodera odgrywa następna osoba

---
Faza zgadywania - próba przechwycenia przez drużynę przeciwną
	Jako członek drużyny przeciwnej (przechwytującej), chcę zobaczyć publiczne wskazówki przeciwnika i spróbować odgadnąć ich tajny kod, aby zdobyć żeton przechwycenia.
	Symulacja:
	- Jestem w drużynie "czarnych". Drużyna "białych" podała wskazówki: " killer2, arduino, killer1"
	- Widzę historię poprzednich wskazówek "białych" (jeśli to nie pierwsza runda).
	- Dyskutuję z moją drużyną i wpisujemy naszą próbę odgadnięcia kodu (np. "2 - 4 - 1") w **nasz tajny panel** przechwytywania.
	- Klikamy "zatwierdź przechwycenie".
	- Nasza odpowiedź ("2-4-1") jest zapisana, ale pozostaje ukryta dla drużyny "Białych", dopóki oni nie zatwierdzą swojej odpowiedzi.
	- Jeśli nie zgadliśmy to następuje następna tura. W przeciwnym razie dostajemy żeton i gra restartuje tablice i tajne słowa rozpoczynając nową rundę

---
Rozstrzygnięcie Rundy i Punktacja
	System gry ma automatycznie podliczać wyniki rundy i aktualizować punktację dla obu drużyn, aby gracze wiedzieli, ile żetonów przechwycenia i komunikacyjnych zdobyli.
	Symulacja:
	- Faza zgadywania właśnie się zakończyła i wszystkie drużyny zatwierdziły swoje odpowiedzi w panelach odpowiedzi drużyny.
	- System porównuje każdą odpowiedź z prawidłowym tajnym kodem Kodera.
	- Drużyna, która poprawnie odgadła kod przeciwnika w swojej fazie przechwytywania, otrzymuje żeton przechwycenia.
	- Drużyna, której członkowie nie odgadli kodu swojego Kodera, otrzymuje żeton nieudanej komunikacji.
	- System aktualizuje punktację i wyświetla ją na ekranach obu drużyn, pokazując liczbę zdobytych żetonów przechwycenia oraz żetonów komunikacyjnych.
	- Wszystkie żetony i punktacja pozostają widoczne dla obu drużyn, a historia rund jest zapisywana w systemie.
	- Po podsumowaniu wyników gra przechodzi do kolejnej rundy, a rola Kodera zmienia się na kolejnego gracza w drużynie zgodnie z ustaloną kolejnością tur.

---
Zakończenie Gry
	System gry chce automatycznie zakończyć grę, gdy jedna z drużyn osiągnie warunek zwycięstwa lub przegranej.
	Symulacja:
	- Po zakończeniu rundy system sprawdza liczbę żetonów przechwycenia i żetonów nieudanej komunikacji dla obu drużyn.
	- Jeżeli którakolwiek drużyna zgromadzi wymaganą liczbę żetonów przechwycenia, zostaje ogłoszona zwycięzcą.
	- Jeżeli drużyna osiągnie maksymalną liczbę żetonów nieudanej komunikacji, zostaje uznana za przegraną, a drużyna przeciwna wygrywa.
	- System wyświetla ekran końcowy z informacją o zwycięzcy, podsumowaniem punktacji oraz historią rund dla obu drużyn.
	- Gra kończy się i blokuje dalsze wprowadzanie danych do paneli odpowiedzi drużyny.


przykładowe user stories jakie jeszcze można zrobić : 
- Faza Zgadywania: Odgadywanie Kodu (Własna Drużyna)
