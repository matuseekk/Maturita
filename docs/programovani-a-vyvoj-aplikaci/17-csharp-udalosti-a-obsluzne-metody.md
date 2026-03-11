# 17. C# – události tříd, přidání reference na obslužnou metodu, tvorba obslužných metod

## Cíle (co musíš umět říct)
- Vysvětlit, co je událost a proč ji používáme (reakce na změnu stavu objektu).
- Popsat, co je delegát, jak funguje a proč je základem událostí.
- Ukázat, jak se událost deklaruje a jak se na ni přihlásí obslužná metoda (`+=` / `-=`).
- Popsat obslužnou metodu – signaturu, parametr `sender` a `EventArgs e`.
- Vysvětlit rozdíl mezi přihlášením události ve WinForms (automaticky) a v konzoli (ručně).
- Uvést praktické příklady z WinForms i z vlastních tříd.

---

## Osnova
1. Co je událost a proč ji používáme
2. Delegát – základ událostí
3. Deklarace události ve třídě
4. Přihlášení a odhlášení obslužné metody (`+=` / `-=`)
5. Obslužná metoda – struktura, `sender`, `EventArgs`
6. Vlastní EventArgs
7. WinForms – automatické přihlášení, Designer.cs
8. Konzole – ruční přihlášení
9. Multicast delegát (více obslužných metod na jednu událost)
10. Lambda výrazy jako obslužné metody
11. Typické chyby
12. Příklady ze života
13. Mini-tahák

---

## Pojmy (rychlé definice)
- **Událost (event):** speciální člen třídy, který umožňuje objektu oznámit ostatním, že nastala určitá akce.
- **Delegát (delegate):** typově bezpečný ukazatel na metodu; definuje signaturu, kterou musí obslužná metoda splňovat.
- **Obslužná metoda (event handler):** metoda, která se zavolá při události; musí odpovídat signatuře delegátu.
- **`+=`:** přihlášení obslužné metody k události.
- **`-=`:** odhlášení obslužné metody od události.
- **`sender`:** objekt, který událost vyvolal.
- **`EventArgs`:** parametr nesoucí detaily události (souřadnice kliknutí, stisknutá klávesa...).
- **`EventHandler`:** předdefinovaný delegát v .NET: `void(object sender, EventArgs e)`.
- **Multicast delegát:** delegát odkazující na více metod najednou.
- **Designer.cs:** automaticky generovaný soubor WinForms s vizuálním nastavením a přihlášením událostí.

---

## Co je událost a proč ji používáme

**Události upozorňují, že se stalo něco zajímavého**, na co by třída (nebo jiný objekt) měla nějak reagovat.

- Pomocí události třída reaguje na **změnu stavu** nebo na **akci uživatele**.
- Ke změně stavu nemusí nutně dojít – může se jednat pouze o **pokus o změnu** (lze ho zrušit / vetovat).
- Příklad: změna barvy auta ve třídě `Auto` → ostatní části programu mohou být upozorněny a reagovat.

### Proč nepoužít obyčejné metody?
- Metodu voláme vždy explicitně – musíme vědět, kdy a koho zavolat.
- Událost umožňuje **volné propojení** (loose coupling) – třída, která vyvolává událost, **nemusí vědět**, kdo ji poslouchá.
- Přihlášených obslužných metod může být **libovolný počet** (multicast).

---

## Delegát — základ událostí

**Delegát** je datový typ, který definuje **signaturu metody** (návratový typ + parametry).

- Je to **typově bezpečný ukazatel na metodu** – kompilátor zkontroluje, zda metoda odpovídá signatuře.
- Události jsou interně implementovány přes delegáty.

### Deklarace vlastního delegátu

```csharp
public delegate void ZmenaBarvy(object sender, EventArgs e);
```

### Předdefinovaný delegát `EventHandler`

```csharp
// Generická verze pro vlastní EventArgs:
public event EventHandler<BarvaEventArgs> BarvaZmenena;
```

---

## Deklarace události ve třídě

