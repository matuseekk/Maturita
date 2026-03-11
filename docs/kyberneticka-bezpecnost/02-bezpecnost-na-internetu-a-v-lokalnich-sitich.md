# 02. Bezpečnost na internetu a v lokálních sítích

## Cíle (co musíš umět říct)
- Popsat bezpečnostní opatření v lokálních sítích (fyzická, softwarová, organizační).
- Vysvětlit firemní bezpečnostní politiku a co zahrnuje.
- Popsat ochranu dat (šifrování, zálohy, RAID, recyklace médií).
- Vysvětlit bezpečnost na internetu – kybernetický prostor, digitální stopa, HTTPS, VPN.

---

## Osnova
1. Lokální sítě – bezpečnostní politika
2. Fyzická bezpečnost (klient, server)
3. Softwarová bezpečnost
4. Operační systém
5. Ochrana dat
6. Ochrana stanic pomocí serveru
7. Recyklace médií
8. Bezpečnost na internetu
9. Digitální stopa
10. Mini-tahák

---

## Pojmy (rychlé definice)
- **Firemní bezpečnostní politika:** soubor pravidel a směrnic, která řídí přístupy, hesla, oprávnění a fyzickou ochranu v organizaci.
- **Active Directory (AD):** adresářová služba (např. Windows Server), která spravuje uživatele, skupiny, práva a přihlášení v síti.
- **SIEM:** Security Information and Event Management – systém pro sběr a analýzu bezpečnostních logů v reálném čase.
- **VPN (Zero Trust):** virtuální privátní síť s principem „nikomu nevěřit automaticky" – každý přístup se ověřuje.
- **Kybernetický prostor:** definován zákonem o kybernetické bezpečnosti; vše digitální – internet, sítě; dělí se na národní a mezinárodní.
- **Digitální stopa:** záznamy o aktivitě uživatele v digitálním prostředí; může být úmyslná (fotky, videa) nebo neúmyslná (metadata, HTTP protokol).
- **HTTPS:** šifrovaný webový protokol; aktuálně v.2, zavádí se v.3.
- **RAID 1:** zrcadlení disků pro ochranu dat před selháním.
- **Skartovačka na disky:** fyzické zničení média s citlivými daty.

---

## Lokální sítě — bezpečnostní politika

Lokální sítě jsou řízeny **bezpečnostní politikou, řády a směrnicemi** organizace.

### Firemní politika zahrnuje:

1. **Přístupy do budov a místností**
   - přístupní karty, biometrika, klíče

2. **Pravidla pro přihlášení a hesla**
   - jak jsou tvořeny přihlašovací údaje (délka, složitost, platnost)

3. **Ověření přihlašovacích údajů**
   - např. Windows Server s Active Directory (AD)

4. **Pravidla pro přístupy k diskům a souborům**
   - definování skupin uživatelů, práva a oprávnění (čtení, zápis, spouštění)

5. **Poštovní schránky**
   - pravidla pro firemní e-mail (šifrování, archivace, přístupy)

6. **Fyzická bezpečnost**
   - zamykání prostor, ochrana hardware

7. **Práce s daty**
   - pravidla pro ukládání, sdílení a mazání firemních dat

> O firemní politice lze mluvit poměrně dlouho – zahrnuje hodně oblastí.

---

## Fyzická a softwarová bezpečnost

### Fyzická bezpečnost

**Klient (pracovní stanice / notebook):**
- Zamykací skříně u stolu (uzamčení techniky a dokumentů)
- U notebooku bezpečnostní zámek (Kensington lock)

**Server:**
- Servery zamknout do **racku**
- Zamknout **serverovnu** s omezeným přístupem
- Serverovna by měla být neoznačená / utajovaná místnost

### Softwarová bezpečnost

**Ověřování (autentizace):**
- Heslo, certifikát nebo různé tokeny
- **Dvoufázové ověření (2FA/MFA):** např. biometrika + heslo
- Používá se Face ID, sken sítnice

**Údržba:**
- Pravidelná údržba dat a systémů

---

## Operační systém

