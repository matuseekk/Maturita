# 03. Dynamické webové stránky

## Cíle (co musíš umět říct)
- Vysvětlit, co je dynamická webová stránka a jak se liší od statické.
- Popsat princip fungování – role serveru, požadavek → server → HTML odpověď.
- Charakterizovat PHP (syntaxe, použití, výhody).
- Popsat ASP.NET MVC – co je návrhový vzor MVC a co dělají jednotlivé komponenty (Model, View, Kontroler).
- Vysvětlit rozdíl hybridní vs. nativní program.

---

## Osnova
1. Co je dynamická webová stránka (vs. statická)
2. Princip fungování – statická vs. dynamická (role serveru)
3. Technologie: PHP vs. ASP.NET
4. PHP – základní charakteristika a syntaxe
5. ASP.NET MVC – návrhový vzor, komponenty
6. IIS (Internet Information Services) – jak spustit ASP server
7. Hybridní vs. nativní program
8. Bezpečnostní doporučení / typické chyby
9. Mini-tahák

---

## Pojmy (rychlé definice)
- **Dynamická webová stránka:** stránka, jejíž obsah je generován na serveru na míru pro každého uživatele / každé zobrazení.
- **Statická webová stránka:** soubor (HTML + CSS + JS), který prohlížeč přímo otevře; obsah je pro všechny stejný.
- **Server-side skript:** kód spuštěný na serveru (PHP, Python, Ruby, C#...) – výsledkem je HTML stránka odeslaná prohlížeči.
- **PHP:** skriptovací jazyk pro tvorbu dynamických webů; běží na serveru; nejrozšířenější (cca 77 % webů).
- **ASP.NET MVC:** webový framework od Microsoftu využívající návrhový vzor MVC (Model–View–Controller).
- **MVC (Model–View–Controller):** návrhový vzor rozdělující aplikaci na 3 nezávislé části pro lepší přehlednost a údržbu.
- **Model:** část MVC zpracovávající data a logiku aplikace; komunikuje s databází.
- **View (Pohled):** část MVC zobrazující data uživateli; šablona, do které se vloží data.
- **Kontroler (Controller):** prostředník mezi Modelem a View; reaguje na požadavky uživatele.
- **IIS (Internet Information Services):** webový server od Microsoftu integrovaný ve Windows; umožňuje spustit ASP.NET aplikace.
- **Hybridní program:** webová aplikace přístupná přes prohlížeč na jakémkoli OS; není třeba ji přepisovat pro každý systém.
- **Nativní program:** aplikace určená pouze pro jedno prostředí/OS; na jiných systémech vyžaduje emulátor.
- **SQL Injection:** útok vložením škodlivého SQL kódu do formuláře za účelem přístupu k databázi.

---

## Co je dynamická webová stránka

Za **dynamickou webovou stránku** je označována taková stránka, jejíž obsah byl **vygenerován na míru pro každé zobrazení**.

- Přizpůsobuje se konkrétnímu uživateli – každý ji vidí jinak.
- Obsah se přizpůsobuje na základě: data a času, cookies, zařízení uživatele, přihlášení, databázových dat...
- Jsou výrazně **flexibilnější a interaktivnější** než statické stránky (personalizace, fóra, e-shopy, přihlášení...).
- Vhodné pro **větší projekty**.
- Jsou **složitější a dražší** na vývoj, mají vyšší nároky na zabezpečení.
- Obsahují **databázi** (SQLite, MySQL, PostgreSQL...).
- Obvykle používají **server-side skripty** (PHP, Python, Ruby, C#/ASP.NET...).

---

## Princip fungování — statická vs. dynamická stránka

### Statická stránka
- Prohlížeč si **přímo otevře soubor** (HTML + CSS + JS).
- Obsah je pro všechny stejný.
- JS může přidávat interaktivitu (animace, DOM manipulace), ale **bez serveru a bez přihlášení**.
- Vhodné pro jednoduché prezentační weby.

### Dynamická stránka
1. Uživatel zadá požadavek (URL) do prohlížeče.
2. Požadavek **jde na server**.
3. Na serveru se spustí aplikace (PHP, ASP.NET...), která zpracuje požadavek, dotáže se databáze a **vygeneruje HTML**.
4. Server **vrátí hotové HTML** prohlížeči.
5. Prohlížeč zobrazí výsledek – uživatel nevidí kód, jen výstup.

```
Uživatel → [Požadavek] → Server → [Aplikace + Databáze] → HTML → Prohlížeč
```

> Klíčový rozdíl: u statické stránky prohlížeč otevírá soubor přímo; u dynamické je navíc **server**, který stránku sestaví.

---

## PHP

**PHP** (Hypertext Preprocessor) je skriptovací programovací jazyk určený zejména pro programování webových stránek.

### Základní charakteristika
- Syntaxe inspirována jazyky **C a Java**.
- Je **case sensitive** (rozlišuje velká a malá písmena).
- Podporuje přístup k většině databázových systémů (MySQL, SQLite, PostgreSQL...).
- Nejrozšířenější skriptovací jazyk pro web – podíl cca **77 % webů**.
- Používán i pro velké projekty: **Wikipedie, Facebook** (původně).
- Podporuje webové formuláře (nutné zabezpečit proti útokům – SQL injection, XSS...).

### Syntaxe
Do HTML se vkládá pomocí tagu `<?php ... ?>`:

```php
<html>
  <body>
    <?php
      echo "Miluju spošku";
    ?>
  </body>
</html>
```

- Na konci výrazů se píše **`;`** (středník).
- Výstup (obdoba `WriteLine`) se provádí příkazem **`echo`**:
  ```php
  echo "Hello, World!";
  ```
- **Implicitní deklarace proměnné** – proměnné se rovnou přiřadí hodnota, netřeba je deklarovat zvlášť:
  ```php
  $jmeno = "Jan";
  $vek = 20;
  ```
- Proměnné začínají znakem **`$`**.

---

## ASP.NET MVC

**ASP.NET MVC** je webový framework od Microsoftu využívající návrhový vzor **MVC (Model–View–Controller)**.

- Rozděluje aplikaci do **tří nezávislých komponent**.
- Odděluje logiku od výstupu → přehlednější kód, snazší údržba a testování.
- Dnes je z velké části nahrazován **ASP.NET Core** (multiplatformní – funguje i mimo Windows).

### Komponenty MVC

#### Model
- Zpracovává **data aplikace**.
- Odpovídá na dotazy zbývajících komponent.
- **Komunikuje s databází** (čtení, zápis, aktualizace).
- Obsahuje **logiku aplikace** (validace, výpočty, pravidla).

#### View (Pohled)
- **Zobrazuje data** uživateli.
- Předává uživatelské vstupy kontroleru.
- Je to **šablona**, do které se vloží data z modelu.
- Neobsahuje logiku – jen prezentační vrstvu.

#### Kontroler (Controller)
- **Reaguje na události** a požadavky uživatele.
- Zajišťuje změny v modelu a pohledu.
- Funguje jako **prostředník mezi View a Modelem**.

### Příklad – URL routing v ASP.NET MVC

```
http://IP/denik            → zavolá Controller "DenikC" → ten zavolá akci Index
http://IP/denik/DenikC     → explicitní volání controlleru
http://IP/denik/edit/4     → akce Edit s parametrem id=4
```

- Stačí zadat `IP/denik` → automaticky se zavolá výchozí controller a jeho akce `Index`.
- Lze volat i konkrétní akce s parametry: `IP/denik/edit/4` (4 = parametr).

---

## IIS — Internet Information Services

- Webový server **integrovaný ve Windows** (ve výchozím stavu není zapnutý).
- Po zapnutí IIS se z PC stane webový server.
- IIS vytvoří strukturu:
  ```
  C:\inetpub\
  └── wwwroot\        ← veřejný kořen webu
      └── denik\      ← složka projektu (přístupná jako IP/denik)
  ```
- Přístup přes prohlížeč: `http://IP/denik` → spustí webové stránky ze složky `denik`.
- Pro ASP.NET aplikace **vyžaduje IIS** (nebo IIS Express pro lokální vývoj).

---

## Hybridní vs. nativní program

| Typ | Popis | Výhody | Nevýhody |
|-----|-------|--------|---------|
| **Hybridní (webová aplikace)** | Otevírá se v prohlížeči na jakémkoli OS; používá HTML, CSS, JS | Levnější vývoj, funguje všude, nepotřeba přepisovat pro jiné systémy | Omezené možnosti přístupu k hardware |
| **Nativní program** | Určen pouze pro jedno prostředí/OS | Plný přístup k hardware a OS funkcím | Na jiných systémech jen s emulátorem; dražší vývoj |

> Hybridní app: uživatel ani nepozná, že pracuje s webovkou – vypadá jako plnohodnotná aplikace.

---

## Bezpečnostní doporučení / typické chyby

- **SQL Injection** – vždy sanitizovat vstupy z formulářů; používat parametrizované dotazy nebo ORM.
- **XSS (Cross-Site Scripting)** – escapovat výstupy do HTML (nevkládat neošetřené uživatelské vstupy).
- **CSRF** – používat CSRF tokeny ve formulářích.
- **Hesla** – nikdy neukládat v plaintextu; používat bcrypt nebo Argon2.
- **HTTPS** – dynamické weby musí běžet přes HTTPS (citlivá data, přihlášení).
- **Aktualizace** – pravidelně aktualizovat PHP, ASP.NET framework a závislosti.
- **Nejmenší privilegia** – databázový uživatel aplikace by měl mít jen nezbytná práva.

---

## Mini-tahák (30–60 s)

- **Dynamická stránka** = generuje se na serveru pro každého uživatele jinak (přihlášení, databáze).
- **Statická** = soubor otevřený prohlížečem; JS může přidat interaktivitu, ale bez serveru/přihlášení.
- Princip: Požadavek → Server (PHP/ASP) → Databáze → HTML → Prohlížeč.
- Technologie: **PHP** (77 % webu, `<?php echo ... ?>`) nebo **ASP.NET MVC**.
- **MVC** = Model (data + logika) + View (zobrazení) + Kontroler (prostředník).
- ASP.NET vyžaduje **IIS** (Windows); Core je multiplatformní.
- URL routing: `IP/složka/kontroler/akce/parametr`.
- Hybridní = webová app (všechny OS, levnější); Nativní = jen jeden OS (výkonnější).
- Hlavní hrozby: **SQL Injection, XSS, CSRF** – vždy sanitizovat vstupy!

---

## Zdroje
- [PHP.net – Oficiální dokumentace](https://www.php.net/docs.php)
- [Microsoft Docs – ASP.NET MVC](https://learn.microsoft.com/cs-cz/aspnet/mvc/overview/getting-started/introduction/getting-started)
- [Microsoft Docs – ASP.NET Core](https://learn.microsoft.com/cs-cz/aspnet/core/)
- [IIS – Internet Information Services](https://learn.microsoft.com/cs-cz/iis/get-started/introduction-to-iis/iis-web-server-overview)