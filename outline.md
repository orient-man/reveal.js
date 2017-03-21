Rok niebezpiecznego życia, czyli F# na produkcji - Outline
===

## Wstęp: moja historia ("story arc")

### Wielka Depresja (kontekst)

Po pierwszym miodowym miesiącu w nowej pracy nadszedł _kryzys_. Przyszłość wydawała się
sprowadzać do 3 rodzajów aktywności:

1. Usprawnianiu i łataniu dziur w wielkich gmachach aplikacji postawionych przez rzesze bezimiennych autorów (dosłownie, bo ktoś uciął historią przy migracji z SVN!).
1. Uczestniczeniu w nasiadówkach, na których jako "Pan Ekspert" miałem _ex catedra_ planować świetlaną przyszłość. W rzeczywistości dyskutować nad (bezsensownymi) kwestiami w rodzaju:
   * "Czy zatrudniać programistów tylko do pisania testów automatycznych?"
   * "Jedno repozytorium czy wiele?"
   * "Kupować drogie narzędzie od IBM (Rational Test Virtalization Server) do testów end-to-end czy nie?"
1. Gaszeniu pożarów na produkcji - co bywa ciekawe, ale jednak lepiej zapobiegać...

Słowem: sytuacja nie była różowa. A przecież mogło być tak fajnie:

* ciekawa domena (rynek walutowy, Hedge Accounting czyli rachunkowość zabezpieczeń)
* i naprawdę niegłupi ludzie zarówno w IT, jaki i w biznesie

Chciałem _zrobić różnicę_ - tylko jak?

I wtedy pojawiła jutrzenka nadziei: biznes wyszedł z pomysłem na _Nowy System_ z nietrywialną logiką (zerro CRUD-a!).

### Wyzwania

* Jak nie wejść po raz drugi do tej samej rzeki i nie popełnić błędów poprzedników? (monolit + kod spaghetti)
* Od kilku lat zajmowałem się programowaniem funkcyjnym: i w pracy, i jako prelegent. Niemniej, używałem do tego celu jedynie języka C# i nie mogłem pochwalić się nawet linijką kodu produkcyjnego napisanego w F#. Jak przekonać innych do nowego języka, który nie był do tej pory używany w banku?
* Będąc jedyną osobą w zespole znającą F# - i to w stopniu początkującym - musiałem nauczyć go innych. Jak to zrobić szybko?
* Co trzeba zrobić, aby F# stał się w ogóle dostępną opcją z punktu widzenia naszych procesów Continous Delivery (kompilacja, paczkowanie, instalacja, badanie jakości kodu)?

### Dostępne rozwiązania (plan gry)

Szczęście nam sprzyjało, bo korporacyjne młyny mielą powoli (analiza czy się opłaci, wykonalności, budżet, dostępność zespołu) i faktyczny start prac miał nastąpić za co najmniej 2 miesiące.

Wstępne założenia - niezwiązane z F# - "oczywiste oczywistości", ale w świecie korpo rewolucyjne:

TODO: slajd "captain Obvious"

1. Nie dodajemy kolejnego modułu do istniejacego systemu tylko robimy "mikroserwisy"
1. Nie powiekszamy długu technologicznego rozszerzając istniejący GUI (WinForms), ale tworzymy nowy (Web/SPA)
1. Minimalizujemy użycie wewnętrznych frameworków
1. Stosujemy Test Driven Developement i piramidę testów
1. Stosujemy podejście iteracyjne i wchodzimy na produkcję z Minimum Viable Product niezależnie od bankowych "big-bangowych" release-ów

To wszystko oczywiście nie w kontrze do banku, ale jak najbardziej w zgodzie ze "strategią IT"

Teraz był czas na przemyślenie rozwiązania i prototypy "Proof-of-Concept". Decyzja o użyciu F# została odłożona.

O tym co było dalej jest ta prezentacja.

TODO...

## "Mięcho" (takeaways)


### Trudne - ludzkie - problem ("hardware")

Trzeba przekonać decydentów i interesariuszy.

#### Kim są Oni?

Przede wszystkim:
 * inni programiści (z Twojego zespołu)
 * menedżer

W zależności od firmy także:
 * analitycy
 * testerzy
 * "nieprogramujący architekt"
 * biznes

Należy pamiętać, że _styczność z kodem mają nie tylko programiści_. Kod jest przede wszystkim czytany (i pod tym kątem należy go optymalizować). A często czytają go również analitycy i testerzy, a czasem również menedżerzy (ex programiści) lub nawet biznes!