```csharp
public class Auto
{
    private string barva;

    // Deklarace události
    public event EventHandler BarvaZmenena;

    public string Barva
    {
        get => barva;
        set
        {
            if (barva != value)
            {
                barva = value;
                // Bezpečné vyvolání události
                BarvaZmenena?.Invoke(this, EventArgs.Empty);
            }
        }
    }
}
```

**Klíčové body:**
- `event` = klíčové slovo označující událost.
- `?.Invoke(...)` = bezpečné volání – pokud není přihlášen žádný handler, neuletí `NullReferenceException`.
- `this` jako sender = říkáme „já, tento objekt, jsem vyvolal událost".

---

## Přihlášení a odhlášení obslužné metody

```csharp
Auto auto = new Auto();

// Přihlášení
auto.BarvaZmenena += Auto_BarvaZmenena;

// Odhlášení
auto.BarvaZmenena -= Auto_BarvaZmenena;
```

**Důležité:**
- `+=` přidá referenci – metoda se bude volat při každém vyvolání události.
- `-=` referenci odebere – metoda se přestane volat.
- Stejnou metodu lze přihlásit vícekrát → zavolá se vícekrát (pozor na chybu!).
- Pokud zapomeneme odhlásit, může dojít k **memory leaku**.

---

## Obslužná metoda — struktura

```csharp
private void Auto_BarvaZmenena(object sender, EventArgs e)
{
    Auto auto = (Auto)sender; // přetypování na konkrétní typ
    Console.WriteLine("Barva auta byla změněna!");
}
```

### Parametry
- **`object sender`** – objekt, který událost vyvolal (přetypovat na konkrétní typ).
- **`EventArgs e`** – detaily události; pro standardní události `EventArgs.Empty`, jinak vlastní data.

---

## Vlastní EventArgs

Pokud chceme předat vlastní data, vytvoříme třídu děděnou z `EventArgs`:

```csharp
public class BarvaEventArgs : EventArgs
{
    public string StaraBarva { get; }
    public string NovaBarva { get; }

    public BarvaEventArgs(string staraBarva, string novaBarva)
    {
        StaraBarva = staraBarva;
        NovaBarva = novaBarva;
    }
}
```

Použití ve třídě `Auto`:

```csharp
public event EventHandler<BarvaEventArgs> BarvaZmenena;

// Ve setteru:
BarvaZmenena?.Invoke(this, new BarvaEventArgs(stara, value));
```

V obslužné metodě:

```csharp
private void Auto_BarvaZmenena(object sender, BarvaEventArgs e)
{
    Console.WriteLine($"Barva změněna z '{e.StaraBarva}' na '{e.NovaBarva}'.");
}
```

---

## WinForms — automatické přihlášení, Designer.cs

Ve **WinForms** se obslužné metody vytváří a přihlašují **automaticky**:

1. Otevřeš form v návrháři.
2. Vybereš ovládací prvek (tlačítko, textové pole...).
3. V panelu **Vlastnosti** přepneš na záložku **Události** (ikona blesku ⚡).
4. Dvakrát klikneš na událost (např. `Click`) → Visual Studio automaticky:
   - Vytvoří obslužnou metodu v `Form1.cs`.
   - Přidá `+=` přihlášení do `Form1.Designer.cs`.

### Designer.cs
- Automaticky generovaný soubor – **neupravujeme ručně**.
- Obsahuje polohu ovládacích prvků, barvy, velikosti a přihlášení událostí.

```csharp
// Automaticky vygenerovaný kód v Designer.cs:
this.button1.Click += new System.EventHandler(this.button1_Click);
```

---

## Konzole — ruční přihlášení

```csharp
static void Main(string[] args)
{
    Auto auto = new Auto();

    // Ruční přihlášení
    auto.BarvaZmenena += Auto_BarvaZmenena;

    auto.Barva = "červená"; // událost se zavolá
    auto.Barva = "modrá";   // událost se zavolá

    // Odhlášení
    auto.BarvaZmenena -= Auto_BarvaZmenena;
    auto.Barva = "zelená";  // událost se už nezavolá
}

private static void Auto_BarvaZmenena(object sender, EventArgs e)
{
    Console.WriteLine("Barva auta se změnila!");
}
```

