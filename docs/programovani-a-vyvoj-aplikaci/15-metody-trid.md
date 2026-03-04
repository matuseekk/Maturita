# 15. Metody trid (navratovy typ, parametry, modifikatory pristupu)

## Cile (co musis umet rict)
- Co je metoda v kontextu tridy a proc se pouziva (chovani objektu).
- Jak vypada **hlavicka metody**: modifikator pristupu, (prip. dalsi modifikatory), navratovy typ, nazev, parametry.
- Rozdil mezi **procedurou** (`void`) a **funkci** (vraci hodnotu).
- Parametry: hodnotove vs referencni (`ref`, `out`), volitelne, `params`.
- Pretezovani metod (overloading) + priklady.
- Zaklady: `static` vs instancni metoda, scope (`this`), kdy metodu volam na objektu/tride.
- Ukazky, na kterych se da mluvit 10–15 minut (vysvetleni + mini demo).

---

## Co je metoda tridy
**Metoda** je cast tridy, ktera obsahuje vykonatelny kod (logiku). Popisuje, **co objekt umi delat**.

- Atributy/pole/vlastnosti = *co objekt ma (data)*
- Metody = *co objekt dela (chovani)*

V OOP je bezne, ze metoda pracuje s daty objektu (vlastnostmi) a meni je nebo z nich pocita vysledky.

---

## Hlavicka metody (podle ucitele „zacina hlavickou“)
Typicky ma metoda tvar:

- **modifikator pristupu** (`public`, `private`, `protected`, `internal`)
- pripadne dalsi modifikatory (`static`, `virtual`, `override`, `abstract`, `async`…)
- **navratovy typ**
- **nazev metody**
- **parametry** v kulatych zavorkach `(...)`

Priklad hlavicky:
- `public int Mocnina(int x)`

---

## Modifikatory pristupu (access modifiers)
- **public** – pristupna odkudkoliv
- **private** – pristupna jen uvnitr tridy (nejcastejsi pro pomocne metody)
- **protected** – pristupna v tride a u potomku (pri dedeni)
- **internal** – pristupna jen v ramci projektu/assembly
- **protected internal / private protected** – kombinace (spis navic)

U maturity casto staci rozumet hlavne `public` vs `private`.

---

## Navratovy typ: procedura vs funkce
Tvoje myslenka je spravna: podle navratoveho typu rozlisujeme:

### Procedura (void)
- nema navratovou hodnotu
- jeji ukol je „neco udelat“ (zobrazit, ulozit, zmenit stav objektu…)

V C# je to metoda s navratovym typem `void`.

### Funkce (vraci hodnotu)
- neco vypocita a **vrati**
- vysledek typicky:
  1) **priradim do promenne**, nebo
  2) pouziju jako soucast vyrazu / parametr jine metody

Napriklad:
- `int vysledek = Mocnina(4);`
- `Console.WriteLine(Mocnina(4));`  *(funkce je parametr jine metody)*

> Dulezite: Funkce nemusí „vracet jen int“. Muze vracet libovolny typ (string, bool, objekt, list…).

---

## Parametry metody
Parametry urcuji, co metoda potrebuje na vstupu.

### Hodnotove parametry (default)
Vetsina parametru se predava hodnotou (u hodnotovych typu kopie, u referencnich typu kopie reference).

```csharp name=examples/Methods.cs
public int Pricist(int a, int b)
{
    return a + b;
}
