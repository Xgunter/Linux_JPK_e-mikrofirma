# Linux_JPK_e-mikrofirma
Instalacja JPK i e-mikrofirma w systemie Linux (10.03.2020)

### Spis treści
* [Weryfikacja](#weryfikacja)
* [Instalacja](#instalacja)
    * [Instalacja JPK](#instalacja-jpk)
    * [Instalacja e-mikrofirma](#instalacja-e-mikrofirma)
    
### Weryfikacja
Weryfikacja pakietów na podstawie podpisu cyfrowego i sum kontrolnych, proponowana na stronie 

https://www.podatki.gov.pl/jednolity-plik-kontrolny/jpk_vat/aplikacje-do-pobrania

nie do końca jest prawidłowa, ponieważ, certyfikat dla JPK wygasł:

```
gpgsm: Podpisano w 2018-02-13 09:16:54 przy użyciu certyfikatu o ID 0xF16984FE
gpgsm: certyfikat wygasł
gpgsm: (expired at 2018-05-04 10:51:48)
gpgsm: główny certyfikat nie jest oznaczony jako zaufany
gpgsm: invalid certification chain: Nie zaufany
```

A plik kontrolny md5 jest, ale z innymi nazwami plików (np. duże litery, dla Linuksa to różnica) i zapisany w błędnym kodowaniu, nie dla Linuksa (a przecież przeznaczony dla niego) i trzeba go przekonwertować do formatu uniksowego.


Po zmianie nazw i konwersji pliku kontrolnego, wynik już jest prawidłowy i sumy potwierdzone, ale tylko słabym md5.
```
Klient_JPK_2.i386.sh.p7s: DOBRZE
Klient_JPK_2.amd64.sh.p7s: DOBRZE
Klient_JPK_2.i386.sh: DOBRZE
Klient_JPK_2.amd64.sh: DOBRZE
```
Lepiej jest z certyfikatem dla e-mikrofirma „wersja portatywna”, jest aktualny.

Przyjąć jako zaufany.
```
gpgsm: Podpisano w 2020-01-07 10:26:22 przy użyciu certyfikatu o ID 0x22F82968
gpgsm: główny certyfikat nie jest oznaczony jako zaufany
gpgsm: odcisk=AF:E5:D2:44:A8:D1:19:42:30:FF:47:9F:E2:F8:97:BB:CD:7A:8C:B4
gpgsm: główny certyfikat nie został oznaczony jako zaufany
gpgsm: Poprawny podpis złożony przez "/CN=Ministerstwo Finansow/O=Ministerstwo Finansow/STREET=ul. Swietokrzyska 12/L=Warszawa/ST=Polska/C=PL/PostalCode=00-916"
```
I potwierdzenie prawidłowo podpisanego pliku.
```
gpgsm: Podpisano w 2020-01-07 10:26:22 przy użyciu certyfikatu o ID 0x22F82968
gpgsm: Poprawny podpis złożony przez "/CN=Ministerstwo Finansow/O=Ministerstwo Finansow/STREET=ul. Swietokrzyska 12/L=Warszawa/ST=Polska/C=PL/PostalCode=00-916"
```
     
*Podsumowując, JPK można sprawdzać tylko sumy kontrolne md5, **certyfikat jest przestarzały (chyba że zmienimy date w systemie, na czas sprawdzania)**, a e-mikrofirma jest podpisana prawidłowym i aktualnym certyfikatem.*

###   Instalacja.

#### Instalacja JPK
Instalacja JPK jest prosta i  sprowadza się do instalacji domyślnego pakietu java, w Debianie trzeba zainstalować (doinstalować) openjfx, oraz pobraniu certyfikatu MF i go dodaniu. Pierwsze uruchomienie i aktualizacja z poziomu aplikacji, zamknie się sama po częściowej aktualizacji, ponownie uruchomić i powtórzyć dalszą aktualizacje. Aplikacja prawidłowo tworzy aktywator. 
Klient JPK uruchamia się dość długo, jak to przystało na jave, ale działa bez dalszych problemów.

#### Instalacja e-mikrofirma
Instalacja e-mikrofirma, do działania wymaga „Oracel Java” w wersji 8. Dlatego jak ktoś instaluje obydwa programy, to od razu niech instaluje Oracle Java, JPK działa też prawidłowo z tą wersją. Jeżeli była zainstalowana java w innej wersji, to tą trzeba ustawić jako domyślną. 

Przy instalacji e-mikrofirma wymagana jest ingerencja w aktualizacje, nie radzi sobie tak jak JPK, który aktualizuje się bez większych problemów. 

W przypadku pobrania *„Wersji portatywnej”* (spakowanej nie wymagającej instalacji, łatwiejsza do użycia w Linuksie ), po rozpakowaniu i uruchomieniu przeprowadzana jest aktualizacja, musimy sami podmienić plik z aktualizowany i sami utworzyć aktywator do programu.   