---

## Multicast delegát

Na jednu událost lze přihlásit více obslužných metod – všechny se zavolají:

```csharp
auto.BarvaZmenena += Metoda1;
auto.BarvaZmenena += Metoda2;
auto.BarvaZmenena += Metoda3;
// Při vyvolání se zavolají všechny tři v pořadí přihlášení.
```

---

## Lambda výrazy jako obslužné metody

```csharp
auto.BarvaZmenena += (sender, e) =>
{
    Console.WriteLine("Lambda handler: barva se změnila.");
};
```

**Pozor:** lambda výraz **nelze odhlásit** pomocí `-=` – vhodná jen pro jednorázové použití.

---

## Bezpečnostní doporučení / typické chyby

- **NullReferenceException** – vždy používat `?.Invoke(...)`, nikdy holé `Událost(...)`.
- **Memory leak** – nezapomenout odhlásit handlery (`-=`) při uvolňování objektu.
- **Vícenásobné přihlášení** – stejná metoda přihlášena vícekrát → zavolá se vícekrát; hlídej to zejm. v cyklech nebo při reinicializaci formu.
- **Přetypování sender** – používej `as` pro bezpečné přetypování: `Auto auto = sender as Auto;`
- **Lambda a odhlášení** – anonymní lambda nelze odhlásit; pokud potřebuješ `-=`, použij pojmenovanou metodu.

---

## Příklady ze života

| Situace | Událost | Obslužná metoda |
|---------|---------|-----------------|
| Kliknutí na tlačítko (WinForms) | `button1.Click` | Otevře nové okno |
| Změna textu v textovém poli | `textBox1.TextChanged` | Aktualizuje náhled |
| Pohyb myši | `MouseMove` | Zobrazí souřadnice |
| Stisk klávesy | `KeyDown` | Reaguje na Enter/Escape |
| Vlastní třída Auto | `BarvaZmenena` | Loguje změnu barvy |
| Časovač (Timer) | `Tick` | Aktualizuje GUI každou sekundu |

---

## Doporučená osnova na 15 minut mluvení

1. Co je událost a proč ji používáme – přirovnání ze života (2 min)
2. Delegát – ukazatel na metodu, typová bezpečnost (2 min)
3. Deklarace události ve třídě + `?.Invoke(...)` (2 min)
4. Přihlášení `+=` a odhlášení `-=` + příklad (2 min)
5. Obslužná metoda – signatura, `sender`, `EventArgs` (2 min)
6. Vlastní EventArgs – jak předat vlastní data (1–2 min)
7. WinForms vs. konzole – automatické vs. ruční přihlášení (2 min)
8. Multicast + lambda + typické chyby (1 min)

---

## Mini-tahák (30–60 s)

- **Událost** = oznámení, že nastala akce; třída ji vyvolá, jiné objekty poslouchají.
- **Delegát** = typový ukazatel na metodu; definuje signaturu obslužné metody.
- Deklarace: `public event EventHandler NazevUdalosti;`
- Vyvolání: `NazevUdalosti?.Invoke(this, EventArgs.Empty);`
- Přihlášení: `objekt.NazevUdalosti += ObsluznaMetoda;`
- Odhlášení: `objekt.NazevUdalosti -= ObsluznaMetoda;`
- Obslužná metoda: `void Metoda(object sender, EventArgs e)`
- WinForms = automaticky přes Designer; konzole = ručně.
- Multicast = více handlerů na jednu událost.
- Nezapomenout odhlásit (`-=`) → jinak memory leak!

---

## Zdroje
- [Microsoft Docs – Events (C#)](https://learn.microsoft.com/cs-cz/dotnet/csharp/programming-guide/events/)
- [Microsoft Docs – Delegates (C#)](https://learn.microsoft.com/cs-cz/dotnet/csharp/programming-guide/delegates/)
- [Microsoft Docs – EventHandler](https://learn.microsoft.com/cs-cz/dotnet/api/system.eventhandler)
- [Microsoft Docs – WinForms Events](https://learn.microsoft.com/cs-cz/dotnet/desktop/winforms/events-overview-windows-forms)
