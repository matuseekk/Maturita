# 13. Hardware a periferne zarizeni

## Cile (co musis umet rict)
- Popsat hlavni komponenty PC (MB, CPU, GPU, RAM, uloziste, zdroj) a jejich funkci.
- Vysvetlit zakladni rozhrani (socket, PCIe, M.2, SATA, DIMM/SO-DIMM) a k cemu jsou.
- Uvest rozdily HDD vs SSD, typy RAID a proc RAID neni zaloha.
- Strucne popsat typy tiskaren a jejich vyhody/nevýhody.

---

## Zakladni deska (motherboard)
Zakladni deska je zakladem pocitace – propojuje jednotlive soucasti do funkcniho celku a zajistuje jejich komunikaci a napajeni.

### Jak se komponenty pripojuji
- **Patice (socket)**: CPU
- **Sloty**: typicky RAM a rozsirujici karty (GPU apod.)
- **Konektory**: disky, periferie, napajeni (SATA, M.2, USB header, ATX konektory…)

### BIOS/UEFI (ROM/flash pamet)
Na zakladni desce je pamet (typicky **EEPROM/flash**), kde je ulozen **BIOS/UEFI**:
- pouziva se pri startu PC pro inicializaci a konfiguraci hardwaru,
- pak preda rizeni bootloaderu/OS.

### Podle ceho vybirame zakladni desku
- **format desky** (ATX, mATX, ITX) podle skrine
- kompatibilita s **procesorem** (socket + chipset)
- typ a pocet slotu pro **RAM** (DDR4/DDR5, DIMM)
- **napajeci kaskada (VRM)** (dulezite pri vyssim vykonu/taktovani)
- konektivita: PCIe sloty, M.2, SATA, USB, LAN, Wi‑Fi
- I/O porty: USB, HDMI/DP (u iGPU), audio, LAN…

---

## Sockety (patice pro CPU)
**Socket** = misto, kam se pripojuje procesor.

- **PGA (Pin Grid Array)** – piny jsou na procesoru (casto AMD u starsich generaci).
- **LGA (Land Grid Array)** – piny jsou v patici na desce, CPU ma kontaktni plosky (typicky Intel, a nove i AMD u AM5).
- **BGA (Ball Grid Array)** – CPU/GPU je **pripajene napevno** na desce (notebooky, mobilni zarizeni). Bez bezne vymeny.

---

## Sloty a sbernice
### RAM sloty
- **DIMM** – desktop
- **SO‑DIMM** – notebook

### Grafika a rozsireni
- **AGP** – historicky slot pro grafiku (dnes uz prakticky ne)
- **PCI Express (PCIe)** – moderni standard:
  - x1, x4, x8, x16 (x16 typicky pro GPU)

---

## Cipova sada (chipset)
Chipset je sada logiky (dnes casto jedna hlavni „platform controller“ cast), ktera resi komunikaci mezi komponentami a I/O.

Historicky se u desktopu uvadelo:
- **Northbridge (severni mustek)** – CPU, RAM, GPU (rychle veci)
- **Southbridge (jizni mustek)** – USB, SATA, PCI, audio, LAN (pomalejsi I/O)

Dnes:
- velka cast funkcí northbridge je integrovana primo v CPU,
- zbytek je v chipsetu na desce.

---

## Procesor (CPU)
CPU vykonava strojovy kod programu.

### Zakladni casti CPU
- **ALU (aritmeticko‑logicka jednotka)** – vypocty, logicke operace
- **ridici jednotka** – ridi vykonavani instrukci a komunikaci s ostatnimi castmi

### Dulezite parametry
- **frekvence** (GHz) – u modernich CPU se meni dle zatizeni (boost)
- **pocet jader** a **vlaken**
- **cache** (L1/L2/L3) – zrychluje pristup k datum
- **TDP/spotreba** a naroky na chlazeni
- **instrukcni sady** (napr. x86‑64, AVX; u ARM jine)

### Hyper‑Threading / SMT
- umoznuje jednomu jadru zpracovavat vice vlaken (virtualne „vice jader“),
- zlepsuje vykon hlavne u paralelnich uloh (ne vzdy 2×).

Poznamka: „HyperTransport“ je stary AMD pojem pro propojeni (dnes spis Infinity Fabric apod.).

---

## Graficka karta (GPU)
GPU vytvari obraz a posila ho na zobrazovac (monitor).

### Druhy podle umisteni
- **integrovana grafika (iGPU)** – soucast CPU nebo chipsetu (mensi vykon)
- **dedikovana grafika** – samostatna karta v PCIe (vykonnejsi)
- **externi grafika (eGPU)** – mimo PC (typicky pres Thunderbolt)

### Zakladni pojmy
- **VRAM (napr. GDDR6/GDDR6X)** – pamet grafiky
- vystupy: **HDMI, DisplayPort (DP), DVI, VGA (D‑Sub)** (VGA uz spis historicky)