Wszyscy oni będą zmuszeni do nauczenia się - choćby w stopniu podstawowym - nowego języka.

#### Idź, ewangelizuj!

Ewangelizacja na każdym kroku (do znudzenia):
 * podrzucaj przykłady firm, które używają F# (jet.com etc.) i inne "success stories"
 * F# jako magnes przyciągający talenty!
 * podrzucaj linki do prezentacji
 * entuzjazm jest zaraźliwy!
 * nie zrażaj się negatywnymi opiniami (ludzie boją się zmian, czasem ktoś ma zły dzień...)

Historyjka:

W moim przypadku F# nie był zupełnie nieznany. Najbardziej popularny jest właśnie w brażny finansowej i nawet ludzie z biznesu o nim słyszeli (generalnie są otrzaskani, bo sami programują np. robią modele w R, aplikacje w Accessie i inne). *Podesłanie linków do prezentacji F# w finansach nie zaszkodziło*.

#### Zrób szkolenie!

Wystarczą podstawy. Jądro F# jest naprawdę proste i eleganckie. Otwieramy VSCode (w moim przypadku VIM) i wio:

 * funkcje
 * typy: krotki, rekordy, listy i sekwencje
 * unie dyskryminowane
 * dopasowywanie wzorca
 * operator "pipe" czyli składnia "fluent"
 * ...

Warto zwrócić uwagę na relację tych konstrukcji do C#.

Na koniec realistyczny przykład z waszej domeny prezentujący podejście _Type_ Driven Development.

Historyjka: _W moim przypadku materiału miałem na 45 minut, ale szkolenie przerodziło się w żywą 3h dyskusję o różnych aspektach programowania funkcyjnego._

