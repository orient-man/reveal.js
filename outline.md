# Rok niebezpiecznego życia, czyli F&#35; na produkcji - Outline

## Moja historia ("story arc")

### Kontekst

Po pierwszych miodowym miesiącu w nowej pracy nadszedł kryzys. Przyszłość wydawała się
sprowadzać do 3 aktywności:

1. Usprawnianiu i łataniu dziur w wielkich gmachach aplikacji postawionych przez rzesze bezimiennych autorów (dosłownie, bo ktoś uciął historią przy migracji z SVN!).
1. Uczestniczeniu w nasiadówkach, na których jako "Pan Ekspert IT" miałem ex catedra planować świetlaną przyszłość. W rzeczywistości dyskutować nad kwestiami w rodzaju (bez sensu!):
   * czy zatrudniać programistów tylko do pisania testów automatycznych?
   * jedno repozytorium czy wiele?
   * kupować drogie narzędzie od IBM (Rational Test Virtalization Server) do testów end-to-end czy nie?
1. Gaszeniu pożarów na produkcji - co bywa ciekawe, ale jednak lepiej zapobiegać...

Słowem: sytuacja nie była różowa. A przecież mogło być tak fajnie:

* ciekawa domena (rynek walutowy, Hedge Accounting czyli rachunkowość zabezpieczeń)
* i naprawdę niegłupi ludzie zarówno w IT, jaki i w biznesie

Chciałem "zrobić różnicę" - tylko jak?

I wtedy pojawiła jutrzenka nadziei: biznes wyszedł z pomysłem na nowy system z nietrywialną logiką (zero CRUD-a!).

### Wyzwania

* Jak nie wejść jeszcze raz do tej samej rzeki i nie popełnić błędów poprzedników? (monolit + kod spaghetti)
* Od kilku lat zajmowałem się programowaniem funkcyjnym: i w pracy, i jako prelegent. Niemniej używałem do tego celu jedynie języka C# i nie mogłem się pochwalić nawet linijką kodu napisanego w F#. Jak przekonać innych do nowego języka, który nie był do tej pory używany w banku?
* Będąc jedyna osobą w zespole znającą F# - i to w stopniu początkującym - musiałem nauczyć go innych. Jak to zrobić szybko?
* Co trzeba zrobić, aby F# był dostępną opcją z punktu widzenia naszych procesów Continous Delivery (kompilacja, paczkowanie, instalacja)?

### Dostępne rozwiązania (plan)

Szczęście nam sprzyjało, bo korporacyjne młyny mielą powoli (analiza czy się opłaci, budżet, dostępność zespołu) i faktyczny start prac nastąpić za 2 miesiące.

Wstępne założenia - nie związane z F# - "oczywiste oczywistości", ale w świecie korpo rewolucyjne:

1. Nie dodajemy kolejnego modułu do istniejacego systemu tylko robimy "mikroserwisy"
1. Również nie powiekszamy długu technologicznego rozszerzając istniejący GUI (WinForms), ale tworzymy nowy (Web/SPA)
1. Minimalizujemy użycie wewnętrznych frameworków
1. Stosujemy Test Driven Developement i piramidę testów
1. Stosujemy podejście iteracyjne i wchodzimy na produkcję MVC niezależnie od bankowych "big-bangowych" release-ów

Był czas na przemyślenie rozwiązania i prototypy "Proof-of-Concept". Decyzja o użyciu F# została odłożona.

O tym co było dalej, jest ta prezentacja.

TODO...

### Rezultaty (takeaways)

...

## Podsumowanie

...
