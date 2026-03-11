# 03. Kybernetické hrozby a ochrana proti nim

## Cíle (co musíš umět říct)
- Vysvětlit pojmy: kybernetická událost, kybernetická hrozba, riziko.
- Rozdělit hrozby na úmyslné a neúmyslné, vnitřní a vnější.
- Popsat základní typy malwaru (virus, trojský kůň, ransomware) a útoků (DDoS, phishing, social engineering).
- Vysvětlit ochranu – legislativa, firemní politika, technická opatření.
- Popsat rozdělení internetu (surface, deep, dark web).

---

## Osnova
1. Základní pojmy (hrozba, riziko, kybernetická událost)
2. Dělení hrozeb – úmyslné vs. neúmyslné
3. Dělení hrozeb – vnitřní vs. vnější
4. Základní rozdělení hrozeb
5. Typy malwaru (virus, trojský kůň, ransomware)
6. Podvodné praktiky (spam, phishing, social engineering)
7. Typy útoků (DDoS a další)
8. Nespokojený zaměstnanec (insider threat)
9. Ochrana
10. Rozdělení internetu
11. Mini-tahák

---

## Pojmy (rychlé definice)
- **Kybernetická hrozba:** potenciální příčina nežádoucí události, která může poškodit systém nebo organizaci.
- **Kybernetická událost:** konkrétní situace, kdy dojde (nebo téměř dojde) k narušení bezpečnosti.
- **Riziko:** pravděpodobnost, že hrozba využije zranitelnost a způsobí škodu; kombinace pravděpodobnosti a dopadu.
- **Malware:** škodlivý software (viry, červi, trojské koně, ransomware, spyware...).
- **Virus:** program, který se šíří připojením ke spustitelným souborům a aktivuje se spuštěním hostitele.
- **Trojský kůň (Trojan):** škodlivý program maskující se jako legitimní software; otevírá útočníkovi přístup.
- **Ransomware:** malware, který zašifruje data oběti a požaduje výkupné za dešifrování.
- **Phishing:** podvodný pokus (nejčastěji e-mailem) přimět uživatele k prozrazení citlivých údajů.
- **Spam:** nevyžádané hromadné zprávy (e-maily, SMS), obvykle reklamní nebo podvodné.
- **Social engineering:** psychologická manipulace lidí s cílem získat citlivé informace nebo přístup do systémů.
- **DDoS (Distributed Denial of Service):** útok přetížením serveru/sítě z mnoha zdrojů najednou; cíl přestane být dostupný.
- **Insider threat:** hrozba zevnitř organizace – nespokojený zaměstnanec, špión, omyl pracovníka.
- **Pentest:** penetrační test – legální simulovaný útok na systém za účelem odhalení zranitelností; v ČR musí být nahlášen.
- **Surface web:** běžně dostupná část internetu indexovaná vyhledávači.
- **Deep web:** část internetu nedostupná přes vyhledávače (e-maily, databáze, intranet, bankovní portály).
- **Dark web:** záměrně skrytá část internetu (přístup přes Tor); používán anonymně, často pro nelegální aktivity.

---

## Základní pojmy

### Co je kybernetická hrozba a riziko?

- **Hrozba** = potenciální příčina škody (co by se mohlo stát).
- **Zranitelnost** = slabina systému, kterou může hrozba využít.
- **Riziko** = pravděpodobnost × dopad; co reálně hrozí, pokud se hrozba naplní.
- **Kybernetická událost** = konkrétní incident, kdy došlo (nebo téměř došlo) k narušení bezpečnosti.

---

## Dělení kybernetických hrozeb

### Podle záměru: úmyslné vs. neúmyslné

**Neúmyslné hrozby:**
- Omylem smazaný soubor nebo data při práci na projektu
- Neúmyslné prozrazení citlivé informace (např. špatný příjemce e-mailu)
- Omylem poškození fyzického / technického aktiva
- **Přírodní pohromy:** povodně, vichřice, vysoké teploty, blesk
- **Výpadky infrastruktury:** blackout (úplný výpadek proudu), brownout (pokles napětí), elektrický šum (noise)
- Tyto události nejsme schopni zcela ovlivnit – jsou náhodné a neúmyslné

**Úmyslné hrozby:**
- Kybernetické útoky (malware, DDoS, phishing...)
- Krádeže (dat, zařízení, přihlašovacích údajů)
- Úmyslné poškození systémů nebo dat

