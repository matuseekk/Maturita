# 12. Principy OOP – trida, objekt, skladani, dediceni, zapouzdreni, delegovani a polymorfizmus

## Rozdělení

## Třídy
- je kod v jazyce c#, který odráží realitu světa(můžeme tedy vytvořit třídu pro jakékoliv podst. Jméno jak konkrétní tak abstraktní)
- Třídu tvoří atributy(základní charakteristiky objektu) 

- Z třídy může vzniknout libovolný počet objektů 

- Objekty vznikají pomocí konstruktoru, který inicializuje třídu(to znamená že jeho úkolem je přiřadit objektům hodnoty) 

- Konstruktory parametrické, který má určité parametry nebo bezparametrické 

- Konstruktorů mohu mít v podstatě tolik kolik má atributů + 1 

- Objekty vznikají užitím logického operátoru new (neznamená nový), jenž zavolá konstruktor třídy který vytvoří objekt
  
### Co je to skládání
- kdybych chtěl třeba vytvořit úsečku tak je tvořena 2 body a každý bod je vytvořen třídou, která má 2 atributy(X,Y) a pak si definuju třídu úsečka a ta bude mít bod A a B

### Dědění 
- věc která je běžná, celý vývoj živočichů, rostlin i hub je zapříčeněn děděním. Umožnuje tvorbu nových tříd na základě již existujících tříd jako houba houbě , musíme přijmou Darwinovu teorii, jinak za to může bůh(v takovém případě je to poměrně jednoduché), kde byla nízká tráva, tak tam žili želvy s krátkými krky, naopak tam kde nebyla tráva vůbec žily želvy s dlouhým krkem a zaobleným krunýřem a takhle je to se vším. Dneska se ta genetika zkoumá na vinných muškách(pořád nás otravují drosophili, které se rychle množí prakticky během několika dní vzniká nová generace, která bud umí nebo neumí lítat) během několika dní se bud naučí nebo odnaučí lítat. V dnešní genetice by jsme nejspíše dokázali fotosyntetizovat, což bychom neměli, ale někdo  to stejně určitě dělá 

- Všimněte si, že principy fungují v reálném životě 

- Dědění provádíme tak, že za název napíšeme dvojtečku a za ní název třídy od které dědí (např. Form1:Form) v tomto případě je Form rodič  

- Třída může dědit pouze od jednoho předka(jako homo sapiens asi ?)

### Zapouzdření
- je provedeno tím, že třída obsahuje metody a ty mohou být privátní(z venku neviditelné) a já mohu zavolat veřejně viditelnou metodu a ta zavolá neviditelnou metodu. Uživatel zapouzdřenou(skrytou) metodu nevidí a tedy neví jak se k ní dostal 

 

### Delegování 
- třída může delegovat některé činnosti. To znamená že funkci nebo činnost předá jinému objektu.  Místo vlastní implementace využívá jinou třídu 

#### Pozor!! Delegování není totéž co delegát, delegát se používá pro události !! 

 

### Polymorfizmus
- když ve třídě vytvořím metodu Počítej, třeba s jedním nebo 2 parametry at to dává smysl a pak tu samou s 3 parametry a pak tu samou se 4 parametry, Tak vlastně vytvářím metody.
- Má to stejný název, ale vždycky to dělá něco jiného 
- Příklad - Slepice dělá Kokoko a pes dělá Haf 

 
### Implementace
- by v této otázce asi měla být taky, i když tu není 

- je samotné napsání konkrétního kódu, který realizuje (uskutečňuje) návrh nebo definici – například metody, třídy nebo rozhraní. 

- Nejčastěji se tím myslí vytvoření konkrétní třídy, která implementuje rozhraní pomocí klíčového slova :, např. když třída přebírá a definuje metody z interface. 

- Implementace tedy znamená převod návrhu (např. UML nebo zadání) do funkčního programu v jazyce C#. 


## Principy OOP 
### Příklad třídy
- Bankovní učet, kde atributy jsou jméno a příjmení majitele číslo účtu 
### Atributy
- základní vlastnosti budoucího objektu, globální proměnné(můžeme použít ve všech metodách třídy) 
### Modifikátory přístupu
- stačí když budeme vědět public a private, pomocí modifikátorů určujeme zda je ten atribut z vnějšku viditelný nebo je viditelný pouze ve třidě 
- Pak můžeme definovat jestli v potomkovy je viditelný 
- Slušelo by říct, že ty atributy až na výjimky implementujeme jako privátní, aby je z venku nemohl nikdo vidět. Výjimkou je návrhový vzor Přepravka 
- Na začátku jsou ty atributy samozřejmě pouze deklarovány a naplní je až konstruktor a jelikož jsou privátní tak bychom se k nim z venku nedostali. Proto konstruujeme gettery a settery, get. Získávají hodnoty a set. Nastavují  

### C# má tzv. Vlastnosti
- které mají jak getter, tak setter (nepovinně). Public color Barva{get;set;} 
- Takhle zkráceně deklaruji v případě že nechci žádnou logiku, pokud logiku chci musím vlastnost vytvořit jako metodu(respektive funkci) Public color Barva a pak tam je část get a část set
- V části set například  dovolím měnit barvu jen v případě že je původní barva bílá (jakoby podmínka), asi je jasný o čem mluvím ne ? 
- Ta vlastnost pak funguje tak že: var barva = Auto.barva (můžu získat tu vlastnost) 

## Zdroje
- Tonda
