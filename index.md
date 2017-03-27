## [Rok niebezpiecznego życia, czyli F# na produkcji](./)

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

Note:

Wszystko zaczęło się od sytuacji, która spotyka wielu w naszej branży. Po pierwszych miodowych miesiącach w nowej pracy nadszedł _kryzys_. 

---

### Wielka Depresja

Dziś w menu (wybierz 1 lub więcej):

- Utrzymanie dziedzictwa
- Nasiadówki
    > „Tony papieru, tony analiz; Genialne myśli, tłumy na sali...” -- Elektryczne Gitary
- Strażak Sam w akcji

Nie tak miało być!

Note:
1. Usprawnianiu i łataniu dziur w wielkich gmachach aplikacji postawionych przez rzesze bezimiennych autorów (migracja svn -> git)
1. Jako "Pan Ekspert" miałem _ex catedra_ planować świetlaną przyszłość:
  -  "Czy zatrudniać programistów tylko do pisania testów automatycznych?"
  - "Jedno repozytorium czy wiele?"
  - "Jaki procent pokrycia?"
  - "Kupować drogie narzędzie od IBM (Rational Test Virtalization Server) do testów end-to-end czy nie?"
1. Bardzo ciekawe, ale po pewnym czasie zaczyna się dostrzegać pewien wzorzec...

Słowem: sytuacja nie była różowa. A przecież mogło być tak fajnie:

* ciekawa domena (rynek walutowy, Hedge Accounting czyli rachunkowość zabezpieczeń)
* i naprawdę niegłupi ludzie zarówno w IT, jaki i w biznesie

Chciałem _zrobić różnicę_ - tylko jak?

I wtedy pojawiła jutrzenka nadziei: biznes wyszedł z pomysłem na _Nowy System_ z nietrywialną logiką (zerro CRUD-a!).

---

### Wyzwania

F# rządzi i co dalej:

- Jak nie wejść do tej samej rzeki?
- Jak przekonać do nowego języka?
- Jak szybko nauczyć siebie i innych?
- Jak to wdrożyć na produkcję?

Note:

* Bez dowodu, bo to nie jest prezentacja o tym...
* Jak nie wejść po raz drugi do tej samej rzeki i nie popełnić błędów poprzedników? (monolit + kod spaghetti)
* Od kilku lat zajmowałem się programowaniem funkcyjnym: i w pracy, i jako prelegent. Niemniej, używałem do tego celu jedynie języka C# i nie mogłem pochwalić się nawet linijką kodu produkcyjnego napisanego w F#. Jak przekonać innych do nowego języka, który nie był do tej pory używany w banku?
* Będąc jedyną osobą w zespole znającą F# - i to w stopniu początkującym - musiałem nauczyć go innych. Jak to zrobić szybko?
* Co trzeba zrobić, aby F# stał się w ogóle dostępną opcją z punktu widzenia naszych procesów Continous Delivery (kompilacja, paczkowanie, instalacja, badanie jakości kodu)?

---

<!-- .slide: data-background="./img/captain_obvious.jpg" data-background-size="contain" -->

&nbsp;

&nbsp;

&nbsp;

> „Houston, we have a problem”

Note:

Szczęście nam sprzyjało, bo korporacyjne młyny mielą powoli (analiza czy się opłaci, wykonalności, budżet, dostępność zespołu) i faktyczny start prac miał nastąpić za co najmniej 2 miesiące.

---

### Plan gry albo oczywiste oczywistości

- Nie powiększamy problemu
- Stosujemy dobre praktyki
- Odraczamy trudne decyzje
- Działamy w zgodzie (ze *Strategią*)

Note:

1. Nie dodajemy kolejnego modułu do istniejacego systemu tylko robimy "mikroserwisy"
1. Nie powiekszamy długu technologicznego rozszerzając istniejący GUI (WinForms), ale tworzymy nowy (Web/SPA)
1. Minimalizujemy użycie wewnętrznych frameworków
1. Stosujemy Test Driven Developement i piramidę testów
1. Stosujemy podejście iteracyjne i wchodzimy na produkcję z Minimum Viable Product niezależnie od bankowych "big-bangowych" release-ów

