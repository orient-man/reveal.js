## Funkcyjne zabawki w obiektowej piaskownicy

Marcin Malinowski

- Twitter: [@orientman](https://twitter.com/orientman)
- GitHub: https://github.com/orient-man
- Blog: https://orientman.wordpress.com/

Note:

Wiedza o tym, skąd autorzy języka C# czerpali inspiracje, jakie były ich intencje i jakie są ich długofalowe plany, nie jest powszechna. Tymczasem uważam, że bez niej nie można w pełni wykorzystać potencjału zawartego w tym języku.

Silne przenikanie paradygmatu funkcyjnego do obiektowego, w pierwotnych założeniach języka, nie będzie zaskoczeniem, gdy uświadomimy sobie, że ci sami autorzy stworzyli również język F#. Ten młodszy i biedniejszy kuzyn poczyna sobie całkiem nieźle i stał się główną inspiracją dla najnowszego wcielenia swojego starszego krewnego. Niedawne otwarcie przez Microsoft platformy .NET i upublicznienie zapisów spotkań komitetu projektowego, daje nam niemożliwy wcześniej wgląd w proces powstawania przyszłych wersji tego języka. Jedno wiemy już na pewno: funkcyjnych zabawek będzie jeszcze więcej!

---

## O mnie

- Tata^2, mąż humanistki, mól książkowy, uparciuch, programista, konferencjoholik.  Don Kichot walczący z entropią. Kocha sprzeczności i humor. Wierzy w przypadek. Piwny filozof. W nielicznych wolnych chwilach harata w gałę (na bramce).

- Basic, Turbo Pascal/C, Assembler, Clipper, MS Access, Visual Basic, Java-XML :), C++, C#, JavaScript, F#...  i ze wszystkiego miałem frajdę, ale nie za wszystkim tęsknię.

- Absolwent informatyki i matematyki na UW. Tech lead w firmie Piątka.

***

## Spis rzeczy

Spojrzenie...

1. ...do cudzego ogródka (Java)
2. ...za siebie (C# 1-5)
3. ...przed siebie (C# 6)
4. ...przez ramię (C# 7+)
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

- mniej stanu, mniej drapania się po głowie
- o działaniu programu można wnioskować z samych deklaracji typów danych i funkcji
- krócej/czytelniej: LINQ, generics, lambdy, var...

Wady:

- więcej parametrów funkcji (długie deklaracje typów)
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

---

<!-- .slide: data-background="./images/features4.png" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->
## C# 5.0 &amp; .NET 4.5 (2012)

- async / await
- ``IReadOnlyList<>``, ``IReadOnlyDictionary<>``...
- Microsoft.Bcl.Immutable

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

***

## Unde malum?

![https://twitter.com/dsyme/status/409476721780334592](./images/donsyme.png)

---

> Don Syme is the designer and architect of the F# programming language [...] Earlier, created generics in the .NET Common Language Runtime, including the initial design of generics for the C# programming language [...]

http://en.wikipedia.org/wiki/Don_Syme


***

<!-- .slide: data-background="./images/fp-way-bg.jpg" -->

# C# 6

# Functional way is the right way

---

### Primary constructors / Readonly auto properties

F# dziś:
```fsharp
type Point(x, y) =
    member this.X = x
    member this.Y = y
```

C# 6 Preview:
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

Note: konstruktory wyleciały prawd. z powodu planowanych rekordów

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

C# 6 Preview:
```csharp
public static class Math
{
    public static int Add(int x, int y) { return x + y; }
}

using Math;

Add(2, 2);
```

Note: czyli używajmy funkcji jak ludzie

---

###  Declaration expressions

F# dziś:
```fsharp
let success, x = Int32.TryParse("123")
// lub
match TryParse("123") with true, x -> ... | _ -> ...
```

C# 6 Preview:
```csharp
if (int.TryParse("123", out int x)) ... else ...
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

C# 6 Preview:
```csharp
try
{
    throw new ArgsException(ErrorCode.UnexpectedArgument);
}
catch (ArgsException e)
    when (e.ErrorCode == ErrorCode.UnexpectedArgument) {...}
```

---

### Monadic null checking aka null propagator

F# dziś:
```fsharp
let (>>=) x y = Option.bind y x // generalnie mało przydatne
```

C# 6 Preview:
```csharp
var bestValue = points?.FirstOrDefault()?.X ?? -1;
```

---

### Method &amp; property expressions (lambdas as definitions)

F# dziś: ha, ha - wolne żarty

C# 6 Preview:
```csharp
public Point Move(int dx, int dy) => new Point(X + dx, Y + dy);
public double Distance => Math.Sqrt((X * X) + (Y * Y));
```

---

### Constructor type parameter inference

F# dziś:
```fsharp
let tuple = (5, "y")
```

C# 6 Preview:
```csharp
// zamiast new Tuple<int, string>(5, "y") / Tuple.Create(5, "y")
var tuple = new Tuple(5, "y");
// zamiast new KeyValuePair<string, Tuple<int, string>>(...)
var pair = new KeyValuePair("x", tuple);
```

***

<!-- .slide: data-background="./images/dexter.jpg" style="padding: 20px; display: block; background: rgba(0, 0, 0, 0.4);" -->

## Tymczasem w laboratorium

C# 7 Design Meeting Notes:

> Let’s continue being inspired by functional languages, and in particular other languages – F#, Scala, Swift – that aim to mix functional and object-oriented concepts as smoothly as possible

https://github.com/dotnet/roslyn/issues/98

---

### Pattern matching

C# dziś:
```csharp
var e = s as ExpressionStatement;
if (e != null) {
    var a = e.Expr as AssignmentExpressionSyntax;
    if (a != null) {
        var l = a.Left as IdentifierName;
        var r = a.RIght as IdentifierName;
        if (l != null && r != null & l.Name.name == r.Name.name) ...
```

C# 7:
```csharp
if (s is ExpressionStatement(
        AssignmentExpressionSyntax(IdentifierName l, IdentifierName r)) 
    && l.name = r.name) ...
// lub
switch (s) {
case ExpressionStatement(
        AssignmentExpressionSyntax(IdentifierName l, IdentifierName r)
        where (l.name == r.name): ...
}
```

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

C# dziś:
```csharp
public void Tally(IEnumerable<int> values, out int sum, out int count) {...}
public Tuple<int, int> Tally(IEnumerable<int> values) {...}
```

F# dziś:
```fsharp
let tally = List.fold (fun (sum, count) v -> (sum + v, count + 1)) (0, 0)
```
C# 7:
```csharp
public (int sum, int count) Tally(IEnumerable<int> values) {
    var sum = 0; var count = 0;
    foreach (var v in values) { sum += v; count++; }
    return (sum, count);
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
- [Why Functional Programming Matters](http://www.cse.chalmers.se/~rjmh/Papers/whyfp.html)
- [John Carmack - In-depth: Functional programming in C++](http://gamasutra.com/view/news/169296/Indepth_Functional_programming_in_C.php)

Materiały:

- Slajdy: http://4Dev2015.orientman.com/
- Źródłowce: https://github.com/orient-man/CleanArgs

***

# Aaa... pytania?

Ankieta: https://www.surveymonkey.com/s/SKPS35K Pls!

![Ankieta QR Code](./images/ankieta-qrcode.png)

