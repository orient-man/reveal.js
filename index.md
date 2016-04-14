## Funkcyjne zabawki w obiektowej piaskownicy

Marcin Malinowski

- Twitter: [@orientman](https://twitter.com/orientman)
- GitHub: https://github.com/orient-man
- Blog: https://orientman.wordpress.com/

Note:

Zacznę tam, gdzie kończy się "Czysty kod" Wujka Boba. Punktem startu będzie najczystszy możliwy kod obiektowy, którypoprawię, a może nawet wywrócę na nice. Jak daleko powinniśmy się posuwać przekształcając kod obiektowy na funkcyjny? Jakie kompromisy wynikają z (nad)użycia języka obiektowego do funkcyjnego programowania? Co kryje się za co raz silniejszym przenikaniem paradygmatu funkcyjnego do języka C# (bezwstydnie ściągającego od swojego młodszego brata - F#)? Jakie funkcyjne zabawki przyniosą nam przyszłe wersje języka C#?

---

## O mnie

- Tata^2, mąż humanistki, mól książkowy, uparciuch, programista, konferencjoholik.  Don Kichot walczący z entropią. Kocha sprzeczności i humor. Wierzy w przypadek. Piwny filozof. W nielicznych wolnych chwilach harata w gałę (na bramce).

- Basic, Turbo Pascal/C, Assembler, Clipper, MS Access, Visual Basic, Java-XML :), C++, C#, JavaScript, F#...  i ze wszystkiego miałem frajdę, ale nie za wszystkim tęsknię.

- Absolwent informatyki i matematyki na UW. Ekspert IT w mBanku.

***

## Spis rzeczy

Spojrzenie...

