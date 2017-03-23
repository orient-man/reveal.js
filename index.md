## [Rok niebezpiecznego życia, czyli F# na produkcji]()

Marcin Malinowski

- Twitter: [@orientman](https://twitter.com/orientman)
- GitHub: https://github.com/orient-man
- Blog: https://orientman.wordpress.com/

Note:

Jak wejść z F# na produkcję i pozostać przy życiu. Moje doświadczenia z wprowadzania języka F# w dużym banku. Recepta krok po kroku jak rozwiązywać łatwe - techniczne - problemy i trudne - międzyludzkie. Czyli wszystko co chcielibyście wiedzieć, ale boicie się zapytać.

---

## O mnie

    [   "Tata^2"
        "Mąż humanistki"
        "Mól książkowy"
        "Uparciuch"
        "Programista"
        "Konferencjoholik"
        "Don Kichot walczący z entropią"
        "Kocha sprzeczności i​ ​humor"
        "Wierzy w przypadek"
        "Piwny filozof"
        "W nielicznych wolnych​ ​chwilach harata w gałę (na bramce)" ]
    |> List.map ((+) "* ") |> List.iter (printfn "%s")

    ``Ekspert IT w mBanku`` >> (``Startup in Stealth Mode`` <| FinAI)

***

<!-- .slide: data-background="./img/7-circles-of-developer-hell.jpg" -->
## Preludium

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

https://blog.toggl.com/2017/02/seven-circles-of-developer-hell/

---

### Wielka Depresja

Dziś w menu (wybierz 1 lub więcej):

- Utrzymanie dziedzictwa
- Nasiadówki
    > „Tony papieru, tony analiz; Genialne myśli, tłumy na sali...” -- Elektryczne Gitary
- Strażak Sam w akcji

---

### Wyzwania

F# rządzi i co dalej:

- Jak nie wejść do tej samej rzeki?
- Jak przekonać do nowego języka?
- Jak szybko nauczyć siebie i innych?
- Jak to wdrożyć na produkcję?

---

<!-- .slide: data-background="./img/captain_obvious.jpg" data-background-size="contain" -->

---

### Plan gry albo oczywiste oczywistości

> „Houston, we have a problem”

- Nie powiększamy problemu
- Stosujemy dobre praktyki
- Odraczamy trudne decyzje
- Działamy w zgodzie (ze *Strategią*)

***

<!-- .slide: data-background="./img/arrival_movie.jpg" data-background-size="contain" -->
## Ludzie

---

<!-- .slide: data-background="#E65100" -->
### Kim są Oni?

> „Optimize for readability first”

- Czytelnik, głupcze!
- Programista, tester, analityk, menedżer, "biznes"...

---

<!-- .slide: data-background="#E65100" -->
### Idź, ewangelizuj!

- Entuzjazm jest zaraźliwy
- Świeć przykładami
- Obawa przed zmianą jest naturalna
- ...ale może to tylko zły dzień
- Entuzjazm jest zaraźliwy (znowu)

---

<!-- .slide: data-background="#E65100" -->
### Zrób szkolenie!

["The Best of"](https://gist.github.com/orient-man/14e9a9780de4d97239aa8d94ce944db8) (na 45-60 minut):

- funkcje
- typy: krotki, rekordy, listy
- unie i dopasowywanie wzorca
- kompozycyjność: operator "|>"
- narzędzia: REPL, VSCode (Vim), VS
- meta: type inference, ekspresywność, F# vs. C#
- DEMO: Type Driven Development

---

<!-- .slide: data-background="#E65100" -->
### Wespół w zespół

- Najważniejsze to dobrze zacząć
- Podziel się (małym sukcesem, odkryciem, wątpliwością...)
- Obawy weź na klatę
- Weź na luz - to tylko gra

***

<!-- .slide: data-background="rgb(123, 22, 29)" -->
## Maszyny

Krok za krokiem

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### FAKE it till you make it

- Nie jest trudno pokonać MSBuild/PowerShell
- Najnudniejsze zadanie staje się fajne
- Potrafi (chyba) wszystko

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Wąska ścieżka na produkcję

- Kompilator (F# Build Tools)
- Paczki (FSharp.Core i GAC)
- Unit testy, pokrycie kodu, SonarQube etc.
- Ukryte zależności w skryptach CI (buu!)

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Test first

- AAA... to świetny poligon do nauki
- Zwięzłe i czytelne
- Im dalej w las tym jaśniej: FsUnit, Unquote, FsCheck, własne DSL...

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Pierwszy moduł, pierwsza krew

- Funkcyjny kod w obiektowej polewie
- Bolączki integracyjne
- Null zostawiamy w przedpokoju
- Twardy bądź jak Roman Bratny

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Pierwsza aplikacyjka

- Niech będzie prosta
- Będzie w stylu OOP choćby nie wiem co
- Będziesz chciał(a) ją przepisać za 3 m-ce

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Run, Forrest, Run!

> „Write like crap if you have to, but write every day” -- @BethDunn

- Kursy, prezentacje, książki - tak, ale...
- Każdy prototyp, każdy PoC, każdy skrypt
- Przepisuj kod obiektowy tak długo aż stanie się funkcyjny
- Dziel się każdym odkryciem lub przeszkodą z Zespołem

***

<!-- .slide: data-background="./img/he-man.jpg" data-background-size="contain" -->
## Mocy przybywaj!

---

<!-- .slide: data-background="#0077bd" -->
### Zmiana przyzwyczajeń
#### Kompozycja

> „Algorytmy + struktury danych = programy” -- Niklaus Wirth

- Życie bez kontenera DI jest możliwe!
- Czyste funkcje vs. funkcje wyższego rzędu
- Pisz deklaratywnie
- Testuj i trzymaj na diecie swój CompositionRoot
- Keep It Simple Short: 10-15 plików, < 100 LoC

---

<!-- .slide: data-background="#0077bd" -->
### Zmiana przyzwyczajeń
#### Ukrywanie informacji

- Dlaczego ukrywamy? Bo chronimy stan. Wróć!
- Często struktury wychodzą proste: listy, krotki
- ...lub kod jest generyczny
- W razie Niemca: prywatne unie i sygnatury

---

<!-- .slide: data-background="#0077bd" -->
### Krew, pot i łzy

- Zły kod da się pisać w każdym języku
- Kompilator chce cię zabić: adnotacje typów!
- Nadużywając operatorów i "when" chcesz zabić się sam
- Tak samo z funkcjami wyższego rzędu: patrz DI
- Nie wszystko jest krotką lub listą: rekordy!, unie!
- Żeby zrozumieć rekurencję trzeba najpierw zrozumieć rekurencję
- Programowanie obiektowe w F# to ZŁO

---

<!-- .slide: data-background="#0077bd" -->
### Kompromisy (wpisz swoje)

Nie wszystko musi/może być innowacyjne:

- Suave/WebSharper/Fable vs. WebApi/Owin/JavaScript/RiotJs
- HTTP/REST vs. WCF
- EventStore vs. pliki vs. SQL Server
- ...

---

<!-- .slide: data-background="#0077bd" -->
### Functional Pit of Success

- Domyślnie wszystko jest takie jak być powinno
- Type inference to - jednak - biała magia
- Agenci + *async* rządzą!
- Typy danych pozwalają - wreszcie! - dobrze modelować domenę
- Zasady SOLID/CleanCode nadal obowiązują tylko łatwiej ich przestrzegać
- Architektura Port & Adapters "sama" wychodzi

---

<!-- .slide: data-background="#0077bd" -->
### Inne objawy

- Programiści zakochani w F# po uszy
- Trudno się oderwać od kodowania
- Objawy funkcyjnego przegięcia
- Nieustające dyskusje o kodzie

***

<!-- .slide: data-background="#2E7D32" -->
## Podsumowanie

I żyli długo i szczęśliwie...
.

.

.

.

.

... prawie :)

---

<!-- .slide: data-background="#2E7D32" -->
## The End

> „Of all the words of mice and men, the saddest are 'It might have been.'” -- Kurt Vonnegut