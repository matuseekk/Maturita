# 14. Konstruktory tříd (bezparametrický, s parametrem, přetížené)

## Cíle (co musíš umět říct)
- Co je konstruktor a kdy se volá.
- K čemu slouží inicializace objektu (nastavení výchozích hodnot, kontrola vstupu).
- Druhy konstruktorů:
  - bezparametrický
  - parametrický
  - přetížené konstruktory
- Jak funguje `this` v konstruktoru.
- Co je řetězení konstruktorů (`: this(...)`) a proč se používá.
- Praktické příklady z C# i ze života (aby bylo na ~15 minut povídání).
- Rozdíl konstruktor vs. metoda, zmínka o destruktoru / finalizeru a o `IDisposable`.

---

## Osnova
1. Úvod — proč konstruktor
2. Základní vlastnosti konstruktoru
3. Inicializace objektu — co to znamená
4. Bezparametrický konstruktor + ukázka
5. Parametrický konstruktor + ukázka
6. `this` v konstruktoru
7. Přetížené konstruktory (overloading)
8. Řetězení konstruktorů (`: this(...)`)
9. Validace v konstruktoru
10. Konstruktor vs. metoda
11. Destruktor / Finalizer a `IDisposable`
12. Příklady ze života
13. Doporučená osnova na 15 minut
14. Mini-tahák

---

## Pojmy (rychlé definice)
- **Konstruktor:** speciální metoda třídy, která se volá při vytvoření objektu (`new`); inicializuje atributy.
- **Bezparametrický konstruktor:** konstruktor bez parametrů – nastaví výchozí hodnoty.
- **Parametrický konstruktor:** konstruktor s parametry – hodnoty předáš při vytváření objektu.
- **Přetížení (overloading):** více konstruktorů ve stejné třídě s různými parametry.
- **`this`:** odkaz na aktuální instanci objektu; v konstruktoru rozlišuje atribut (`this.barva`) od parametru (`barva`).
- **Řetězení konstruktorů:** volání jiného konstruktoru stejné třídy pomocí `: this(...)`.
- **Validace:** kontrola vstupních hodnot přímo v konstruktoru; při neplatném vstupu se vyhodí výjimka.
- **Destruktor / Finalizer:** metoda volaná při uvolnění objektu z paměti (garbage collector); v C# zapsaná jako `~NazevTridy()`.
- **`IDisposable`:** rozhraní pro deterministické uvolnění zdrojů (soubory, spojení); voláme `Dispose()` nebo blok `using`.

---

## Úvod — proč konstruktor

Konstruktor je základní mechanismus tříd v objektově orientovaném programování pro vytvoření nových instancí v konzistentním stavu. Bez konstruktoru by vytváření objektu často znamenalo „vytvořím prázdný objekt" a pak krok po kroku nastavím vlastnosti. Konstruktor umožňuje:

- zajistit, že objekt bude mít všechny povinné hodnoty hned po vytvoření,
- provádět základní validaci vstupů,
- nastavit výchozí hodnoty,
- případně alokovat zdroje (např. otevřít spojení nebo soubor).

**Přirovnání ze života:** když si kupuješ auto, nedostaneš prázdné šasi — dostaneš auto s motorem, koly a základním vybavením. Konstruktor „sestaví" objekt správně.

---

## Základní vlastnosti konstruktoru

- Název konstruktoru je **stejný jako název třídy**.
- **Nemá návratový typ** (ani `void`).
- Volá se automaticky při použití `new`.
- Může být přetížen (více konstruktorů s různými parametry).
- Může obsahovat logiku (přiřazení, kontrolu, volání dalších metod, logování...).

---

## Inicializace objektu — co to znamená

Inicializace = přiřazení hodnot do atributů/vlastností tak, aby objekt dával smysl a byl v použitelném stavu.

Co se obvykle dělá v konstruktoru:
- přiřazování vlastností z argumentů,
- nastavení výchozích hodnot (pokud argumenty chybějí),
- validace (kontrola rozsahů, null-check),
- zajištění invariantu třídy (stavy, které musí platit po celou dobu života objektu),
- volání pomocných metod pro složitější inicializaci.

---

## 1) Bezparametrický konstruktor

Konstruktor bez parametrů – nastaví výchozí hodnoty automaticky.

```csharp
public class Auto
{
    public string Značka { get; set; }
    public int RokVýroby { get; set; }
    public string Barva { get; set; }

    // bezparametrický konstruktor
    public Auto()
    {
        Značka = "Neznámá";
        RokVýroby = 2000;
        Barva = "bílá";
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

## Přetížené konstruktor

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

## Řetězení konstrukt

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

## Konstruktor vs. metoda

| Vlastnost | Konstruktor | Metoda |
|-----------|------------|--------|
| Název | Stejný jako třída | Libovolný |
| Návratový typ | Žádný (ani `void`) | Má návratový typ (nebo `void`) |
| Kdy se volá | Automaticky při `new` | Explicitně voláme na objektu |
| Počet | Může být přetížen | Může být přetížena |
| Účel | Inicializace objektu | Operace nad objektem |

**Důležité:** konstruktor **není** metoda — nemůžeš ho zavolat ručně jako `auto.Auto()`.

---

## Destruktor / Finalizer a `IDisposable`

### Destruktor (Finalizer)

- Destruktor se volá, když **garbage collector** uvolňuje objekt z paměti.
- V C# se zapisuje jako `~NazevTridy()`.
- **Nevíme přesně kdy** se zavolá — záleží na GC.
- Použití: uvolnění nespravovaných zdrojů (COM objekty, nativní handles).

```csharp
public class Auto
{
    ~Auto()
    {
        // úklid při zničení objektu (GC)
    }
}
```

### `IDisposable` — deterministické uvolnění zdrojů

Pokud objekt drží zdroje (soubor, databázové spojení, síťový socket), implementujeme `IDisposable`:

```csharp
public class Soubor : IDisposable
{
    private FileStream _stream;

    public Soubor(string cesta)
    {
        _stream = File.OpenRead(cesta);
    }

    public void Dispose()
    {
        _stream?.Dispose();
    }
}
```

**Použití s `using` (doporučeno):**
```csharp
using (var soubor = new Soubor("data.txt"))
{
    // práce se souborem
} // Dispose() se zavolá automaticky na konci bloku
```

**Co říct:**
- `IDisposable` + `using` = deterministické uvolnění zdrojů (víme přesně kdy).
- Destruktor = nedeterministické (GC rozhodne sám).

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
8. (Bonus) Konstruktor vs. metoda, destruktor, `IDisposable` (1–2 min)

---

## Mini-tahák (30–60 s)

- Konstruktor se volá při `new`, inicializuje objekt.
- Stejný název jako třída, nemá návratový typ.
- Druhy: bezparametrický, parametrický, přetížené.
- `this` rozlišuje atribut vs. parametr a umožňuje řetězení `: this(...)`.
- Konstruktor může dělat validaci, aby nevznikl „špatný" objekt.
- Destruktor (`~Trida()`) = GC ho volá sám; `IDisposable` + `using` = voláme sami.

---

## Zdroje
- [Microsoft Docs – Constructors (C#)](https://learn.microsoft.com/cs-cz/dotnet/csharp/programming-guide/classes-and-structs/constructors)
- [Microsoft Docs – Destructors (C#)](https://learn.microsoft.com/cs-cz/dotnet/csharp/programming-guide/classes-and-structs/destructors)
- [Microsoft Docs – IDisposable](https://learn.microsoft.com/cs-cz/dotnet/api/system.idisposable)