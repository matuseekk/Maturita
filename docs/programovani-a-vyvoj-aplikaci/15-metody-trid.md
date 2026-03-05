# 15. Metody trid (navratovy typ, parametry, modifikatory pristupu) – prehled

## Cile (co musis umet rict)
- Co je metoda v kontextu tridy a proc se pouziva (chovani objektu)
- Jak vypada hlavicka metody:
  - modifikator pristupu
  - (pripadne dalsi modifikatory)
  - navratovy typ
  - nazev
  - parametry
- Rozdil mezi:
  - procedurou (`void`)
  - funkci (vraci hodnotu)
- Parametry:
  - hodnotove
  - referencni (`ref`, `out`)
  - volitelne
  - `params`
- Pretezovani metod (overloading) + priklady
- Zaklady:
  - `static` vs instancni metoda
  - scope (`this`)
  - kdy metodu volam na objektu/tride
- Ukazky, na kterych se da mluvit 10–15 minut (vysvetleni + mini demo)

---

## Co je metoda tridy
- Metoda = cast tridy s vykonatelnym kodem (logikou)
- Popisuje, co objekt umi delat (chovani)
- Rozdeleni v OOP:
  - atributy/pole/vlastnosti = co objekt ma (data)
  - metody = co objekt dela (chovani)
- Metody casto:
  - pracuji s vlastnostmi objektu
  - meni stav objektu
  - nebo pocitaji vysledek a vraci ho

---

## Hlavicka metody (z ceho se sklada)
- Modifikator pristupu: `public`, `private`, `protected`, `internal`
- Dalsi modifikatory (volitelne): `static`, `virtual`, `override`, `abstract`, `async`…
- Navratovy typ
- Nazev metody
- Parametry v kulatych zavorkach `(...)`

Priklad:
- `public int Mocnina(int x)`

---

## Modifikatory pristupu (access modifiers)
- `public` – pristupna odkudkoliv
- `private` – pristupna jen uvnitr tridy (casto pomocne metody)
- `protected` – pristupna v tride a u potomku (pri dedeni)
- `internal` – pristupna jen v ramci projektu/assembly
- `protected internal` / `private protected` – kombinace (spis doplnkove)

---

## Navratovy typ: procedura vs funkce
### Procedura (`void`)
- nema navratovou hodnotu
- ucel: „neco udelat“ (zobrazit, ulozit, zmenit stav objektu)

### Funkce (vraci hodnotu)
- neco vypocita a vrati hodnotu pomoci `return`
- vysledek typicky:
  - priradim do promenne  
    - `int vysledek = Mocnina(4);`
  - nebo pouziju jako parametr / ve vyrazu  
    - `Console.WriteLine(Mocnina(4));`
- funkce muze vracet libovolny typ (int/string/bool/objekt/list…)

---

## Parametry metody (prehled + mini priklady)
### 1) Hodnotove parametry (default)
- bezny zpusob predani hodnoty do metody
- priklad:
  - `int Pricist(int a, int b)`

### 2) `out` (vraceni vice hodnot / vysledku)
- kdyz chces z metody dostat vice informaci
- priklad:
  - `bool ZkusParsovatInt(string text, out int cislo)`
- volani:
  - `if (ZkusParsovatInt("123", out int x)) { ... }`

### 3) `ref` (upravovani existujici promenne)
- metoda muze zmenit hodnotu promenne predane odkazem
- priklad:
  - `void Zvys(ref int x)`

### 4) Volitelne parametry (default hodnota)
- parametr ma vychozi hodnotu, nemusis ho pri volani vyplnit
- priklad:
  - `void Pozdrav2(string jmeno = "kamarade")`

### 5) `params` (promenny pocet argumentu)
- muzes poslat libovolny pocet hodnot
- priklad:
  - `int Soucet(params int[] cisla)`
- volani:
  - `Soucet(1, 2, 3, 4);`

---

## Static vs instancni metody
### Instancni metody
- volas na objektu
- muzou pracovat se stavem objektu (`this`)
- priklad:
  - `ucet.Deposit(100);`

### Static metody
- patri tride, ne konkretni instanci
- volas pres nazev tridy
- casto „utility“ funkce
- priklad:
  - `Math.Sin(x);`

---

## Priklad: metody meni stav objektu (BankAccount)
- `Deposit` / `Withdraw`:
  - procedury (`void`)
  - meni stav (`Balance`)
  - validuji vstup + mohou vyhodit vyjimku
- `CanWithdraw`:
  - funkce (vraci `bool`)
  - nic nemeni, jen informuje
- zapouzdreni:
  - `Balance` ma `private set` (zvenku nejde libovolne menit)

---

## Pretezovani metod (overloading)
- stejne jmeno, jina signatura (pocet/typ parametru)
- priklad:
  - `Soucet(int a, int b)`
  - `Soucet(int a, int b, int c)`
- kompilator vybere spravnou variantu podle argumentu pri volani

---

## Navaznost na WinForms: obsluzna metoda udalosti
- Ve WinForms jsou metody casto „event handlers“ (obsluzne metody)
- typicky priklad:
  - `private void button1_Click(object sender, EventArgs e)`
- co rict:
  - je to procedura (`void`) – reaguje na udalost (klik)
  - `sender` = kdo udalost vyvolal (napr. Button)
  - `e` = data o udalosti (EventArgs nebo potomci)
  - Visual Studio umi metodu vytvorit a napojit na `Click` (designer)

---

## Doporucena osnova na 15 minut mluveni
- Co je metoda, proc existuje (2 min)
- Hlavicka metody + modifikatory pristupu (2–3 min)
- Procedura vs funkce + prirazeni / parametr (3 min)
- Parametry (`out/ref`, volitelne, `params`) (4–5 min)
- `static` vs instancni + pretezovani (2–3 min)
- BankAccount (OOP, zapouzdreni, validace) (3–5 min)
- WinForms event handler (1–2 min)

---

## Mini-tahak (30–60 s)
- Metoda = kod v tride (chovani). Hlavicka: pristup + navratovy typ + nazev + parametry.
- `void` = procedura (neco udela). Funkce vraci hodnotu -> priradim nebo pouziju jako parametr.
- Parametry: normalni, `out/ref`, volitelne, `params`.
- Metody: instancni nebo `static`, mohou byt pretezene.
- WinForms: metody casto obsluhuji udalosti (napr. `button_Click`).
