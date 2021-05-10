# Mechatroniczne kije nordic walking

<!-- TOC -->
- [Mechatroniczne kije nordic walking](#mechatroniczne-kije-nordic-walking)    
- [Przed uruchomieniem](#przed-uruchomieniem)    
- [Uruchomienie](#uruchomienie)        
- [Restart urządzenia](#restart-urządzenia)            
- [Zalecany](#zalecany)            
- [Niezalecany](#niezalecany)    
- [Rozpoczęcie/zakończenie pomiaru](#rozpoczęciezakończenie-pomiaru)        
- [Kalibracja](#kalibracja)        
- [Pomiar](#pomiar)    
- [Stany działania programu](#stany-działania-programu)    
- [Troubleshooting](#troubleshooting)    
- [Połączenie przez WiFi](#połączenie-przez-wifi)        
- [TL;DR](#tldr)    
- [Połączenie przez Ethernet](#połączenie-przez-ethernet)        
- [Windows](#windows)        
- [Linux](#linux)    
- [Odczyt plików z danymi przez sieć](#odczyt-plików-z-danymi-przez-sieć)        
- [Windows](#windows-1)        
- [Linux](#linux-1)    
- [Edycja ustawień przez sieć](#edycja-ustawień-przez-sieć)        
- [Windows](#windows-2)        
- [Linux](#linux-2)    
- [Odczytanie zapisanych danych bezpośrednio z karty](#odczytanie-zapisanych-danych-bezpośrednio-z-karty)    
- [Instalacja systemu na nowej karcie](#instalacja-systemu-na-nowej-karcie)    
- [Ogólny schemat działania](#ogólny-schemat-działania)
<!-- /TOC -->


## Przed uruchomieniem


- Sprawdź naładowanie akumulatora (power bank)

- Sprawdź czy karta pamięci uSD wraz z systemem obsługi kijka jest włożona do czytnika w Raspberry Pi

- Sprawdź czy do Raspberry Pi są podłączone dwa kije i stopki

## Uruchomienie
Po potwierdzeniu gotowości urządzenia do uruchomienia podłącz zasilanie do Raspberry Pi.
Po uruchomieniu oczekiwane działanie to:

- Zapalenie zielonej diody

- Zgaszenie zielonej diody

- Zapalenie czerwonej diody

Jeżeli procedura podłączenia zasilania (lub włączenia urządzenia) przebiegła jak powyżej to można rozpocząć pomiar. Od tego momentu nie jest możliwe podłączenie lub odłączenie czujników. Jeżeli nastąpi modyfikacja podłączenia należy zrestartować urządzenie.

W przypadku gdy wystąpi schemat:

- Zapalenie zielonej diody

- Miganie zielonej diody

- Zapalenie czerwonej diody

 Należy sprawdzić poprawność podłączenia czujników a następnie ponownie uruchomić urządzenie.

### Restart urządzenia
Urządzenie można zrestartować na dwa sposoby:
#### Zalecany
Wyłączamy urządzenie poprzez wciśnięcie czerwonego przycisku. Po zgaszeniu czerwonej diody należy odczekać około 10 sekund a następnie ponownie wcisnąć czerwony przycisk który ponownie uruchomi urządzenie.  
**⚠️UWAGA!** W tym sposobie nie odłączamy zasilania od urządzenia.
#### Niezalecany 
Wyłączamy urządzenie poprzez wyciągnięcie kabla zasilającego. Następnie po odczekaniu około 10 sekund ponownie podłączamy zasilanie.  
**⚠️UWAGA!** Ten sposób może doprowadzić do uszkodzenia danych na karcie uSD. Dodatkowo po uruchomieniu może zostać rozpoczęta procedura sprawdzenia integralności danych, która może potrwać do 5 minut (urządzenie nie będzie odpowiadać).

## Rozpoczęcie/zakończenie pomiaru
Po poprawnej inicjalizacji urządzenia można przystąpić do kalibracji.  W tym celu należy postępować według opisanej poniżej procedury. 
### Kalibracja
W celu poprawnej kalibracji czujników należy położyć je poziomo.
Po wciśnięciu zielonego przycisku nastąpi kalibracja czujników położenia kątowego na kijkach. Po ustaleniu się stanu diody (stałe światło) można rozpocząć chód.
### Pomiar
Pomiar zapisuje się do pliku `dane_X.txt` gdzie `X` to kolejne numery pomiarów. Można zakończyć pomiar poprzez wciśnięcie zielonego przycisku oraz rozpocząć nową kalibrację i pomiar poprzez ponowne wciśnięcie zielonego przycisku.  

## Stany działania programu
|Nr| Czerwona dioda | Zielona dioda|Stan programu |
|-|-|-|-|
|1|OFF|OFF|Brak zasilania / uruchomienie urządzenia|
|2|OFF|ON|Test podłączenia czujników|
|3|OFF|MIGA|Błąd podczas inicjalizacji urządzenia|
|4|ON|OFF|Oczekiwanie na działanie użytkownika|
|5|ON|MIGA|Jeżeli wcześniej wystąpił stan 4 -> Kalibracja|
|6|ON|MIGA|Jeżeli wcześniej nie wystąpił stan 4 -> Błąd podczas inicjalizacji urządzenia|
|7|ON|ON|Pomiar|


## Troubleshooting
| Objaw | Działanie|
|-|-|
|Po podłączeniu zasilania nie świeci się żadna dioda	|Sprawdź podłączenie zasilania, potwierdź obecność karty uSD z zainstalowanym systemie w RasbperryPi. UWAGA! Karty nie należy wkładać/wyjmować przy podłączonym zasilaniu |
|Migająca zielona dioda |Sprawdź podłączenie czujników do RaspberryPi |


## Połączenie przez WiFi
Każdy komputer RaspberryPi uruchamia swoją sieć WiFi o unikalnej nazwie do której można się połączyć w celu modyfikacji ustawień lub odczytu danych.
Nazwy sieci to: `kijek_X`, gdzie `X` oznacza numer zestawu. W przypadku wgrania nowego systemu na kartę sieć będzie nosiła nazwę `kijek_dev`. 
W celu odczytania danych/modyfikacji ustawień łączymy się z siecią dla interesującego nas zestawu. Hasło do sieci to `kijek_X`, gdzie `X` to numer zestawu. W przypadku sieci `kijek_dev` hasło to `kijek_dev`.
### TL;DR
|Nazwa sieci| Hasło|
|-|-|
|kijek_X|kijek_X|
Powyższą konfigurację połączenia wykonuje się zazwyczaj raz.

Po podłączeniu się do sieci WiFi należy otworzyć program do połączenia SSH.

## Połączenie przez Ethernet
### Windows 
https://forbot.pl/blog/kurs-raspberry-pi-instalacja-komunikacja-przez-siec-id21051  
rozdział: **Połączenie z Raspberry Pi** 
- bez zmiany hasła
|||
|-|-|
|Host Name|`raspberrypi.local`|
|Nazwa użytkownika: |`pi`|
|Hasło: |`raspberry`|

### Linux
`ssh pi@raspberrypi.local`  
hasło: `raspberry`

## Odczyt plików z danymi przez sieć

- Windows 
- WinSCP lub podobne

- Linux 
- dowolny terminal

### Windows
https://webinsider.pl/raspberry-pi-winscp/
**⚠️UWAGA!** Nie usuwamy pliku `mknw.py`,

### Linux
`scp pi@rasbpberrypi.local:./dane_* .`
## Edycja ustawień przez sieć

- Windows 
- Putty lub podobne

- Linux 
- dowolny terminal

### Windows 
https://forbot.pl/blog/kurs-raspberry-pi-instalacja-komunikacja-przez-siec-id21051
rozdział: **Połączenie z Raspberry Pi** 
- bez zmiany hasła
|||
|-|-|
|Host Name|`raspberrypi.local`|
|Nazwa użytkownika: |`pi`|
|Hasło: |`raspberry`|

### Linux
`ssh pi@raspberrypi.local`
hasło: `raspberry`  
**⚠️UWAGA!** Nie usuwamy pliku `mknw.py`,


## Odczytanie zapisanych danych bezpośrednio z karty
Należy zainstalować sterowniki i oprogramowanie z podanego linka, wystarczy licencja trial.

https://www.paragon-software.com/home/linuxfs-windows/

Po włożeniu karty do czytnika otwieramy urządzenie `rootfs`. Interesujące nas dane znajdziemy w katalogu `home/pi`.  
**⚠️UWAGA!** Nie usuwamy pliku `mknw.py`,

## Instalacja systemu na nowej karcie
To do

## Ogólny schemat działania
```mermaid
graph TD
A[Sprawdzenie poprawności podłączenia] 
B[Podłączenie zasilania]
C{Migająca zielona dioda}
D[Oczekiwanie na czerwona diodę]
E[Oczekiwanie na czerwoną diodę]
F[Restart urządzenia]
G[Wybór użytkownika]
H[Start pomiaru]
I[Stop pomiaru]
J[Wyłączenie urządzenia]
K[Kalibracja]

A --> B
B --> C
C -- TAK--> D
C -- NIE -->E
D --> F 
F --> C
E --> G
G -- Czerwony przycisk -->J
G --Zielony przycisk --> H
H --> K
K --Zielony przycisk--> I
I --> G
