Rok niebezpiecznego życia, czyli F# na produkcji - Outline
===

## Wstęp: moja historia ("story arc")

### Kontekst

Po pierwszym miodowym miesiącu w nowej pracy nadszedł _kryzys_. Przyszłość wydawała się
sprowadzać do 3 rodzajów aktywności:

1. Usprawnianiu i łataniu dziur w wielkich gmachach aplikacji postawionych przez rzesze bezimiennych autorów (dosłownie, bo ktoś uciął historią przy migracji z SVN!).
1. Uczestniczeniu w nasiadówkach, na których jako "Pan Ekspert IT" miałem ex catedra planować świetlaną przyszłość. W rzeczywistości dyskutować nad kwestiami w rodzaju (bez sensu!):
   * czy zatrudniać programistów tylko do pisania testów automatycznych?
   * jedno repozytorium czy wiele?
   * kupować drogie narzędzie od IBM (Rational Test Virtalization Server) do testów end-to-end czy nie?
1. Gaszeniu pożarów na produkcji - co bywa ciekawe, ale jednak lepiej zapobiegać...

Słowem: sytuacja nie była różowa. A przecież mogło być tak fajnie:

* ciekawa domena (rynek walutowy, Hedge Accounting czyli rachunkowość zabezpieczeń)
* i naprawdę niegłupi ludzie zarówno w IT, jaki i w biznesie

Chciałem _zrobić różnicę_ - tylko jak?

I wtedy pojawiła jutrzenka nadziei: biznes wyszedł z pomysłem na nowy system z nietrywialną logiką (zero CRUD-a!).

### Wyzwania

* Jak nie wejść po raz drugi do tej samej rzeki i nie popełnić błędów poprzedników? (monolit + kod spaghetti)
* Od kilku lat zajmowałem się programowaniem funkcyjnym: i w pracy, i jako prelegent. Niemniej, używałem do tego celu jedynie języka C# i nie mogłem pochwalić się nawet linijką kodu produkcyjnego napisanego w F#. Jak przekonać innych do nowego języka, który nie był do tej pory używany w banku?
* Będąc jedyną osobą w zespole znającą F# - i to w stopniu początkującym - musiałem nauczyć go innych. Jak to zrobić szybko?
* Co trzeba zrobić, aby F# stał się w ogóle dostępną opcją z punktu widzenia naszych procesów Continous Delivery (kompilacja, paczkowanie, instalacja, badanie jakości kodu)?

### Dostępne rozwiązania (plan)

Szczęście nam sprzyjało, bo korporacyjne młyny mielą powoli (analiza czy się opłaci, wykonalności, budżet, dostępność zespołu) i faktyczny start prac miał nastąpić za co najmniej 2 miesiące.

Wstępne założenia - nie związane z F# - "oczywiste oczywistości", ale w świecie korpo rewolucyjne:

1. Nie dodajemy kolejnego modułu do istniejacego systemu tylko robimy "mikroserwisy"
1. Również nie powiekszamy długu technologicznego rozszerzając istniejący GUI (WinForms), ale tworzymy nowy (Web/SPA)
1. Minimalizujemy użycie wewnętrznych frameworków
1. Stosujemy Test Driven Developement i piramidę testów
1. Stosujemy podejście iteracyjne i wchodzimy na produkcję z Minimum Viable Product niezależnie od bankowych "big-bangowych" release-ów

Teraz był czas na przemyślenie rozwiązania i prototypy "Proof-of-Concept". Decyzja o użyciu F# została odłożona.

O tym co było dalej jest ta prezentacja.

TODO...

## "Mięcho" (takeaways)

### Łatwe - techniczne problemy - "software"

### Trudne - ludzkie - "hardware"

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
 * przykłady firm, które używają F# (jet.com etc.) i inne "success stories"
 * linki do prezentacji
 * entuzjazm jest zaraźliwy!

Historyjka:

W moim przypadku F# nie był zupełnie nieznany. Najbardziej popularny jest właśnie w brażny finansowej i nawet ludzie z biznesu o nim słyszeli (generalnie są otrzaskani, bo sami programują np. robią modele w R, aplikacje w Accessie i inne). *Podesłanie linków do prezentacji F# w finansach nie zaszkodziło*.

#### Zrób szkolenie!

Wystarczą podstawy. Jądro F# jest naprawdę proste i eleganckie. Otwieramy VSCode (w moim przypadku VIM) i wio:

 * funkcje
 * typy: krotki, rekordy, listy i sekwencje
 * unie dyskryminowane
 * dopasowywanie wzorca
 * operator "pipe" czyli składnia "fluent"

Warto zwrócić uwagę na relację tych konstrukcji do C#.

Na koniec realistyczny przykład z waszej domeny prezentujący podejście Type Driven Development.

Historyjka: _W moim przypadku materiału miałem na 45 minut, ale szkolenie przerodziło się w żywą 3h dyskusję o różnych aspektach programowania funkcyjnego._

[Przykładowy kod do szkolenia](https://gist.github.com/orient-man/14e9a9780de4d97239aa8d94ce944db8)

Historyjki: błyszczące oczy i smutek przy odejściu... (??)

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

## Proces ("learning process")

## Podsumowanie

Historyjka: nagroda na odejście

Nie czekajcie aż ktoś zrobi to za was!

> Of all the words of mice and men, the saddest are 'It might have been.' -- Kurt Vonnegut