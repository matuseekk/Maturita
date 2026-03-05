# 11. Jazyk C# – základní struktury a principy, datové typy a proměnné

## Cíle (co musíš umět říct)
- Co je C# a k čemu se používá (typické aplikace).
- Základní vlastnosti jazyka (OOP, case‑sensitive, bez globálních proměnných/metod).
- Co je CTS (Common Type System) a že všechny typy dědí ze `System.Object`.
- Rozdíl mezi hodnotovými a referenčními typy.
- Co je proměnná, konstanta, identifikátor a jak je deklarovat.
- Přehled základních datových typů + praktické ukázky.

---

## Základy C#
- C# (C Sharp) je objektově orientovaný jazyk od Microsoftu, běžící na platformě .NET (CLR).
- Použití: desktop (WinForms/WPF), web (ASP.NET), služby, mobil (.NET MAUI), hry (Unity) atd.
- V praxi se kompiluje do mezikódu (IL) a spouští se pod CLR (JIT).
- Důležité: C# je case‑sensitive (rozlišuje velká/malá písmena).

---

## Vlastnosti jazyka (maturitní body)
- Není vícenásobná dědičnost tříd (trida dědí jen z jedné třídy).
- Žádné globální proměnné/metody — vše v rámci tříd/struktur.
- Pořadí deklarací metod není důležité (není potřeba dopředná deklarace).
- Podpora OOP: třídy, objekty, dědičnost, zapouzdření, rozhraní.

---

## CTS – Common Type System
- CTS sjednocuje typový systém v .NET — všechny jazyky sdílejí typy.
- Všechny typy jsou potomky `System.Object`.
- Typy jsou buď:
  - hodnotové (value types), nebo
  - referenční (reference types).

---

## Hodnotové vs referenční typy
- Hodnotové typy:
  - Proměnná obsahuje přímo hodnotu.
  - Při přiřazení se kopíruje hodnota.
  - Příklady: `int`, `double`, `bool`, `char`, `decimal`, `struct`, `enum`.
- Referenční typy:
  - Proměnná obsahuje referenci (ukazatel) na objekt v paměti (heap).
  - Při přiřazení se kopíruje reference — více proměnných může odkazovat na tentýž objekt.
  - Příklady: `string`, `class`, pole (`int[]`), `List<T>`.

> Pozn.: `string` je referenční, ale immutable (neměnný).

---

## Proměnné (variables)
- Proměnná má identifikátor (jméno) a datový typ.
- Může mít modifikátor přístupu (`public`, `private`, `protected`).
- Deklarace a inicializace:
```csharp
int vek = 18;
string jmeno = "Karel";
bool dospely = true;
```

---

## Konstanty (neměnné proměnné)
- Označí se pomocí `const` a musí být inicializovány při deklaraci.
```csharp
const double PI = 3.1415926535;
```
- Konstantu nelze později změnit.

---

## Gettery a settery (zapouzdření)
- Privátní pole se často zpřístupňují přes vlastnosti (properties):
```csharp
private int vek;

public int Vek
{
    get { return vek; }
    set { vek = value; }
}
```
- Zkrácený zápis / auto‑property:
```csharp
public int Vek { get; private set; }
```

---

## Datové typy – přehled a ukázky

### 1) Jednoduché (primitivní) typy
- Ordinální (mají předchůdce/následníka):  
  - `bool` (true / false)  
  - Celá čísla: `byte`, `short`, `int` (32 bit), `long` (64 bit)  
  - `char` – znak (Unicode)
```csharp
int a = 5;
int b = 5;
int c = a + b;
```
- Neordinální (reálná čísla): `float`, `double`, `decimal`
```csharp
double teplota = 36.6;
decimal cena = 199.90m;
```
- Prázdný typ: `void` (pouze jako návratový typ metod).

---

### 2) Výčtové typy (enum)
- Množina předdefinovaných hodnot.
```csharp
public enum Barva { Piky, Srdce, Kary, Krize }

Barva b = Barva.Srdce;
```

---

### 3) Struktury (struct)
- Uživatelsky definované hodnotové typy.
- Nemohou dědit od jiných struktur (kromě `object`), mohou implementovat rozhraní.
```csharp
public struct Bod
{
    public int X;
    public int Y;
}
```

---

### 4) Složené datové typy
- Pole (array): indexované od 0
```csharp
int[] cisla = { 1, 2, 3 };
int prvni = cisla[0];

int[,] matice = new int[2,3]; // vícerozměrné pole
```
- String: textový řetězec (referenční, neměnný)
```csharp
string veta = "Ahoj svete";
```
- List (List<T>): dynamická kolekce, indexovatelná
```csharp
var seznam = new List<string>();
seznam.Add("Ahoj");
seznam.Add("Čau");
string prvni = seznam[0];
```

> Oprava: `List<T>` lze indexovat (`seznam[0]`) — je to výhoda nad některými jinými strukturami.

---

### 5) Zvláštní typy
- Pointer (ukazatel) — pouze v `unsafe` kódu (běžně se nepoužívá).
- Práce se soubory přes třídy (`File`, `FileStream`).
- Komplexní čísla: `System.Numerics.Complex` (knihovna).

---

## Krátké příklady (rychle k vložení do kódu)

- Konstanty
```csharp
const double PI = 3.1415926535;
```

- Gettery / settery (auto‑property)
```csharp
private int vek;
public int Vek { get { return vek; } set { vek = value; } }

// nebo zkráceně
public int Vek { get; private set; }
```

- Enum
```csharp
public enum Barva { Piky, Srdce, Kary, Krize }
Barva b = Barva.Srdce;
```

- Struct
```csharp
public struct Bod { public int X; public int Y; }
var p = new Bod { X = 1, Y = 2 };
```

- Pole a List
```csharp
int[] cisla = { 1, 2, 3 };
var seznam = new List<string> { "Ahoj", "Čau" };
```

---

## Mini‑tahák (30–60 s)
- C# = OOP jazyk pro .NET (Microsoft). Použití: desktop, web, služby, mobil, hry.
- Case‑sensitive, bez globálních funkcí/proměnných, nepotřebuje dopřednou deklaraci.
- CTS: všechny typy dědí ze `System.Object`.
- Typy: hodnotové (int, bool, struct, enum) vs referenční (string, class, array, List).
- Proměnná = typ + identifikátor + hodnota; konstanta = `const`.
- Zapouzdření: privátní pole + vlastnosti (get/set).

