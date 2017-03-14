## Rok niebezpiecznego życia, czyli F# na produkcji

<!-- .slide: data-background="#e41e0a" -->
<!-- .slide: data-background="#18a035" -->
<!-- .slide: data-background="#0077bd" -->
<!-- .slide: data-background="#f39100" data-background-transition="zoom" -->
<!-- .slide: data-background="rgb(77, 126, 101)" -->
<!-- .slide: data-background="#cc0b18" -->
<!-- .slide: data-background="#f39100" -->
<!-- .slide: data-background="rgb(181, 83, 60)" -->

Marcin Malinowski

- Twitter: [@orientman](https://twitter.com/orientman)
- GitHub: https://github.com/orient-man
- Blog: https://orientman.wordpress.com/

Note:

Jak wejść z F# na produkcję i pozostać przy życiu. Moje doświadczenia z wprowadzania języka F# w dużym banku. Recepta krok po kroku jak rozwiązywać łatwe - techniczne - problemy i trudne - międzyludzkie. Czyli wszystko co chcielibyście wiedzieć, ale boicie się zapytać.

---

## O mnie

- Tata^2, mąż humanistki, mól książkowy, uparciuch, programista, konferencjoholik.  Don Kichot walczący z entropią. Kocha sprzeczności i humor. Wierzy w przypadek. Piwny filozof. W nielicznych wolnych chwilach harata w gałę (na bramce).

- Basic, Turbo Pascal/C, Assembler, Clipper, MS Access, Visual Basic, Java-XML :), C++, C#, JavaScript, F#...  i ze wszystkiego miałem frajdę, ale nie za wszystkim tęsknię.

- Absolwent informatyki i matematyki na UW. Ekspert IT w mBanku.

Note:

TODO: skrócić / nie pokazywać...

***

## Agenda

1. Wait but why?
2. But how?
3. Learning process
4. Am I in heaven?

***

## "Dania na wynos"

* Praktyczne rady jak się do tego zabrać
* TODO

***

## Kontekst

* F# jest świetny i usycham z pragnienia, aby w nim programować
* Niestety nie wszystko ode mnie zależy...
* ...albo chciał(a)bym, ale boje się

---

## Ale co właściwie chcemy osiągnąć?

Functional "pit of success"?

***

## Wdrażamy! Ale jak?

* Łatwe: ogarnięcie technicznych problemów
* Trudne: ludzie

***

## Pierwsze koty za płoty: FAKE

* Statycznie typowane skrypty budujące! +1
* Super zwięzłe, super proste +2
* ...prawdopodobnie nikt nam nie zabroni
* ...a że większość skryptów w MSBuild/PowerShell ssie to łatwo o sukces :)

---

## FAKE: Start

```fsharp
#r "packages/FAKE/tools/FakeLib.dll"
open Fake
let projects = !! "src/**/*.*sproj"
Target "Clean" (fun _ -> CleanDirs ["./build/"])
Target "Build" (fun _ ->
    MSBuild  "./build/" "Build" [] projects
    |> Log "Build-Output: ")

"Clean" ==> "Build"
RunTargetOrDefault "Build"
```

---

## FAKE: ...

---

## Unit testy

* ``długie nazwy testów``
* zwięzłe
* inline classes
* FsUnit
* FsCheck
* Unqoute (raises, list =! list)
* "use Fixture"
* easy to write DSLs

Note:

* Testy są dobre do nauki
* Mają określoną strukturę AAA
* Na ogół są - powinny być - proste
* Przykłady testów

---

```fsharp
[<Test>]
let ``reversing updated deal`` () =
    FxAgentState.empty
    ++ { deal with Amount = 10m; DealId = "A" }
    ++ { deal with Amount = 15m; DealId = "A"; Id = "xyz" }
    -- "xyz"
    |> getPositionChanges
    =! [[10m]; [-10m; 15m]; [-15m]]
```

---
## Więcej

* Build Process
* Pierwszy moduł
    * FSharpInterop, FuncConvert.ToFSharpFunc
    * Wrapping classes
    * Func vs FSharpFunc

***

## Hard part: People

* Who they are?
* How to convince them?
* How to teach them?
* This is Team Work!
* Be proud & responsible

***

***

## Learning Process

* Embracing functional thinking and loosing OOP habits
* Take it easy
* Things that can slow you down
* 3x practice

##