---

### Podle původu: vnitřní vs. vnější

**Vnitřní hrozby:**
- Technické závady uvnitř organizace
- Zaměstnanci (omyl, sabotáž, špionáž)
- Fyzické události uvnitř budovy (prasknutí potrubí, požár, výpadek klimatizace v serverovně)

**Vnější hrozby:**
- Útoky z kybernetického prostoru (různé typy malwaru, DDoS, phishing...)
- Přírodní katastrofy a vnější fyzické události

---

## Základní rozdělení hrozeb

1. **Malware** – škodlivý kód (viry, červi, trojské koně, ransomware, spyware, adware...)
2. **Insider threat** – nespokojený zaměstnanec, špionáž zevnitř
3. **Podvodné praktiky** – sociální inženýrství, phishing, spam
4. **Typy útoků** – DDoS, útoky na infrastrukturu, man-in-the-middle, SQL injection...
5. **Neohlášené pentesty** – podle české legislativy jsou nelegální (i když „jen testujete")

---

## Typy malwaru

### Virus
- Program, který se šíří **připojením ke spustitelným souborům** (nebo dokumentům).
- Aktivuje se spuštěním napadeného souboru.
- Může mazat, šifrovat nebo odesílat data; zpomalovat systém.
- Šíří se kopírováním na jiná média (USB, síťové sdílení, e-mailové přílohy).

### Trojský kůň (Trojan)
- Škodlivý program, který se **vydává za legitimní software** (dle řecké pověsti o trojském koni).
- Uživatel ho sám nainstaluje v domnění, že jde o užitečný program.

**Druhy trojských koní:**
- **Downloader Trojan** – po instalaci stahuje další škodlivý software
- **Backdoor Trojan** – otevírá zadní vrátka do systému pro vzdálený přístup útočníka
- **Spy Trojan (spyware)** – sleduje aktivitu uživatele, odesílá citlivá data (hesla, klávesy, screenshoty)

### Ransomware
- Zašifruje data oběti a útočník **požaduje výkupné** za dešifrování.
- **6. generace ransomwaru** (nejmodernější):
  - Umí šifrovat i cloudová úložiště
  - Ukládá se do BIOSu/UEFI (přežije reinstalaci OS)
  - Využívá AI pro lepší cílení a vyhýbání se detekci
- Ransomware musíme sami spustit (sociální inženýrství, phishing) – proto je prevence klíčová.

---

## Podvodné praktiky

### Spam
- **Nevyžádané hromadné zprávy** (e-maily, SMS, zprávy na sociálních sítích).
- Obvykle reklamní, podvodné nebo šíří malware.
- Ochrana: spamové filtry, nesdílet e-mail veřejně, neotevírat podezřelé přílohy.

### Phishing
- Podvodný pokus (nejčastěji **e-mailem nebo falešnou webovou stránkou**) přimět oběť k prozrazení citlivých údajů (heslo, číslo karty, přihlašovací údaje).
- Útočník se vydává za důvěryhodnou instituci (banka, úřad, Microsoft...).
- **Spear phishing** = cílený phishing na konkrétní osobu nebo firmu (personalizovaný útok).
- **Vishing** = phishing přes telefon (voice phishing).
- **Smishing** = phishing přes SMS.

### Sociální inženýrství (Social Engineering)
- **Psychologická manipulace** lidí s cílem získat citlivé informace nebo přístup.
- Útočník nevyužívá technické zranitelnosti, ale **lidský faktor** (důvěra, strach, autorita, spěch).
- Příklady: vydávání se za IT podporu, záměrně zanechaný USB disk, falešná telefonní volání.
- Nejúčinnější obrana: **vzdělávání a školení zaměstnanců**.

---

## Typy útoků

### DDoS (Distributed Denial of Service)
- Útok, při kterém **velké množství zařízení (botnet) zahlcuje server nebo síť** požadavky.
- Cíl přestane být dostupný pro legitimní uživatele.
- Využívá se pro vydírání, sabotáž nebo jako odváděcí manévr.
- Obrana: CDN, rate limiting, DDoS protection služby (Cloudflare apod.).

### Další typy útoků
- **Man-in-the-Middle (MitM):** útočník se vloží mezi komunikaci dvou stran a odposlouchává / mění data.
- **SQL Injection:** vložení škodlivého SQL kódu do vstupních polí aplikace za účelem přístupu k databázi.
- **Brute Force:** opakované zkoušení hesel až do nalezení správného.
- **Zero-day útok:** útok využívající dosud neznámou (neopatchovanou) zranitelnost.

---

## Insider Threat — nespokojený zaměstnanec

- Hrozba zevnitř organizace – zaměstnanec (nebo bývalý zaměstnanec) s přístupem k systémům.
- Motivace: nespokojenost, finanční zájem, nátlak, špionáž.

**Reálný příklad – T-Mobile:**
- Nespokojený zaměstnanec unikl databázi **15 GB dat** všech uživatelů.
- Obsahovala osobní údaje, čísla karet, hesla.
- Jeden z největších datových úniků v historii telekomunikací.

**Ochrana:**
- Minimalizace oprávnění (princip nejmenšího privilegia)
- Logování a monitoring aktivity zaměstnanců
- Okamžité odebrání přístupů při odchodu zaměstnance

---

## Ochrana proti kybernetickým hrozbám

### Legislativa a normy
- **Zákon o kybernetické bezpečnosti (ZoKB)** – základní právní rámec v ČR
- **NIS2** – směrnice EU (nejnovější změny 2025) – rozšiřuje povinnosti na více organizací
- **GDPR** – ochrana osobních údajů
- **Autorský zákon** – ochrana SW a digitálního obsahu
- **Trestní zákoník** – kybernetické trestné činy (neoprávněný přístup, poškození dat...)

### Technická opatření
- Antimalware / EDR
- Firewall, IDS/IPS
- VPN (Zero Trust)
- Šifrování dat
- Zálohy (3-2-1 pravidlo: 3 kopie, 2 média, 1 mimo lokaci)
- Aktualizace a patch management

### Organizační opatření
- Firemní bezpečnostní politika a směrnice
- Školení a vzdělávání zaměstnanců (zejm. proti social engineering)
- Pravidelné audity a pentesty (nahlášené!)
- SIEM a log management
- Incident response plán

---

## Rozdělení internetu

| Vrstva | Popis | Příklady |
|--------|-------|---------|
| **Surface web** | Veřejně dostupná část, indexovaná vyhledávači | Weby, e-shopy, zpravodajství |
| **Deep web** | Nedostupná vyhledávačům, ale legální | E-maily, bankovní portály, databáze, intranet |
| **Dark web** | Záměrně skrytá, přístup přes Tor; anonymní | Anonymní fóra, nelegální tržiště, úniky dat |

> Pozn.: Deep web ≠ dark web. Deep web je obrovský a z velké části zcela legální.

---

## Mini-tahák (30–60 s)

- **Hrozba** = co se může stát; **riziko** = pravděpodobnost × dopad; **událost** = co se stalo.
- Hrozby: **úmyslné** (útok, krádež) vs. **neúmyslné** (omyl, přírodní pohroma).
- Hrozby: **vnitřní** (zaměstnanci, závady) vs. **vnější** (útoky z internetu, katastrofy).
- Malware: **virus** (šíří se soubory), **trojský kůň** (maskuje se), **ransomware** (šifruje + výkupné).
- Podvody: **phishing** (falešný e-mail/web), **social engineering** (manipulace lidí), **spam** (nevyžádané zprávy).
- **DDoS** = zahlcení serveru z mnoha zdrojů.
- **Insider threat** = hrozba zevnitř (T-Mobile: 15 GB únik).
- Ochrana: legislativa (ZoKB, NIS2), firemní politika, technická opatření (firewall, antimalware, VPN, zálohy).
- Internet: **surface** (viditelný) → **deep** (skrytý, legální) → **dark** (anonymní, Tor).

---

## Zdroje
- [NÚKIB – Kybernetické hrozby](https://nukib.gov.cz/cs/kyberneticka-bezpecnost/hrozby/)
- [Zákon o kybernetické bezpečnosti (ZoKB)](https://www.zakonyprolidi.cz/cs/2014-181)
- [NIS2 Directive](https://eur-lex.europa.eu/legal-content/CS/TXT/?uri=CELEX%3A32022L2555)
- [ENISA – Threat Landscape](https://www.enisa.europa.eu/topics/cyber-threats/enisa-threat-landscape)