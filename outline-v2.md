Rok niebezpiecznego życia, czyli F# na produkcji - ToC
===

## Wstęp: Moja historia

 * Wielka Depresja

   Programowanie to (wybierz 1 lub więcej odpowiedzi):

   - Utrzymanie dziedzictwa
   - Nasiadówki
     > Tony papieru, tony analiz; Genialne myśli, tłumy na sali... -- Elektryczne Gitary
   - Strażak Sam w akcji

 * Wyzwania

   F# rządzi i co dalej:

   - Jak nie wejść do tej samej rzeki?
   - Jak przekonać do nowego języka?
   - Jak szybko nauczyć siebie i innych?
   - Jak to wdrożyć na produkcję?

 * Plan gry, albo oczywiste oczywistości

   > Houston, we have a problem

   - Nie powiększamy problemu
   - Stosujemy dobre praktyki
   - Odraczamy trudne decyzje
   - Działamy w zgodzie (ze Strategią)

## Ludzie

 * Kim są Oni?

   > Optimize for readability first

   - Czytelnik, głupcze!
   - Wszyscy inni

 * Idź, ewangelizuj!

   - Entuzjazm jest zaraźliwy
   - Świeć przykładami
   - Obawa przed zmianą jest naturalna
   - ...ale może to tylko zły dzień
   - Entuzjazm jest zaraźliwy (znowu)

 * Zrób szkolenie!

   "The Best of" (na 45-60 minut):

   - funkcje
   - typy: krotki, rekordy, listy
   - unie i dopasowywanie wzorca
   - kompozycyjność: operator "|>"
   - narzędzia: REPL, VSCode (Vim), VS
   - meta: type inference, ekspresywność, F# vs. C#
   - DEMO: Type Driven Development

 * Wespół w zespół

   - Najważniejsze to dobrze zacząć
   - Podziel się (małym sukcesem, odkryciem, wątpliwością...)
   - Obawy weź na klatę
   - Weź na luz - to tylko gra

## Maszyny

 Krok za krokiem

 * FAKE it till you make it

   - Nie jest trudno pokonać MSBuild/PowerShell
   - Najnudniejsze zadanie staje się fajne
   - Potrafi (chyba) wszystko

 * Wąska ścieżka na produkcję

   - Kompilator (F# Build Tools)
   - Paczki (FSharp.Core i GAC)
   - Unit testy, pokrycie kodu, SonarQube etc.
   - Ukryte zależności w skryptach CI (buu!)

 * Test first

   - AAA... to świetny poligon do nauki
   - Zwięzłe i czytelne
   - Im dalej w las tym jaśniej: FsUnit, Unqoute, FsCheck, własne DSL...

 * Pierwszy moduł, pierwsza krew

   - Funkcyjny kod w obiektowej polewie
   - Bolączki integracyjne
   - Null zostawiamy w przedpokoju
   - Twardy bądź jak Roman Bratny

 * Pierwsza aplikacyjka

   - Niech będzie prosta
   - Będzie w stylu OOP choćby nie wiem co
   - Będziesz chciał(a) ją przepisać za 3 m-ce

 * Run, Forrest, Run!

   > Write like crap if you have to, but write every day -- @BethDunn

   - Kursy, prezentacje, książki - tak, ale...
   - Każdy prototyp, każdy PoC, każdy skrypt
   - Przepisuj kod obiektowy tak długo aż stanie się funkcyjny
   - Dziel się każdym odkryciem lub przeszkodą z Zespołem

## Co z tego wynikło?

 * Zmiana przyzwyczajeń: kompozycja

   > Algorytmy plus struktury danych równa się programy -- Niklaus Wirth

   - Życie bez kontenera DI jest możliwe!
   - Czyste funkcje vs. funkcje wyższego rzędu
   - Pisz deklaratywnie
   - Testuj i trzymaj na diecie swój CompositionRoot
   - Keep It Simple Short: +/- 10 plików, < 100 LoC

 * Zmiana przyzwyczajeń: ukrywanie informacji

   - Dlaczego ukrywamy? Bo chronimy stan. Wróć!
   - Często struktury wychodzą proste: listy, krotki
   - ...lub kod jest generyczny
   - W razie Niemca: prywatne unie i sygnatury

 * Przestrogi okupione krwią, potem i łzami

   - Zły kod da się pisać w każdym języku
   - Kompilator chce cię zabić: adnotacje typów!
   - Nadużywając operatorów i "when" chcesz zabić się sam
   - Tak samo z funkcjami wyższego rzędu: patrz DI
   - Nie wszystko jest krotką lub listą: rekordy!, unie!
   - Żeby zrozumieć rekurencję trzeba najpierw zrozumieć rekurencję
   - Programowanie obiektowe w F# to ZŁO

 * Kompromisy (wpisz swoje)

   Nie wszystko musi/może być innowacyjne:

   - Suave/WebSharper/Fable vs. WebApi/Owin/JavaScript/RiotJs
   - HTTP/REST vs. WCF
   - EventStore vs. pliki vs. SQL Server

 * Functional Pit of Success

   - Domyślnie wszystko jest takie jak być powinno
   - Type inference to - jednak - biała magia
   - Agenci (MailboxProcessor) + async rządzą!
   - Typy danych pozwalają - wreszcie! - dobrze modelować domenę
   - Zasady SOLID/CleanCode nadal obowiązują tylko łatwiej ich przestrzegać
   - Architektura Port & Adapters "sama" wychodzi

 * Inne objawy

   - Programiści zakochani w F# po uszy
   - Trudno się oderwać od kodowania
   - Objawy funkcyjnego przegięcia
   - Nieustające dyskusje o kodzie

## Podsumowanie

   I żyli długo i szczęśliwie... [*]

   [*] Prawie :)

## The End

> Of all the words of mice and men, the saddest are 'It might have been.' -- Kurt Vonnegut
