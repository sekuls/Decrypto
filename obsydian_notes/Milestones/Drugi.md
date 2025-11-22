*grudzień*
##### 1. Zarządzanie rozgrywkami

- przechowywanie gier na serwerze
	- Aktywne gry są przechowywane w pamięci serwera w strukturze mapy gdzie kluczem jest identyfikator gry. Każda gra zawiera kompletny stan potrzebny do zarządzania rozgrywką
	- Gra przechodzi przez kilka stanów: OCZEKIWANIE → W TRAKCIE → ZAKOŃCZONA. Automatyczne czyszczenie nieaktywnych gier 


##### 2. System rejestracji graczy

- Każdy gracz który dołącza do gry jest rejestrowany w systemie z unikalnym identyfikatorem. System przechowuje informacje o:
	- Identyfikatorze sesji WebSocket
	- Pseudonimie gracza
	- Przypisanej drużynie
	- Aktualnej roli w grze (dający podpowiedź/odgadujący)
- automatyczne przepisywanie drużyn (np. w zależności od kolejności dochodzących graczy)
- walidacja stanu gry - czy gracz który wykonuje akcje należy do właściwej gry, ma odpowiednią rolę, jest aktywny i podłączony
- usuwanie nieaktywnych 

##### 3. System słów

- mamy pulę słów i są one losowane do rozgrywek
- przy tworzeniu gry system tworzy pule słów , miesza je i wybiera po 8 (4 dla każdej z drużyn)
- słowa nie mogą się powtarzać

##### 4. Rozgrywka

 1. System podpowiedzi
 2. System odgadywania
 3. System tur
	 - zmiana między zgadującymi i podpowiadającymi
	 - licznik tur
	 - aktualizuje graczy z odpowiedzią
 4. Monitorowanie przebiegu gry