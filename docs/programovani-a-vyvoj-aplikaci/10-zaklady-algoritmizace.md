# 10. Zaklady algoritmizace

## Cile (co musis umet rict)
- Rict, co je algoritmus a uvest priklad z bezneho zivota (napr. kucharka).
- Vyjmenovat vlastnosti algoritmu (konecnost, urcitost, proveditelnost, obecnost…).
- Popsat zakladni ridici struktury: sekvence, vetveni, cykly.
- Vysvetlit rozdil mezi cyklem s podminkou na zacatku a na konci + k cemu je `for` a `foreach`.
- Vyjmenovat zpusoby zapisu algoritmu (slovne, vyvojovy diagram, program).

---

## Algoritmus – definice
**Algoritmus** je **presny navod / postup**, jak vyresit urcity typ problemu.

- Je to „predpis“, ktery vede od **vstupu** k **vystupu**.
- Priklad z bezneho zivota: **kucharsky recept** (kucharka).
  - Kdyz chci uvarit svickovou, recept me ma dovest k vysledku.

---

## Vlastnosti algoritmu (co by mel splnovat)
Algoritmus by mel byt:

- **Konecny (rezultativni)**  
  Musi skoncit v konecnem poctu kroku. (Kroku muze byt hodne, ale nesmi byt nekonecne.)
- **Jednoznacny (urcity, determinovany krok po kroku)**  
  Kazdy krok musi byt presne definovany – musi byt jasne, co se ma udelat.
- **Proveditelny**  
  Kroky musi jit realne vykonat (clovekem nebo pocitacem).
- **Obecny**  
  Ma fungovat pro vice moznych vstupu (resi ulohy daneho typu, ne jen jeden konkretni priklad).
- **Korektni**  
  Pro spravne vstupy da spravny vysledek a skonci.
- **Ma vstup a vystup**  
  Minimalne jeden vystup (odpoved / vysledek), ktery souvisi se zadanim.

Poznamka k „jednoduchosti“: casto se pozaduje, aby byl algoritmus co nejjednodussi (elementarni kroky, dobra citelnost).

---

## Ridici struktury (zaklad logiky programu)

### 1) Sekvence
Kroky jdou **jednoznacne za sebou** v poradi, v jakem jsou napsane (radek po radku).

Priklad (sekvence vypoctu):
- mame `a = 5`, `b = 5`
- vypocitam `c = a + b`
- vypisu `c`

### 2) Vetveni (rozhodovani)
Algoritmus se muze **rozvetvit** podle podminky (napr. `if`, `if/else`).

Priklad:
- kdyz je `vek < 18` → „nezletily“
- jinak → „dospely“

### 3) Cykly (opakovani)
Cykly opakuji urcitou cast algoritmu.

#### Cyklus `for` (pocitany cyklus)
Typicky ma 3 casti:

1. **inicializace ridici promenne**  
   napr. `int i = 0`
2. **podminka pokracovani**  
   napr. `i < 10` (dokud plati, cyklus bezi)
3. **zmena ridici promenne**  
   napr. `i++`

Z parametru casto dokazes odhadnout, **kolikrat cyklus probehne**.

> Pozn.: V C# jsou casti `for` oddelene stredniky `;`.

#### Cyklus s podminkou na zacatku (while)
- nejdriv se zkontroluje podminka,
- kdyz neplati, telo cyklu se muze **preskocit uplne**.

Priklad myslenky:
- „dokud `h > 5`, provadej prikazy…“
- kdyz `h > 5` neplati uz na zacatku, cyklus se neprovede ani jednou.

#### Cyklus s podminkou na konci (do-while)
- nejdriv se vykona telo cyklu,
- az potom se kontroluje podminka.

Dulezite: cyklus se provede **vzdy alespon jednou**.

#### `foreach` (pruchod kolekci)
Pouziva se pro „projeti“ prvku v kolekci (seznam, pole, vysledek dotazu z databaze…).
- je prehledny
- typicky nepotrebujes rucne ridici promennou `i`

---

## Zapis algoritmu
Algoritmus lze zapsat:

1. **Slovne** (jako recept v kucharce)
2. **Diagramem** (vyvojovy diagram / flowchart)
   - obdelnik = akce (prikaz)
   - kosodelnik = vstup/vystup
   - kosoctverec = podminka (vetveni)
   - sipky = tok rizeni
3. **Programovacim jazykem**  
   Zapis algoritmu, ktery muze vykonat pocitac = **program**.

---

## Metody navrhu algoritmu
- **Shora dolu (top-down)**: problem rozdelim na mensi kroky/podproblemy.
- **Zdola nahoru (bottom-up)**: z jednoduchsich funkci/bloku skladam slozitejsi reseni.
- Casto se pouziva kombinace (top-down + knihovny hotovych funkci).

---

## Deleni algoritmu (prehled)
- **Iterativni** vs **rekurzivni**
  - iterativni: opakovani bloku (cyklus)
  - rekurzivni: volani sebe sama (casto citelne, ale narocnejsi na prostredky)
- **Deterministicky** vs **nedeterministicky**
  - deterministicky: v kazdem kroku je jasne dana jedna cesta
- **Seriovy** vs **paralelni** vs **distribuovany**
  - seriovy: kroky po sobe
  - paralelni: vice kroku najednou (vlákna)
  - distribuovany: na vice strojich

---

## Asymptoticka slozitost (jen zakladni myslenka)
Popisuje, jak roste pocet operaci algoritmu s velikosti vstupu (napr. O(n), O(n^2)…).
U maturity obvykle staci vysvetlit, ze:
- cim efektivnejsi algoritmus, tim lepe skaluje na velka data.

---

## Mini-tahak (na 30–60 s)
- Algoritmus = presny postup reseni problemu (napr. recept).
- Musi byt konecny, jednoznacny, proveditelny, obecny a korektni.
- Struktury: sekvence, vetveni (if/else), cykly (for/while/do-while/foreach).
- while: podminka na zacatku (muze byt 0×), do-while: podminka na konci (min. 1×).
- Zapis: slovne, vyvojovy diagram, program.
