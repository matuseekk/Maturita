# 14. Konstruktor třídy, přetížené konstruktory, konstruktor s parametrem a bezparametrický

## Cíle (co musíš umět říct)
- Vysvětlit, co je konstruktor, kdy se volá a proč nemá návratový typ.
- Popsat rozdíl mezi bezparametrickým a parametrickým konstruktorem.
- Uvést příklady přetížených konstruktorů a řetězení pomocí `: this(...)`.

---

## Osnova
1. Definice konstruktoru (co to je, kdy se volá, žádný návratový typ)
2. Inicializace objektu – co nastavuje
3. Bezparametrický vs. parametrický konstruktor + ukázky
4. `this` a přiřazení parametru do atributu
5. Přetížené konstruktory + proč se používají
6. Řetězení `: this(...)` a výhoda oproti opakování kódu
7. Validace v konstruktoru + příklad
8. Mini-tahák

---

## Pojmy (rychlé definice)
- **Konstruktor:** speciální metoda třídy, která se volá při vytvoření objektu (`new`); inicializuje atributy.
- **Bezparametrický konstruktor:** konstruktor bez parametrů – nastaví výchozí hodnoty.
- **Parametrický konstruktor:** konstruktor s parametry – hodnoty předáš při vytváření objektu.
- **Přetížení (overloading):** více konstruktorů ve stejné třídě s různými parametry.
- **`this`:** odkaz na aktuální instanci objektu; v konstruktoru rozlišuje atribut (`this.barva`) od parametru (`barva`).
- **Řetězení konstruktorů:** volání jiného konstruktoru stejné třídy pomocí `: this(...)`.
- **Validace:** kontrola vstupních hodnot přímo v konstruktoru; při neplatném vstupu se vyhodí výjimka.

---

## Definice konstruktoru

Konstruktor je speciální metoda, která se **automaticky volá při vytvoření objektu** (`new`).

- Má **stejný název jako třída**.
- **Nemá návratový typ** (ani `void`).
- Jeho úkolem je **inicializovat objekt** – nastavit atributy/vlastnosti na výchozí nebo zadané hodnoty.

---

## 1) Bezparametrický konstruktor

Konstruktor bez parametrů – nastaví výchozí hodnoty automaticky.

```csharp
public class Auto
{
    public string Značka { get; }
    public int RokVýroby { get; }
    public string Barva { get; }

    // bezparametrický konstruktor
    public Auto()
    {
        Značka = "Neznámá";
        RokVýroby = 2000;
        Barva = "šedá";
    }
}
```

**Použití:**
```csharp
var a = new Auto();
```

**Co říct u maturity:**
- Vytvoří se objekt a automaticky se nastaví výchozí hodnoty.
- Je to pohodlné, když chceš „rychle" objekt a hodnoty doplníš později.

---

## 2) Parametrický konstruktor (konstruktor s parametry)

Předáš hodnoty při vytvoření objektu – konstruktor je uloží do vlastností/atributů.

```csharp
public class Auto
{
    public string Značka { get; }
    public int RokVýroby { get; }
    public string Barva { get; }

    // parametrický konstruktor
    public Auto(string značka, int rokVýroby, string barva)
    {
        Značka = značka;
        RokVýroby = rokVýroby;
        Barva = barva;
    }
}
```

**Použití:**
```csharp
var auto = new Auto("Ford", 2008, "bílá");
```

---

## `this` v konstruktoru (a proč se používá)

Když se parametry jmenují stejně jako vlastnosti/atributy, používá se `this`, aby bylo jasné, co je co:

```csharp
public class Auto
{
    private string barva;

    public Auto(string barva)
    {
        this.barva = barva; // this.barva = atribut, barva = parametr
    }
}
```

**Vysvětlení:**
- `this.barva` = atribut/vlastnost objektu
- `barva` = parametr konstruktoru

Přesně odpovídá zápisu: „`this.barva = barva` – atributu je přiřazen parametr".

---

## Přetížené konstruktory (overloading)

Přetížené konstruktory = v jedné třídě máš více konstruktorů s různými parametry.

**Důležité:**
- Nelze mít 2 konstruktory se stejnou signaturou (stejné parametry).
- „Kolik jich můžeme mít": teoreticky hodně, ale má to dávat smysl (aby to bylo přehledné).