1. ...do cudzego ogródka (Java)
2. ...za siebie (C# 1-6)
3. ...przed siebie (C# 7+)
6. ...z lotu ptaka

***

## Na początku Bóg stworzył obiekty

<!-- .slide: data-background="./images/book.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->

<!-- .element: class="fragment" -->
![Clean Code](./images/clean_code.jpg)

- Dobry prezent dla każdego nowego programisty w zespole
- Opublikowana na początku 2007r.
- Rozdział 14: refaktoring programu Args
- Port 1-1 z Javy do C# i co dalej?

---

## DEMO: Args w C# ##

Note:

Co możemy nabroić przy pomocy tych funkcyjnych zabawek?

- dobre OOP, unit testy, top-down, krótkie metody, dobre nazwy, SRP, łatwo rozszerzalny
- Alt-Enter i do przodu!
- lambdy i factory method (na górę kod, który będzie rozszerzany)
- ``Get<T>`` zamiast GetDouble... (nadal nie podoba mi się object)
- 1 zamiast 5 "zmiennych" instancji
- "zmienna", a raczej wartość bo się nie zmienia
- pure functions
- klasa Args stała się "workiem" na funkcje
- marshaller też jest w zasadzie funkcją
- IEnumerator jedynym stanem

---

<!-- .slide: data-background="./images/spices.jpg" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->

## Kod przyprawiony funkcyjnie

Zalety:

- mniej stanu, mniej drapania się po głowie (likwidacja "zmiennych zmiennych" i nielokalnych)
- o działaniu programu można wnioskować z samych deklaracji typów danych i funkcji
- krócej/czytelniej: LINQ, generics, lambdy, var...

Wady:

- więcej parametrów funkcji (i długie deklaracje typów)
- niewygodne zwracanie więcej niż 1 wartości z funkcji (``IEnumerator``)

Note: Java '06 vs. C# '14 - bój był nierówny...

***

<!-- .slide: data-background="./images/features1.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->
## Teza: C# z każdą wersją zawiera coraz więcej "przypraw" funkcyjnych i to nie jest przypadek

Note:
- za chwilę: stronniczy przegląd zmian w języku C#

---

<!-- .slide: data-background="./images/features2.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->

## C# 2 (2005)

- Generics
- Nullable types and ?? operator
- Generators aka iterators
- Anonymous delegates
- Static classes
- ...

Note:
- Anonymous delegates: zalążek lambd
- Static classes: worki na funkcje

---

<!-- .slide: data-background="./images/features3.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->
## C# 3 (2007)

- LINQ
- Anonymous types
- Lambda expressions
- Local variable type inference (var)
- Object &amp; collection initializers
- Automatic properties
- ...

Note:

LINQ i wszystkie dobrodziejstwa z tego wynikające, przydatne same w sobie, a bez których LINQ-a by nie było.

---

<!-- .slide: data-background="./images/features4.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->
## C# 5.0 &amp; .NET 4.5 (2012)

- async / await
- ``IReadOnlyList<>``, ``IReadOnlyDictionary<>``...
- Microsoft.Bcl.Immutable

Note:
- możliwość wyrażenia (oznaczenia) intecji "niemodyfikowalności" przez użytkownika API
- BCL warto korzystać, szczególnie w scenariuszach współbieżnych, gdzie ważne jest unikanie locków...

---

## C# 6.0 (2015)
<!-- .slide: data-background="./images/features5.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->

- Readonly auto properties
- Static type using statements
- Exception filters
- Monadic null checking aka null propagator
- Method &amp; property expressions

Usunięte w ostatniej chwili z Preview:

- Primary constructors
- Declaration expressions
- Constructor type parameter inference

Note:
- skąd się to wzięło, kto nam tak język komplikuje?
- inne: semicolon operator: var y = (var x = Foo(); Write(x); x * x))
- finalnie w C# 6: https://github.com/dotnet/roslyn/wiki/New-Language-Features-in-C%23-6

***

## Unde malum?

![https://twitter.com/dsyme/status/409476721780334592](./images/donsyme.png)

Note:
- Skąd zło? Dlaczego nam ten język tak komplikują, że powoli zaczyna przypominać C++?
- Skąd autorzy czerpią inspiracje?

---

> Don Syme is the designer and architect of the F# programming language [...] Earlier, created generics in the .NET Common Language Runtime, including the initial design of generics for the C# programming language [...]

http://en.wikipedia.org/wiki/Don_Syme

Note:
- Można oowiedzieć "Australijski łącznik" przemycający idee z F# do C#
- To co zrobiłem w kodem obiektowym jest jak najbardziej w zgodzie z ewolucją C#

***

<!-- .slide: data-background="./images/fp-way-bg.jpg" -->

# C# 6

# Functional way is the right way

Note:
- Podejście funkcyjne to jedyne słuszne podejście!
- C# 6 miał być większą rewolucją niż się okazał...
- ...ale to co wyleciało z Preview zapowiada kierunek dalszych zmian

---

### Primary constructors / Readonly auto properties

F# dziś:
```fsharp
type Point(x, y) =
    member this.X = x
    member this.Y = y
```

C# 6 Preview - [Roslyn #6997](https://github.com/dotnet/roslyn/issues/6997):
```csharp
public class Point(int x, int y)
{
    private int x, y;
}
```

```csharp
public class Point(int x, int y)
{
    public int X { get; } = x;
    public int Y { get; } = y;
}
```

Note: konstruktory wyleciały prawd. z powodu planowanych rekordów, ale można inicjować w zwykłym konstruktorze

---

### C# 6 final

```charp
public class Customer
{
    public string Name { get; } // backing field is readonly

    public Customer(string first, string last)
    {
        Name = first + " " + last;
    }
}
```

---

### Static type using statements

F# dziś:
```fsharp
module Math =
    let Add x y = x + y

Math.Add 2 2
open Math
Add 2 2
```

C# 6:
```csharp
public static class Math
{
    public static int Add(int x, int y) { return x + y; }
}

using static Math;
Add(2, 2);

using static System.Console;
WriteLine("Hello World!");
```

Note:
- mała rzecz a cieszy
- czyli używajmy funkcji jak ludzie (funkcje na globalnym poziomie)

---

###  Declaration expressions (out var)

F# dziś:
```fsharp
let success, x = Int32.TryParse("123")
// lub
if (true, x) = Int32.TryParse("123") then ... else ...
// lub
match TryParse("123") with true, x -> ... | _ -> ...
```

C# 6 Preview ([Roslyn #6183](https://github.com/dotnet/roslyn/issues/6183)):
```csharp
if (int.TryParse("123", out var x))
    // x dostępne
else
    ...
```

---

### Exception filters

F# dziś:
```fsharp
type ErrorCode = | UnexpectedArgument | InvalidFormat
exception ArgsException of ErrorCode

try
    raise (ArgsException UnexpectedArgument)
with
  | ArgsException UnexpectedArgument -> printfn "Unexpected argument"
  | ArgsException _ -> printfn "Other parsing error"
```

C# 6:
```csharp
try
{
    throw new ArgsException(ErrorCode.UnexpectedArgument);
}
catch (ArgsException e)
    when (e.ErrorCode == ErrorCode.UnexpectedArgument) {...}
```

Note:
- Zostało jako namiastka pattern matchingu
- Też by się przydało w programie Args...

---

### Monadic null checking aka null propagator

F# dziś:
```fsharp
let (>>=) x y = Option.bind y x // generalnie mało przydatne
```

C# 6:
```csharp
int bestValue = points?.FirstOrDefault()?.X ?? -1;
int? first = customers?[0].Orders?.Count();
```

Note: magiczna nazwa, ale przydane w C# (w F# mniej - o null-a trzeba się postarać)
---

### Method &amp; property expressions (lambdas as definitions)

F# dziś: ha, ha - wolne żarty
```fsharp
member thix.Move x y = Point(X + dx, Y + dy)
member this.Distance = Math.Sqrt((X * X) + (Y * Y))
```

C# 6:
```csharp
public Point Move(int dx, int dy) => new Point(X + dx, Y + dy);
// property
public double Distance => Math.Sqrt((X * X) + (Y * Y));
```

***

<!-- .slide: data-background="./images/dexter.jpg" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->

## Tymczasem w laboratorium

C# 7 Design Meeting Notes:

> Let’s continue being inspired by functional languages, and in particular other languages – F#, Scala, Swift – that aim to mix functional and object-oriented concepts as smoothly as possible

https://github.com/dotnet/roslyn/issues/98

Note:
- Roslyn jest OpenSource i możemy śledzić proces powstawania nowej wersji
- Można sobie pobrać źródła kompilatora (z różnych branchy...)
---

### Pattern matching

C# dziś:
```csharp
var e = s as ExpressionStatement;
if (e != null) {
    var a = e.Expr as AssignmentExpressionSyntax;
    if (a != null) {
        var l = a.Left as IdentifierName;
        var r = a.Right as IdentifierName;
        if (l != null && r != null & l.Name.name == r.Name.name) ...
```
C# 7 (VS 15 Preview):
```csharp
if (s is ExpressionStatement(
        AssignmentExpressionSyntax(IdentifierName l, IdentifierName r))
    && l.name = r.name) ...
// lub
switch (s) {
case ExpressionStatement(
        AssignmentExpressionSyntax(IdentifierName l, IdentifierName r))
        when (l.name == r.name): ...
}
```

Note: pattern matching działa w VS, ale może nie do końca (składnia?)

---

### Rekordy

Rekord to niezmienna klasa o semantyce *value type*. Zamiast pisać:
```csharp
public class Point
{
    public Point(int x, int y) { this.X = x; this.Y = y; }
    public int X { get; }
    public int Y { get; }
    public override int GetHashCode() {...}
    public override bool Equals(...) {...}
    // New pattern-matching decomposition operator
    public static bool operator is(Point self out int x, out int y) {...}
}
```

Wystarczy:
```csharp
class Point(int X, int Y);
var p1 = new Point(15, 6);
var p2 = p1 with { Y = 21 }; // == new Point(p1.X, 21)
if (p1 is Point { X is 15, Y is int y }) ...
if (p2 is Point(int x, 21)) ...
```

Note: prawdopodobnie przez to wstrzymali się z głównymi konstruktorami

---

### Zastosowania rekordów

- proste, niemodyfikowalne typy danych (tworzone często *ad hoc*)
- DTOs
- zwracania wielu wartości z metody
- anonimowe typy o większym zasięgu
- symulacja algebraicznych typów danych bla, bla...

Note:
- recepta na zdiagnozowany psychologicznie przypadek lęku programistów przed tworzeniem nowych klas
- zwracanie wielu wartości w Args (zamiast Enumerator)

---

### Killer combo: rekordy + pattern matching

```csharp
abstract class Expr;
class X() : Expr;
class Const(double Value) : Expr;
class Mult(Expr Left, Expr Right) : Expr;
...
Expr Simplify(Expr e) {
  switch (e) {
    case Mult(Const(0), *): return Const(0);
    case Mult(*, Const(0)): return Const(0);
    case Mult(Const(1), var x): return Simplify(x);
    case Mult(var x, Const(1)): return Simplify(x);
    case Mult(Const(var l), Const(var r)): return Const(l*r);
    ...
  }
}
```

---
### Pattern matching w C# 6 ;-)

```csharp
public class Variable : Exception {
  public string Name { get; set; }
}
public class Add : Exception {
  public Exception Left { get; set; }
  public Exception Right { get; set; }
}

public static int Evaluate(Exception e, IDictionary<string, int> vars) {
  int res;
  try { throw e; }
  catch (Variable v) when (vars.TryGetValue(v.Name, out res)) { return res; }
  catch (Variable _) { throw new ArgumentException("Variable not found!"); }
  catch (Add a) { return Evaluate(a.Left, vars) + Evaluate(a.Right, vars); }
}
```

http://tomasp.net/blog/2015/csharp-pattern-matching/

---

### Tuples (krotki)

F# dziś:
```fsharp
let tally = List.fold (fun (sum, count) v -> (sum + v, count + 1)) (0, 0)
```

C# dziś:
```csharp
public void Tally(IEnumerable<int> values, out int sum, out int count) {...}
public Tuple<int, int> Tally(IEnumerable<int> values) {...}
```

C# 7 (pokazane na Build 2016):
```csharp
public (int sum, int count) Tally(IEnumerable<int> values) {
    return values.Aggregate(
        (sum: 0, count: 0), (r, v) => (r.sum + v, r.count + 1));
}

var t = Tally(myValues);
Console.WriteLine($"Sum: {t.sum}, count: {t.count}");
```

Note: wygodne w połączeniu z LINQ

---

### Immutable types

Wszystkie pola readonly:

```csharp
public readonly class Args
{ ...
```

Rekurencyjnie wszystkie pola readonly (faktycznie niezmienna klasa):

```csharp
public immutable class Args
{ ...
```

---

### Inne propozycje

#### Nullable and non-nullable reference types

```csharp
string? n; // nullable string
string! s; // non-nullable string

n = null; // Ok
s = null; // Error!

WriteLine(s.Length); // Ok
WriteLine(n.Length); // Error!
if (n is string! ns) WriteLine(ns.Length); // Ok
```

#### REPL (read-eval-print-loop) i skryptowanie

Wyobraź sobie [scriptcs](http://scriptcs.net/) wbudowany w VS, zintegrowany z Debuggerem i zastępujący "immediate window"...

Note: lepszy REPL jest już w VS 2015 update 1

***

## Podsumowanie

<!-- .slide: data-background="./images/podsumowanie.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->

 - <!-- .element: class="fragment" --> C# czerpie pełnymi garściami z języków funkcyjnych
 - <!-- .element: class="fragment" --> ...mimo to zawsze pozostanie w kategorii "OOP first"
 - <!-- .element: class="fragment" --> ...jednak przyprawy funkcyjne mogą całkowicie zmienić smak potrawy

<!-- .element: class="fragment" --> Żyjemy w ciekawych czasach :)

Note:

 - FP jest trudne, może boleć głowa ;)
 - nie chodzi o to bym Was nauczył, a zainspirować: programowanie jest fajne!

***

![Rękopis znaleziony w Saragossie](./images/rekopis.jpg)

***

## Bibliografia

- Książka: [Real-World Functional Programming: With Examples in F# and C# - Petricek & Skeet](http://www.amazon.com/Real-World-Functional-Programming-With-Examples/dp/1933988924)
- [Don Syme - .NET/C# Generics History](http://blogs.msdn.com/b/dsyme/archive/2011/03/15/net-c-generics-history-some-photos-from-feb-1999.aspx)
- [C# 7 Desing Notes](https://github.com/dotnet/roslyn/labels/Design%20Notes)
- Video: [The Future of C# @ Build 2016](https://channel9.msdn.com/Events/Build/2016/B889)
- [Why Functional Programming Matters](http://www.cse.chalmers.se/~rjmh/Papers/whyfp.html)
- [John Carmack - In-depth: Functional programming in C++](http://gamasutra.com/view/news/169296/Indepth_Functional_programming_in_C.php)

Materiały:

- Slajdy: http://orient-man.github.io/getnet2016
- Źródłowce: https://github.com/orient-man/CleanArgs

***

# Aaa... pytania?

Ankieta: https://www.surveymonkey.com/r/MTJP2HR Pls!

![Ankieta QR Code](./images/ankieta-qrcode.png)

Note: http://goqr.me/