[Przykładowy kod do szkolenia](https://gist.github.com/orient-man/14e9a9780de4d97239aa8d94ce944db8)

Do kwestii nauki będę jeszcze kilka razy wracał. Ważne: takie szkolenie jest może nawet bardziej wartościowe dla prowadzącego.

#### O polityce i odpowiedzialności

 * dobrze zacząć od sukcesu
 * trzeba dzielić się nawet drobnymi sukcesami
 * trzeba umieć wziąć na siebie odpowiedzialność: pomogać, uspokajać, wziąć na klatę

TODO...

Na koniec anegdota:

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

### Łatwe - techniczne - problemy ("software")

#### Po kolei, krok za krokiem

TODO...

 * FAKE
 * Build process:
   * Kompilator F# na build serwerze
   * zależność od paczki FSharp.Core zamiast z GAC
   * wszystkie potrzebne paczki w feedzie firmowym
   * czy jakieś skrypty CI bazują na *.csproj?
   * integracja z SonarQube (TODO)
     * problemy z dotCover
     * starsze wersje NUnit zachowują się dziwnie...
 * pierwszy kod: unit testy
   * zwięzłe i czytelne
   * testy są/powinny być proste - dobry poligon do nauki składni
   * na początek drobne smaczki: długie nazwy testów, "use", asercja FsUnit
   * z czasem odkrywamy: FsCheck, Unqoute i łatwość tworzenia własnych DSL-i (TODO: przykład?)
 * pierwszy moduł
   * FSharpInterop (Func vs FSharpFunc, Option)
   * funkcyjny kod w obiektowej polewie (do konsumpcji przez C#/kontener DI)
   * Event interop (boli głowa)
   * ważne, żeby nie poddać się w tym momencie (współpraca z C# to najmniej przyjemna część)
 * pierwsza aplikacja
   * kod będzie w stylu OOP (niespodzianka!)
   * najlpiej mała, bo będziesz chciał ją przepisać za 3-mce :)
 * inne:
   * dobre ćwiczenia na boku: to przepisać istnijącą małą aplikację 1-1, a potem iteracyjnie poprawiać
   * wszystkie prototypu, PoC etc.
   * warto dzielić się każdym, nawet drobnym odkryciem

## Proces ("learning process")

Czyli, czegośmy się nauczyli w trakcie projektu...

### Stopniowe pozbywanie się "obiektowych" przyzwyczajeń

#### Kompozycja albo Dependency Inversion

 * można żyć bez kontenera DI
 * w tej roli świetnie sprawdzają się funkcje wyższego rzędu i częściowa aplikacja
 * jeszcze lepiej minimalizować użycie powyższych i gros logiki umieszczać w czystych funkcjach
 * kompozycję (CompositionRoot) również należy testować i trzymać na ciągłej diecie

#### Ukrywanie informacji

W OOP to podstawa, ale w FP/F# jest... inaczej:

 * ukrywamy struktury bo nie chcemy, aby ktoś niepowołany zmienił stan
 * co gdy nie ma stanu, bo wszystko jest niezmienne (immutable)?
 * w FP/F# oddzielamy logikę od struktur danych - często prostych (listy, krotki)
 * przy złożonych strukturach można użyć prywatnych unii lub sygnatur (plików *.fsi)
 * nie jest to jednak tak często potrzebne

```fsharp
module EmailAddress
	// string representation is hidden
	type EmailAddress = private EmailAddress of string
	let create s = EmailAddress s
	let toString (EmailAddress s) = s
```

### Przestrogi okupione krwią, potem i łzami

 * zły kod da się pisać w każdym języku!
 * kod który napiszesz w pierwszych miesiącach nauki języka będzie zły choćby nie wiem co
 * brak typów podanych explicite i komunikaty kompilatora na początku nie pomagają
   * adnotacja z typami warto pozostawić na poziomie API pomiędzy modułami
 * trzeba walczyć z pokusą nadużywania operatorów: |>, <|, >>, List.filter ((<=) 5) etc.
 * zbyt wiele funkcyjnych parametrów boli (patrz DI)
 * nie wszystko jest krotką albo listą (rekordy!, unie!)
 * rekurencja nie zawsze jest naturalna (ale jak już fold kliknie!)
 * nic nie poradzę: nie lubię części OOP w F# - niby to samo co C#, ale inaczej - czasem konieczne, ale przez 90% czasu nie (F# Good Parts)

### Życie to sztuka kompromisu

Nie wszystko musi/może być innowacyjne. M.in. ze względów czasowych, wymagań niefunkcjonalnych i operacyjnych:

 * Nie użyliśmy Suave/WebSharper/Fable, ale WebApi/Owin/JavaScript/RiotJs
 * Zamiast HTTP/REST użyliśmy WCF (standard w banku)
 * Mimo wybitnie pasującego problemu nie użyliśmy EventStore, ale własnej - "wystarczająco dobrej" - implementacji

Za to użyliśmy i sprawdziło się: agentów (MailboxProcessor), FSharp.Control.Reactive, FSharp.Data...

### Kawałki układanki zaczynają do siebie pasować

Po jakimiś czasie nadchodzi nirwana ("Functional Pit of Success"):

 * domyślnie wszystko jest takie jak powinno być (immutability, brak null)
 * type inference to - biała - magia
 * automatyczna generalizacja jest f-a-n-t-a-s-t-y-cz-n-a
 * agenci (MailboxProcessor) + async rządzą!
 * algebraiczne typy danych pozwalają - wreszcie! - dobrze modelować domenę
 * zasady SOLID/CleanCode nadal obowiązują tylko łatwiej ich przestrzegać
 * naturalnie dążymy do architektury Port & Adapters (heksagonalnej) z "core domain" w środku

TODO: rozwinąć wątek Ports & Adapters??
TODO: rozmiary plików, modułów...

Inne objawy: trudno oderwać się od kodowania, nieustające dyskusje o kodzie, roześmiane japy i błyszczące oczy ;-).

F# prawie u wszystkich programistów wywołuje miłość od pierwszego wejrzenia - po roku i "konsumpcji" - jest to już trwały związek.

## Podsumowanie

I żyli długo i szczęśliwie... Niestety finał jest słodko-gorzki - jak to w życiu:
 * System jest na produkcji ku ogólnemu zadowoleniu - Yupi!
 * Dostałem za niego roczną nagrodę $$$
 * Ale... nasz biznes przegrał coroczną "bitwę o mendeje", budżet się skurczył i na razie nie ma dalszego ciągu...
 * Kolega został wypożyczony do zespołu rzeźbiącego w Angularze 2/C# nowy system o Najwyższym Priorytecie i odchodząc miał prawie łzy w oczach
 * Zespół wrócił do utrzymywania monolitów (ale z użyciem F#!)
 * Oczy koleżanki już tak się nie świecą na myśl o pracy
 * A ja... odszedłem do startup-u

Trzeba realizować swoje marzenia. Ja jedno spełniłem i teraz przyszła pora na następne! To był wspaniały rok!

Nikt za Was marzeń nie zrealizuje:

> Of all the words of mice and men, the saddest are 'It might have been.' -- Kurt Vonnegut