To wszystko oczywiście nie w kontrze do banku, ale jak najbardziej w zgodzie ze "strategią IT" (z duchem reformatorskim).

Teraz był czas na przemyślenie rozwiązania i prototypy "Proof-of-Concept". Decyzja o użyciu F# została odłożona.

***

<!-- .slide: data-background="./img/arrival_movie.jpg" data-background-size="contain" -->
## Ludzie

Note:

Nadszedł czas, aby przekonać innych do F#-a, oraz aby się go nauczyć na żywym organizmie, ale w kontrolowany sposób.

---

<!-- .slide: data-background="#2E7D32" -->
### Kim są Oni?

> „Optimize for readability first”

- Czytelnik, głupcze!
- Programista, tester, analityk, menedżer, "biznes"...

Note:

Należy pamiętać, że _styczność z kodem mają nie tylko programiści_. Kod jest przede wszystkim czytany (i pod tym kątem należy go optymalizować). A często czytają go również analitycy i testerzy, a czasem również menedżerzy (ex programiści) lub nawet biznes!

Wszyscy oni będą zmuszeni do nauczenia się - choćby w stopniu podstawowym - nowego języka.

Z programistami jest najłatwiej (choć bywają ciężko doświadczeni przez los...), bo generalnie lubią nowe technologie. Pisząc kod jest też najłatwiej się go nauczyć.

---

<!-- .slide: data-background="#2E7D32" -->
### Idź, ewangelizuj!

- Entuzjazm jest zaraźliwy
- Świeć przykładami
- Obawa przed zmianą jest naturalna
- ...ale może to tylko zły dzień
- Entuzjazm jest zaraźliwy
    > Poza tym uważam, że ~~Kartaginę należy zniszczyć~~ w F# da się to zrobić o wiele lepiej