- Používat **aktuální verze**: pravidelné aktualizace OS a ovladačů
- **Firewall** (lokální i síťový)
- **Antimalware / EDR**
- **VPN** – ideálně Zero Trust VPN
  - Zero Trust = „nikomu nevěř automaticky, vše ověřuj, omezuj přístupy"

---

## Ochrana dat

- **Šifrování** – data by měla být šifrována jak při přenosu, tak v klidu
- **RAID 1** – zrcadlení disků (ochrana před selháním disku)
- **Automatické zálohování dat** – ideálně na jiné místo než sídlo firmy
- **Vlastní cloud** – OK (kontrola nad daty)
- **Velký firemní cloud** – riziko (výjimka: Proton má šifrování)

---

## Ochrana stanic pomocí serveru

- **SIEM systémy** (Security Information and Event Management)
  - sběr, korelace a analýza bezpečnostních událostí v reálném čase
- **Log managery** – centrální správa logů ze všech zařízení
- Každý server má svého **administrátora se speciálním heslem**
- Pro každou službu **jiný uživatel / jiné heslo** (vícestupňová ochrana)

---

## Recyklace médií

Při vyřazení zařízení s citlivými daty:

- **Skartovačka na disky** – fyzické zničení (nejbezpečnější)
- **7× formátování s nulami** – relativně bezpečné softwarové smazání

---

## Bezpečnost na internetu

**Kybernetický prostor:**
- Definován v **zákoně o kybernetické bezpečnosti** (nejnovější změny – 2025 + NIS2)
- Zahrnuje principiálně vše digitální: internet, sítě
- Dělí se na **národní** a **mezinárodní** kybernetický prostor
- V ČR se o národní kybernetický prostor stará **CZ.NIC** (a NÚKIB)

**Doporučení pro bezpečný pohyb na internetu:**
- Minimalizovat **digitální stopu**
- Navštěvovat bezpečné weby s **HTTPS** (v.2, zavádí se v.3)
- **Odmítnout všechny cookies** (nebo přijmout jen nezbytné)
- Používat **VPN**, ideálně Zero Trust
- Pro přenos a ukládání dat používat **certifikovaná úložiště se šifrováním** (např. Proton Drive)

---

## Digitální stopa

**Digitální stopa** = záznamy, které zanecháváme v digitálním prostředí.

> Poznámka: digitální stopa zatím není zavedena přímo v zákoně jako pojem (zavádí se přibližně od listopadu 2024), takže se nemusí brát jako důkaz v právním řízení.

### Typy digitální stopy:

- **Úmyslná** – fotky a videa, příspěvky na sociálních sítích, co vědomě zveřejňujeme
- **Neúmyslná** – data sdílená v rámci protokolů (např. HTTP), metadata souborů, IP adresa, cookies

**Metadata** = data o datech (např. kdy byl soubor vytvořen, z jakého zařízení, GPS souřadnice fotky apod.)

---

## Mini-tahák (30–60 s)

- Lokální sítě řídí **bezpečnostní politika** – přístupy, hesla, oprávnění, AD.
- Fyzická bezpečnost: zamykací skříně, rack, serverovna s omezeným přístupem.
- Softwarová bezpečnost: 2FA, firewall, antimalware, VPN (Zero Trust).
- Ochrana dat: šifrování, RAID 1, zálohy mimo sídlo, skartovačka na disky.
- Internet: HTTPS, odmítnout cookies, VPN, minimalizovat digitální stopu.
- Kybernetický prostor = definován zákonem (ZoKB, NIS2); CZ.NIC chrání národní prostor.
- Digitální stopa: úmyslná (fotky) vs. neúmyslná (metadata, HTTP).

---

## Zdroje
- [Zákon o kybernetické bezpečnosti (ZoKB)](https://www.zakonyprolidi.cz/cs/2014-181)
- [NIS2 – Směrnice EU o kybernetické bezpečnosti](https://eur-lex.europa.eu/legal-content/CS/TXT/?uri=CELEX%3A32022L2555)
- [NÚKIB – Národní úřad pro kybernetickou a informační bezpečnost](https://nukib.gov.cz)
- [CZ.NIC](https://www.nic.cz)