---

## Uloziste (pevny disk / SSD)
Uloziste = nevolatilni pamet pro data, OS a programy.

### Typy
- **HDD** – mechanicky disk (plotny + hlavicky)
  - velka kapacita za nizkou cenu
  - pomalejsi a nachylnejsi na otrasy
- **SSD** – flash pamet
  - rychle cteni/zapis, nizka latence
  - omezeny pocet zapisu (zivotnost se udava napr. TBW), ale v praxi obvykle dostatecna
- **SSHD** – hybrid (HDD + mala SSD cache), dnes uz spis okrajove

### Rozhrani
- **SATA** (SATA I/II/III) – bezne 2,5"/3,5" disky
- **M.2**:
  - M.2 SATA (jede pres SATA)
  - M.2 **NVMe** (jede pres PCIe – rychlejsi)
- (historicky) eSATA

### Velikosti
- **2,5"** – notebooky, nektere servery
- **3,5"** – desktop a servery/racky

---

## RAID (dulezite!)
RAID zlepsuje dostupnost nebo vykon, ale **RAID neni zaloha**.

- **RAID 0 (striping)**: vyssi vykon, kapacity se scitaji, ale pri poruse 1 disku ztrata vsech dat (min. 2 disky)
- **RAID 1 (mirroring)**: data jsou na obou discich, vysledna kapacita = kapacita jednoho disku (min. 2 disky)
- **RAID 5**: striping + parita, prezije poruchu 1 disku (min. 3 disky)

Zaloha = oddelena kopie (idealne i mimo lokaci), ktera se da obnovit.

---

## ROM / RAM (pameti)
### ROM (Read Only Memory) – obecne
Pamet pro firmware, data zustanou i bez napajeni.
Typy (historicky/teoreticky):
- ROM (vyrobcem naprogramovana)
- PROM (naprogramujes 1×)
- EPROM (mazani UV svetlem)
- EEPROM/Flash (mazani elektricky) – bezne pro BIOS/UEFI

### RAM (Random Access Memory)
- volatilni pamet (po vypnuti se data ztrati)
- uklada instrukce a data, se kterymi PC prave pracuje
- parametry: kapacita, frekvence, casovani, generace (DDR3/DDR4/DDR5)

Formaty:
- **DIMM** (desktop)
- **SO‑DIMM** (notebook)

---

## Zdroj (PSU)
Zdroj napaji vsechny komponenty a prevadi sitove AC na DC napeti.

### Zakladni konektory
- **24‑pin ATX (20+4)** – hlavni napajeni zakladni desky
- **4/8‑pin EPS** – napajeni CPU
- **PCIe 6/8‑pin** – napajeni GPU (podle karty)
- **SATA power**, (historicky) Molex

### Barvy vodicu (klasicky ATX)
- zluta: +12 V
- cervena: +5 V
- oranzova: +3,3 V
- cerna: GND (zem)

### Dulezite parametry zdroje
- **vykon (W)**
- **ucinnost (80 PLUS)** – jak moc energie jde na teplo vs. do komponent
- kvalita ochrannych prvku (OCP/OVP/OTP…).

---

## Periferie – tiskarny (prehled)
### Jehlickova (maticova)
**Vyhody**
- velmi levny tisk (paska)
- zvladne prurezovy papir, kopie (prutah)

**Nevyhody**
- hlucna
- nizsi kvalita tisku
- pomalejsi, omezeny pocet barev

### Inkoustova (inkjet)
- inkoust je vystrelen na papir (termalne / piezo)

**Vyhody**
- dobra kvalita barevnych tisku
- nizka cena zarizeni, casto multifunkce

**Nevyhody**
- drahy inkoust
- zasichani trysek pri necinosti

### Laserova
- toner + nabojovy valec, zapekani toneru

**Vyhody**
- rychla, vyhodna na velky objem
- ostre texty

**Nevyhody**
- drazsi porizeni, spotrebak
- nekterym lidem vadi zapach pri zapekani

### Termalni
- tisk na termopapir (uctenky)

**Vyhody**
- rychla a jednoducha
- levny provoz

**Nevyhody**
- tisk casem bledne, na slunci muze zcernat
- vyzaduje termocitlivy papir

---

## Mini-tahak (na 30–60 s)
- MB spojuje komponenty; BIOS/UEFI startuje PC.
- Socket: PGA/LGA/BGA; sloty: DIMM, PCIe; uloziste: SATA vs NVMe.
- CPU: jadra/vlakna, frekvence, cache, SMT.
- GPU: iGPU vs dedikovana; vystupy HDMI/DP.
- HDD vs SSD; RAID zlepsuje dostupnost/vykon, ale neni zaloha.
- PSU: 24‑pin, EPS, PCIe napajeni; ucinnost.
- Tiskarny: jehlickova/inkoustova/laserova/termalni.
