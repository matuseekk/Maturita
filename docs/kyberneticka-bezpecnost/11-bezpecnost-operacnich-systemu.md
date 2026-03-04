# 11. Bezpecnost operacnich systemu z pohledu kybernetiky


## Deleni opatreni
Kybernetickou bezpecnost muzeme zjednodusene delit na:
- **Fyzickou bezpecnost** (ochrana prostoru a zarizeni)
- **Softwarovou/technickou bezpecnost** (ochrana systemu, uctu, siti a dat)
- (casto se jeste resi) **Organizacni opatreni** (pravidla, role, procesy)

---

## Fyzicka bezpecnost

### Klient (pracovni stanice / notebook)
- Zamykaci skrin u stolu (uzamceni techniky, dokumentu, nosicu).
- U notebooku pouzivat **bezpecnostni zamek (Kensington lock)**, pokud je k dispozici.
- Nenechavat zarizeni bez dozoru na verejnych mistech.

### Server
- Servery zamknout do **racku** (uzamykatelne dvere).
- Zamknout **serverovnu** a zavest **omezene pristupy** (jen opravneny personal).
- Serverovna by mela byt idealne:
  - bezne neoznacena / nenapadna (snizeni rizika cileho utoku),
  - se systemem evidence vstupu (karta, klic, kod),
  - s kamerami / alarmem dle moznosti.

---

## Softwarova a pristupova bezpecnost

### Overovani (autentizace)
- Prihlasovani pres:
  - **heslo**,
  - **certifikat**,
  - **token** (napr. aplikace, HW token, jednorazove kody).
- **Dvoufaktorove overeni (2FA/MFA)**:
  - kombinace dvou ruznych faktoru, napr. **heslo + jednorazovy kod / aplikace / biometrie**.
- Biometrie (Face ID, otisk, sken sitnice) muze byt faktor, ale porad je dulezite mit i dalsi zabezpeceni.

### Udrzba a sprava
- Pravidelna udrzba systemu a dat (aktualizace, kontrola logu, revize uctu).
- Minimalizace opravneni (uzivatel ma jen to, co potrebuje).

---

## Operacni system (stanice i server)
- Pouzivat aktualni verze:
  - pravidelne **aktualizace OS**,
  - aktualni **ovladace** (kde to dava smysl a je to overene).
- **Firewall** (lokalni i sitovy).
- **Antimalware/EDR** (podle prostredi).
- **VPN** pro vzdaleny pristup.
  - Doporuceni: pristup resit principem **Zero Trust** (neverit automaticky, vse overovat, omezovat pristupy).

---

## Ochrana dat
- **Sifrovani dat** (disku i prenosu) – minimalne na noteboocich a prenosnych mediich.
- **RAID** (napr. RAID 1) zvysuje dostupnost pri poruse disku, ale **nenahrazuje zalohy**.
- **Automaticke zalohovani**:
  - idealne **mimo hlavni lokaci** (off-site),
  - testovat obnovu (restore test).
- Cloud:
  - vlastni cloud muze byt OK (kdyz je dobre spravovany),
  - u verejnych cloudu resit **sifrovani**, umisteni dat a smluvni podminky (GDPR apod.).

---

## Ochrana stanic pomoci serveru / dohled
- Centralizovana sprava a dohled, napr.:
  - **SIEM systemy**,
  - **log management** (sběr, centralizace a vyhodnoceni logu),
  - monitoring dostupnosti a bezpecnostnich udalosti.

---

## Ucty, role a hesla
- Kazdy server by mel mit spravovane admin ucty:
  - idealne oddeleny admin ucet (ne admin na bezny browsing),
  - silna hesla + MFA, kde je to mozne.
- Pro kazdou sluzbu oddelit pristupy:
  - **jina sluzba = jiny ucet / jine heslo**,
  - omezeni dopadu pri uniku (segmentace pristupu).

---

## Recyklace a likvidace (citliva data)
- Citliva data nelikvidovat jen „smazanim“.
- Bezpecna likvidace:
  - fyzicka destrukce (skartovacka na disky / drceni) – nejjistejsi,
  - nebo bezpecne prepsani (wipe) – typicky vice pruchodu (dnes casto staci spravne jednopruhove prepsani podle metody a typu disku; u SSD je lepsi pouzit vyrobni secure erase).
- Dulezite: u SSD nefunguje „klasicke“ prepisovani vzdy spolehlive kvuli wear-levelingu.

## Mini-tahak
- Fyzicka bezpecnost: zamky, rack, serverovna, omezeny pristup.
- Softwarova bezpecnost: hesla + MFA, aktualizace, firewall, antimalware, VPN.
- Data: sifrovani, zalohy off-site, RAID neni zaloha.
- Dohled: logy, SIEM, monitoring.
- Likvidace: secure erase / destrukce.