**Příklad:**
```csharp
public class Auto
{
    public string Značka { get; }
    public int RokVýroby { get; }
    public string Barva { get; }

    // 1) bezparametrický
    public Auto()
    {
        Značka = "Neznámá";
        RokVýroby = 2000;
        Barva = "šedá";
    }

    // 2) jen se značkou
    public Auto(string značka)
    {
        Značka = značka;
        RokVýroby = 2000;
        Barva = "šedá";
    }

    // 3) kompletní
    public Auto(string značka, int rokVýroby, string barva)
    {
        Značka = značka;
        RokVýroby = rokVýroby;
        Barva = barva;
    }
}
```

**Použití:**
```csharp
var a1 = new Auto();
var a2 = new Auto("Ford");
var a3 = new Auto("Ford", 2008, "bílá");
```

**Co říct:**
- Přetěžování zvyšuje pohodlí (různý „způsob vytvoření" objektu).
- Ale nemá se to přehánět, aby se v tom dalo vyznat.

---

## Řetězení konstruktorů (doporučená praxe)

Aby se neopakoval kód, konstruktory se často řetězí:

```csharp
public class Auto
{
    public string Značka { get; }
    public int RokVýroby { get; }
    public string Barva { get; }

    public Auto() : this("Neznámá", 2000, "šedá")
    {
    }

    public Auto(string značka) : this(značka, 2000, "šedá")
    {
    }

    public Auto(string značka, int rokVýroby, string barva)
    {
        Značka = značka;
        RokVýroby = rokVýroby;
        Barva = barva;
    }
}
```

**Co říct:**
- `: this(...)` zavolá jiný konstruktor ve stejné třídě.
- Výhoda: jedna centrální inicializace, méně chyb.

---

## Validace v konstruktoru (aby objekt nevznikl špatně)

Konstruktor může zkontrolovat, jestli jsou parametry v pořádku:

```csharp
public class Auto
{
    public string Značka { get; }
    public int RokVýroby { get; }

    public Auto(string značka, int rokVýroby)
    {
        if (string.IsNullOrWhiteSpace(značka))
            throw new ArgumentException("Značka nesmí být prázdná.", nameof(značka));

        if (rokVýroby < 1886) // první auta zhruba kolem konce 19. století
            throw new ArgumentOutOfRangeException(nameof(rokVýroby), "Rok výroby je příliš malý.");

        Značka = značka;
        RokVýroby = rokVýroby;
    }
}
```

**Co říct:**
- Validace brání tomu, aby vznikaly neplatné objekty.
- Když se vstupy nelíbí, konstruktor může vyhodit výjimku.

---

## Příklady ze života (jak to říct u maturity)

Konstruktor = „když něco vytvářím, musím tomu dát základní parametry":

- **Auto:** značka, rok výroby, barva, výkon
  - bezparametrický = „auto s defaultním nastavením"
  - parametrický = „konfigurace na zakázku"
- **Účet (bankovní/uživatelský):** owner, počáteční zůstatek, měna
  - konstruktor hlídá, aby zůstatek nebyl záporný
- **Student:** jméno, příjmení, třída
  - bezparametrický: „neznámý student"
  - parametrický: vyplním hned vše

---

## Doporučená osnova na 15 minut mluvení

1. Definice konstruktoru, kdy se volá, že nemá návratový typ (2 min)
2. Inicializace objektu – co všechno nastavuje (2–3 min)
3. Bezparametrický vs. parametrický konstruktor + ukázky (4–5 min)
4. `this` a přiřazení parametru do atributu (2 min)
5. Přetížené konstruktory + proč se používají (2–3 min)
6. Řetězení `: this(...)` a výhoda oproti opakování kódu (2–3 min)
7. Validace v konstruktoru + příklad (1–2 min)

---

## Mini-tahák (30–60 s)

- Konstruktor se volá při `new`, inicializuje objekt.
- Stejný název jako třída, nemá návratový typ.
- Druhy: bezparametrický, parametrický, přetížené.
- `this` rozlišuje atribut vs. parametr a umožňuje řetězení `: this(...)`.
- Konstruktor může dělat validaci, aby nevznikl „špatný" objekt.

---

## Zdroje
- [Microsoft Docs – Constructors (C#)](https://learn.microsoft.com/cs-cz/dotnet/csharp/programming-guide/classes-and-structs/constructors)