# 16. WinForms – standardni ovladaci prvky

## Cile (co musis umet rict)
- Co je WinForms a proc je Windows „udalostni“ (event-driven) prostredi.
- Co je **formular (Form)** a jak vznika (dedenim tridy `Form`).
- Co se deje, kdyz na formular pretahnu ovladaci prvek z Toolboxu.
- Vyjmenovat typicke ovladaci prvky (Button, CheckBox, RadioButton, ListBox, ComboBox, TextBox, Label, Panel, ScrollBar…) a rict jejich zakladni vlastnosti + udalosti.
- Ukazat, kde se to projevi v kodu (**Form.Designer.cs**, `InitializeComponent()`).

---

## Zaklad: projekt WinForms a formular
K teto otazce je idealni sednout si k PC a otevrit nejaky **WinForms** projekt.

Zakladni „vykreslovaci prvek“ je **formular (Form)**:
- Formular je okno aplikace a typicky se vytvari jako trida (napr. `Form1`), ktera **dedi** z tridy `System.Windows.Forms.Form`.
- To znamena: *formular vznika dedenim*.

### Jak se formular spousti (Application.Run)
Ve WinForms aplikaci obvykle existuje vstupni bod (`Program.cs`), kde se vola neco jako:

- vytvori se instance formulare (napr. `new Form1()`),
- a ta se preda do `Application.Run(...)`.

`Application.Run(new Form1())` spusti tzv. **message loop** (smycku zprav) – Windows je **udalostni system**, tzn. aplikace reaguje na udalosti (kliknuti, stisk klavesy, zmena hodnoty, posun…).

> Dulezite: Formular (a dalsi prvky) jsou graficke komponenty – ve WinForms se „vykresluji“ za pomoci frameworku a OS. V konzolove aplikaci bys mohl taky otevrit okno, ale musel bys si na to napojit GUI knihovnu a message loop; WinForms tohle dela standardne za tebe.

---

## Co se stane, kdyz pretahnu prvek z Toolboxu na formular
Kdyz z panelu nastroju (Toolbox) pretahnes ovladaci prvek (napr. Button) na formular, tak se typicky stane:

1. Vygeneruje se **deklarace pole** (private field) ovladaciho prvku v designeru, napr.:
   - `private System.Windows.Forms.Button button1;`

2. V metode `InitializeComponent()` se provede:
   - **vytvoreni instance** (napr. `this.button1 = new Button();`)
   - nastaveni vlastnosti (pozice, velikost, text, jmeno…)
   - pridani prvku do kolekce ovladacich prvku formulare (zjednodusene „prida se na formular“)

3. Kdyz pak pridas obsluhu udalosti (napr. DoubleClick na `Click`), designer doplni i napojeni udalosti na metodu (event handler), napr.:
   - `this.button1.Click += new System.EventHandler(this.button1_Click);`

Tohle vsechno najdes v souboru **`Form1.Designer.cs`**.

---

## Vlastnosti (Properties) a udalosti (Events)
Ve Visual Studiu mas typicky:
- okno **Properties** – vlastnosti vybraneho prvku
- karta/ikonka „**blesk**“ – seznam **udalosti** prvku

Poznamka z praxe:
- Kdyz mas vybrany konkretni prvek (napr. `Button`), vidis jeho vlastnosti.
- Kdyz kliknes na prazdne misto formulare (vyberes `Form`), uvidis vlastnosti formulare.

---

## Standardni ovladaci prvky (prehled)

### Form (formular)
- Zakladni okno aplikace.
- Dulezite vlastnosti: `Text` (titulek), `Size`, `StartPosition`, `BackColor`, `FormBorderStyle`.
- Udalosti: `Load`, `Shown`, `FormClosing`, `Resize`.

### Button
- Tlacitko pro spousteni akce.
- Vlastnosti: `Text`, `Enabled`, `Visible`.
- Udalosti: hlavne `Click`.

### Label
- Popisek (text na obrazovce).
- Vlastnosti: `Text`, `AutoSize`.

### TextBox
- Vstup textu.
- Vlastnosti: `Text`, `Multiline`, `PasswordChar`.
- Udalosti: `TextChanged`, `KeyPress`.

### CheckBox
- Zaskrtavaci volba (ano/ne).
- Nejdulezitejsi vlastnost: `Checked` (zda je zaskrtnuty).
- Nejdulezitejsi udalost: `CheckedChanged`.

### RadioButton
- Volba z vice moznosti (typicky ve skupine).
- Vlastnost: `Checked`.
- Udalost: `CheckedChanged`.
- Poznamka: aby fungovala spravna „skupina“, davaji se do stejneho kontejneru (napr. `GroupBox` nebo `Panel`).

### ListBox
- Seznam polozek k vyberu.
- Dulezite vlastnosti:
  - `Items` (kolekce polozek – muzes pridavat/odebirat)
  - `SelectedIndex`, `SelectedItem`
- Udalosti:
  - casto `SelectedIndexChanged` (zmena vyberu)

### ComboBox
- Rozbalovaci seznam.
- Podobne jako ListBox: `Items`, `SelectedIndex`, `SelectedItem`.
- Udalosti: `SelectedIndexChanged`, pripadne `TextChanged` (podle stylu).

### Panel / GroupBox
- Kontejnery pro seskupeni prvku.
- Uzitecne pro rozlozeni UI a skupinovani RadioButtonu.

### ScrollBar (HScrollBar / VScrollBar)
- Posuvnik (horizontalni/vertikalni).
- Dulezite vlastnosti:
  - `Value` (aktualni hodnota)
  - `Minimum`, `Maximum` (rozsah)
  - `SmallChange`, `LargeChange` (kroky posunu)
- Udalosti: napr. `Scroll`, `ValueChanged`.

---

## Co je dulezite u maturity (jak to rict)
U maturity je dobre postupovat takhle:

1. **Spustim WinForms projekt** a ukazu formular.
2. Vysvetlim, ze `Form1` je trida a **dedi z `Form`**.
3. Ukazu `Program.cs` a `Application.Run(new Form1())`:
   - Windows je **udalostni system** → aplikace bezi v message loop a reaguje na udalosti.
4. Pretahnu prvek z Toolboxu (napr. Button) a ukazu:
   - vlastnosti v Properties
   - udalosti pres „blesk“
   - a v `Form1.Designer.cs`, ze:
     - se vytvorilo pole `button1`
     - instance `new Button()`
     - nastaveni vlastnosti
     - pripadne napojeni udalosti na obsluznou metodu

---

## Mini-tahak (na 30–60 s)
- WinForms je GUI framework pro Windows, funguje udalostne (event-driven).
- Formular je trida dedi z `System.Windows.Forms.Form`.
- `Application.Run(new Form1())` spusti message loop.
- Pretazeni prvku z Toolboxu vygeneruje kod v `Form1.Designer.cs` (deklarace, `new`, nastaveni, pridani na form).
- Nejdulezitejsi prvky: Button (Click), CheckBox (Checked + CheckedChanged), ListBox (Items + SelectedIndexChanged), ScrollBar (Value/Minimum/Maximum + Scroll).