Książka: [Driving Technical Change](https://pragprog.com/book/trevan/driving-technical-change)

Note:

Nudzić: "success stories" (jet.com, inne banki), prezentacje, kawałki kodu.

Obawy przed zmianą nie brać osobiście. 

Typy sceptyków: niedoinformowani, idący za stadem, cynicy, wypaleni, przygnieceni czasem, szef, irracjonalni.

> Nie ma czasu, aby zrobić dobrze, ale jest czas aby zrobić 2x

TODO: może slajd z tego?

Entuzjazm nie wystarczy! Pokazujemy, że da się lepiej - a jak? Szkolenie!

---

<!-- .slide: data-background="#2E7D32" -->
### Zrób szkolenie!

["The Best of"](https://gist.github.com/orient-man/14e9a9780de4d97239aa8d94ce944db8) (na 45-60 minut):

- tylko funkcyjne jądro
- ekspresywność
- szybka pętla zwrotna (REPL)
- system typów, który prowadzi za rękę
- DEMO: Type Driven Development
  - TDD = pętla zwrotna + eksploracja -> dobra architektura 

Note:

Na koniec realistyczny przykład z waszej domeny prezentujący podejście _Type_ Driven Development (termin Marka Seemanna).

Historyjka: _W moim przypadku materiału miałem na 45 minut, ale szkolenie przerodziło się w żywą 3h dyskusję o różnych aspektach programowania funkcyjnego._

Test vs Type - opisać te 2 podejścia...

Do kwestii nauki będę jeszcze kilka razy wracał. Ważne: takie szkolenie jest może nawet bardziej wartościowe dla prowadzącego.

---

<!-- .slide: data-background="#2E7D32" -->
### Wespół w zespół

- Najważniejsze to dobrze zacząć
- Podziel się (małym sukcesem, odkryciem, wątpliwością...)
- Pair Programming!
- Obawy weź na klatę
- Weź na luz - to tylko gra

Note:

Kończąc ten wątek:

- zaprojektuj pierwszy sukces - to podnosi morale
- szkoda czasu na samotną walkę, ktoś może się zniechęcić
- Pair Programming! Najlepiej się sprawdza w trudnych a nie żmudnych problemach. Tu właśnie taki mamy.
- przeglądy kodu częściej
- "dasz radę, a jak nie to Ci pomogę", "tak, dowieziemy Sprint", "podejrzane jest jak ktoś dowozi każdy Sprint"

Anegdota (z ukrytym przekazem):

> Mówi ojciec do syna:
> - Synu, znalazłem ci wspaniałą kandydatkę na żonę!
> - EEEE..... tato... sam potrafię znaleźć sobie dziewczynę? a kto to jest?
> - To córka Billa Gatesa!
> - OOO! Suuuper! Trzeba było tak od razu!
>
> Ojciec udaje się do Billa Gatesa na rozmowę:
> - Dzień dobry Panu! Wydaje mi się, że znalazłem doskonałego kandydata  na męża Pańskiej córki!
> - Wie Pan... ale ja nie szukam męża dla mojej córki?
> - Ależ to wiceprezes Banku Światowego!
> - Ooo! Chyba, że tak!
>
>Następnie ojciec udaje się do prezesa Banku Światowego:
> - Witam Pana Panie prezesie! Przychodzę z dobrą nowiną - mam idealnego kandydata na wiceprezesa w Pańskim banku.
> - No tak.. Ale ja nie szukam nikogo na tę posadę.
> - No wie Pan?! To zięć Billa Gatesa!
> - Cudownie! To zmienia postać rzeczy!

***

<!-- .slide: data-background="./img/terminator.jpg" -->
## Maszyny

Krok za krokiem

Note:

Przed nami były 2 miesiące, aby rozwiązać wszystkie problemy techniczne.

Z maszynami - inaczej niż ludźmi - jest prosto. Można je okiełznać za pomocą kodu. Ważne, żeby robić to krok za krokiem.

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### FAKE it till you make it

- Nie jest trudno pokonać MSBuild/PowerShell
- Najnudniejsze zadanie staje się fajne
- Potrafi (chyba) wszystko

Note:

FAKE to MAKE. Zero zależności.

Do czego użyliśmy: kompilacja, unit testy, pokrycie i analiza kodu, paczki, podniesienie środowiska testowego, przygotowanie bazy testowej, testy integracyjne...

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Wąska ścieżka na produkcję

- Kompilator (F# Build Tools)
- Paczki (FSharp.Core i GAC)
- Unit testy, pokrycie kodu, SonarQube etc.
- Ukryte zależności w skryptach CI (buu!)

Note:

- Poprawki do SonarQube plugin (na szczęście projekt ożył).
- Niestety wszystkie obecne narzędzia do pokrycia kodu wrednie zaniżają. Nie fetyszyzujmy liczby, ale jeśli faktyczne pokrycie jest 95%, a pokazuje się 65 to przykro - nie wygramy rankingu...
- Podobne problemy pewnie sprawia każda nowa wdrażana technologia.

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Test first

- AAA... to świetny poligon do nauki
- Zwięzłe i czytelne
- Im dalej w las tym jaśniej: FsUnit, Unquote, FsCheck, Canopy, expecto, własne DSL...

Note:

Testy mają - albo powinny mieć - prostą strukturę (3A), co sprawia, że są świetnym poligonem do nauki.

Poczynając od drobnych smaczków jak nazwy testów pełnymi zdaniami czy implementacje interfejsów inline (no mocks!), a kończąć na strukturalna równości, co znakomicie upraszcza asercje.

Wychodząc poza testy jednostkowe w kierunku integracyjnych, UI czy end2end to przydaje się łatwość tworzenia własnych DSL (Canopy).

My: testy wydajnościowe (analityk). TODO: Przykład

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Pierwszy moduł, pierwsza krew

- Funkcyjny kod w obiektowej polewie
- Bolączki integracyjne
- Null zostawiamy w przedpokoju
- Twardy bądź jak Roman Bratny

Note:

Ograniczenia:
- warstwa danych to istniejacy ORM (Linq-to-Sql)
- kod był konsumowany z C# via kontener DI (Autofac)
- kod musiał wołać brzydkie API C# (możliwy null, parametry "out")

Zdziwienia:
- LINQ w F# jest _inny_ (obsługa NULL sensowna, ale zdziwienie)
- Func <> FSharpFunc w przeciewieństwie np. do krotek
- konieczne przejście null <-> Option
- CLIMutableAttribute

Są jeszcze gorsze problemy np. eventy.

Nie polecam mieszanych projektów C#/F#. A jeśli już to od początku z tą myślą - i dbamy o API.

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Pierwsza aplikacyjka

- Niech będzie prosta
- Będzie w stylu OOP choćby nie wiem co
- Będziesz chciał(a) ją przepisać za 3 m-ce

Note:

W naszym przypadku to była integracja, interfejs pomiędzy dwoma systemami.

Parsowane pliki -> protokół Tibco i w drugą stronę (ciekawiej bo API PUSH/observer).

Dziś bym to zrobił inaczej.

---

<!-- .slide: data-background="rgb(123, 22, 29)" -->
### Run, Forrest, Run!

> „Write like crap if you have to, but write every day” -- @BethDunn

- Kursy, prezentacje, książki - tak, ale...
- Każdy prototyp, każdy PoC, każdy skrypt
- Przepisuj kod obiektowy tak długo aż stanie się funkcyjny
- Dziel się każdym odkryciem lub przeszkodą z Zespołem

Note:

Kończąc wątek okiełznania maszyny/języka, aby robił to co my chcemy. I abyśmy potrafili się w nim jasno komunikować. Tak jak z językiem mówionym - nie wystarczy bierna znajomość.

Kod, który już znamy na wylot, przepiszmu 1-1 na F#.

***

<!-- .slide: data-background="./img/he-man.jpg" data-background-size="contain" -->
## Mocy przybywaj!

Note:

Startujemy projekt! Klamka zapadła, piszemy w F#.

W tej części opowiem nie o małym 2-tygodniowym projekcie, tylko o czymś co powstawało dobrych kilka miesięcym, zatem zupełnie inna skala problemu.

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

Note:

- Zamiast kontenera świetnie sprawdzają się funkcje wyższego rzędu i częściowa aplikacja.
- Jeszcze lepiej minimalizować użycie powyższych i gros logiki umieszczać w czystych funkcjach. Oddzielać czystą logikę od efektów ubocznych i kompozycji. Wyrażać efekty deklaratywnie (unie). Jeśli nie będziemy tego robić, to kompozycja będzie nas bolała. Polecam wykłady Marka Seemanna.
- CompositionRoot/konfigurację kontenera należy testować (żeby nie wyszło iż np. strzela do bazy).
- Kod F# jest dużo bardziej skondensowany/naładowany treścią - dlatego powinien być krótki - 100 LoC F# = 1000+ C#

---

<!-- .slide: data-background="#0077bd" -->
### Zmiana przyzwyczajeń
#### Ukrywanie informacji

- Dlaczego ukrywamy? Bo chronimy stan. Wróć!
- Często struktury wychodzą proste: listy, krotki
- ...lub kod jest generyczny
- W razie Niemca: prywatne unie i sygnatury

Note:

- Ukrywanie informacji to podstawa w OOP/C#. Tu też, ale inaczej.
- Ukrywanie objawia się natomiast w tym, że przekazujemy minimum informacji do funkcji (co jest łatwiej robić, tworzyć DTO per funkcja).

```fsharp
module EmailAddress
	// string representation is hidden
	type EmailAddress = private EmailAddress of string
	let create s = EmailAddress s
	let toString (EmailAddress s) = s
```

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

Note:

Życie programisty nie jest usłane różami. Pewne rzeczy sprawiały nam sporo trudności.

- Oczywista, oczywistość albo rozczarowanie. F# to nie panaceum. Oprócz składni, trzeba znać SOLID/CleanCode/wzorce/architektury.
- Najpierw kod z adnotacjami, które usuwamy. W miarę zdobywania doświadczenia odwrotnie: brak typów, a na koniec dodajemy tu i ówdzie dla czytelności (szczególnie w publicznym API)
- krotki są dobre na krótkim zasięgu, w publicznym API nie
- rekurencja w końcu "klinie", ale często nie jest potrzebna: przetwarzanie strumieniowe, fold

---

<!-- .slide: data-background="#0077bd" -->
### Kompromisy (wpisz swoje)

Nie wszystko musi/może być innowacyjne:

- Suave/WebSharper/Fable vs. WebApi/Owin/JavaScript/RiotJs
- HTTP/REST vs. WCF
- EventStore vs. pliki vs. SQL Server
- ...

Ale była zabawa! I się działo!

Note:

Ograniczenia czasowe, pojemność mózgu i cache. Nie uczymy się na raz kilku technologi (nie w pracy).

W banku standardem jest WCF+certyfikaty+monitoring.

Ale użyliśmy dużo agentów i Rx-a, type-providerów. I tak był fun!

---

<!-- .slide: data-background="#0077bd" -->
### Functional Pit of Success

- Domyślnie wszystko jest takie jak być powinno
- Type inference to - jednak - biała magia
- Agenci + *async* rządzą!
- Typy danych pozwalają - wreszcie! - dobrze modelować domenę
- Zasady SOLID/CleanCode nadal obowiązują tylko łatwiej ich przestrzegać
- Architektura Port & Adapters "sama" wychodzi

Note:

- Brak null, immutable
- Czyli jak zjeść ciastko (lekkość języków dynamicznych) i mieć ciastko (bezpieczeństwo języków statycznie typowanych) + automatyczna generalizacja
- żadnych wątków i locków
- "Wzorce projektowe kompensują za braki w języku". Koszt _dobrego_ kodu jest duużo mniejszy
- Odsyłam do Ian Coopera i Marka Seemanna. To logika biznesowa dyktuje warunki, a nie wykorzystane technologie.

---

<!-- .slide: data-background="#0077bd" -->
### Inne objawy

- Programiści zakochani w F# po uszy
- Trudno się oderwać od kodowania
- Objawy funkcyjnego przegięcia
- Nieustające dyskusje o kodzie

Note:

Roześmiane japy i błyszczące oczy. Stoisz w drzwiach w kurtce, gadasz o kodzie przez pół godziny, po czym rozbierasz się i wracasz do kodowanie. Nie jest to częsty widok w korpo.

Przy obiedzie, przy kawie. Nie pamiętam takiej ekscytacji.

To na doprowadziło do końca.

***

<!-- .slide: data-background="./img/castle.gif" -->
## The End

I żyli długo i szczęśliwie...

&nbsp;

&nbsp;

&nbsp;

> „Of all the words of mice and men, the saddest are 'It might have been.'” -- Kurt Vonnegut

Note:

Słodko-gorzki finał. Sukces, wejście na produkcję ku zadowoleniu wszystkich: programistów, Product Ownera i użytkowników.

Tylko nie nastąpił dalszy ciąg, bo... w nowym roku biznes przegrał bitwę o manday-e. Priorytety banku się zmieniły, obcięto budżet na dalszy ciąg, zabrano człowieka.. Który odchodził ze łzami w oczach do Angulara (złoooo). Kto by chciał w Angularze jak może w F#.

Ja zrealizowałem swoje marzenie, a teraz pora na następne!

***

# Pytania