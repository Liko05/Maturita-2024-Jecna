# Teorie OS - fungování OS, struktura OS, správa procesů, pseudoparalelismus

## Fungovani OS

- Jadro (kernel):
    - Jadro Linuxu je srdcem operacniho systemu. Zajistuje zakladni funkce jako rizeni pameti, spravu procesu, souborovy
      system, sitovou komunikaci a ovladace zarizeni.
    - Jadro je spusteno jako prvni cast operacniho systemu a prebira kontrolu nad hardwarem
    - Jadro provadi operace na nizke urovni, jako spravu pameti, planovani procesu, komunikaci se zarizenimi a
      souborovym systemem.
- Uzivatelsky prostor:
    - Nad jadrem linuxu je uzivatelsky prostor, ve kterem bezi uzivatelske procesy a aplikace.
    - Uzivatelske procesy bezi v izolovanem prostredi a komunikuji s jadrem prostrednictvim systemovych volani (system
      calls)
    - Aplikace bezi ve virtualnim prostredi, ktere jim poskytuje abstrakci hardwaru a dalsi systemove zdroje, jako jsou
      knihovny, sitova rozhrani a souborovy system.
- Sprava procesu:
    - Jadro spravuje spustene procesy v systemu.
    - Planovac procesu rozhoduje, ktery proces bude spusten, pozastaven nebo ukoncen a jak bude cas procesoru pridelovan
      jednotlivym procesum.
    - Jadro poskytuje mechanismy pro komunikaci a synchronizaci mezi procesy, jako jsou vlakna, semafory, fronty zprav
      apod.
- Sprava pameti:
    - Jadro Linuxu spravuje pametovy prostor a alokuje pamet pro jednotlive procesy
    - Zajistuje virtualizaci pameti, ktera umoznuje kazdemu procesu videt svuj vlastni adresovy prostor.
    - Jadro resi spravu stranek v pameti, strankovani, vymenu stranek na disk a spravu docasne pameti (cache).
- Souborovy system:
    - Jadro linuxu poskytuje abstrakci nad ruznymi typy souborovych systemu, ktere umoznuji pristup a praci se soubory a
      adresari
    - Souborovy system definuje strukturu datovych blokum, metadat a atributu souboru.
    - Linux podporuje ruzne souborove systemy, jako ext4, Btrfs, XFS, NTFS, FAT ktere mohou byt pouzity pro ruzna media,
      jako pevne disky, SSD, USB disky apod.
    - Jadro poskytuje rozhrani pro souborove operace, jako je cteni, zapis, vytvareni, mazani a prejmenovani souboru a
      adresaru.

### Sitova Komunikace:

- Jadro Linuxu poskytuje podporu pro sitovou komunikaci. (napr. TCP/IP)
- Zahrnuje ovladace pro sitova zarizeni, protokoly pro sitovou komunikaci (napr. TCP/IP) a sitove rozhrani pro
  komunikaci s aplikacemi.
- Jadro zajistuje prenos dat pres sit, smerovani paketu, spravu sitovych spojeni a poskytuje sitove sluzby, jako jsou
  sockety a sitove rozhrani

### Ovladace zarizeni:

- Jadro linuxu obsahuje ovladace ozarizeni, ktere umoznuji komunikaci s hardwarem jako jsou klavesnice, mys, displeje,
  sitove karty, zvukove karty a dalsi periferni zarizeni.
- Ovladace zarizeni jsou soucasti jadra a zprostredkovavaji komunikaci mezi hardwarem a operacnim systemem.

### Systemova volani:

- Systemova volani jsou rozhranim mezi uzivatelskymi procesy a jadrem
- Umoznuji uzivatelskym procesum komunikovat s jadrem a ziskavat pristup k jadrovym funkcim, jako je sprava procesu,
  souborovy system, sitova komunikace apod.
- Priklady systemovych volani zahrnuji vytvareni procesu, otevirani a zavirani souboru, cteni a zapis dat, sitove
  operace a spravu pameti.

## Struktura OS

![struktura-os.png](struktura-os.png)

### Ukoly OS:

- Spoustet a dohlizet na uzivatelske programy
- Efektivni vyuziti HW
- Usnadnit reseni uzivatelskych problemu
- Ucinit pocitact (snaze) pouzitelny

### Sklada se z  (struktura)

- Jadro: Po zavedeni do pameti ridi cinnost pocitace, poskytuje procesum sluzby a resi spravu prostredku a spravu
  procesu
- Ovladac: zvlastni (pod)program pro ovladani konkretniho zarizeni standardnim zpusobem. Pouziti strategie s ovladaci
  umoznuje snadnou konfigurovatelnost technickeho vybaveni.
- Prikazovy procesor: program, ktery umoznuje uzivatelum zadavat prikazy ve specialnim obvykle jednoduchem jazyce.
- Podpurne programy: do teto kategorie jsou mnohdy zahrnovany i prekladace (jazyk C v OS UNIX) a sestavujici programy.
  Stoji na stejnem miste jako aplikacni programy

## Jadro OS

Jadro se zpravidla deli na dve podstatne casti:

- Sprava procesu: sprava procesu (prakticky neni u jednoduchych OS) resi problematiku aktivovani a deaktivovani procesu
  podle jejich priority resp. pozadavku na prostredky.
- Sprava prostredku: zajistuje cinnost V/V zarizeni, prideluje pamet, pripadne procesory. Velmi dulezitou casti spravy
  prostredku je: sprava souboru - zpusob ukladani souboru a pristupu k nim. Moderni OS zajistuji jednotny pohled na
  soubory a zarizeni. Zarizeni jsou povazovany za soubory se specialnim jmenem.

### Monoliticka jadra (Monolithic kernel)

V monolitickém jádru všechny služby operačního systému běží spolu s hlavním vláknem jádra a tedy i ve stejné oblasti
paměti. To umožňuje neomezený a efektivní přístup k hardware. Mnozí vývojáři zastávají názor, že monolitické systémy je
jednodušší navrhnout i implementovat než ostatní řešení a jsou extrémně účinné, když jsou dobře napsané. Hlavní
nevýhodou je závislost mezi systémovými komponentami – chyba v libovolném ovladači zařízení může shodit celý systém – a
fakt, že velká jádra mohou být těžko udržovatelná.
![kernel-software.png](kernel-software.png)

### Microkernel

Mikrojádro poskytuje jen základní funkčnost nezbytnou pro vykonávání služeb; většina služeb je realizována
specializovanými ovladači v uživatelském prostoru. Mikrojádro definuje jednoduché abstrakce hardwaru se soupravou
primitivních funkcí nebo systémových volání implementujících minimální služby OS jako je správa paměti nebo
meziprocesová komunikace(IPC). Mikrojádra jsou jednodušší než monolitická jádra, delegování úkolů na ovladače však
snižuje efektivitu systému, proto musí být mikrojádro navrženo tak, aby byl tento dopad minimalizován.
![microkernel.png](microkernel.png)

## Sprava procesu

- Proces: cinnost rizena programem, provedeni programu "process" nebo "task"
- Proces potrebuje pro svou realizaci jiste zdroje (CPU, pamet, I/O zarizeni, ...)
- Z hlediska spravy procesu je OS zodpovedny za:
    - Vytvareni a ruseni procesu
    - Potlaceni a obnoveni procesu
    - Synchronizace procesu a jejich vzajemna komunikace
- Variantou procesu je tzv. Vlakno - jednotka planovani cinnosti definovana v programu. Vlakna pouzivaji zdroje
  pridelene procesu.

### Planovani procesu

Plánování procesů (anglicky scheduling) je v informatice úkol jádra operačního systému, ve kterém je spuštěno více
procesů najednou. Týká se tedy víceúlohových systémů podporujících multitasking anebo multithreading, které využívají
paralelizmus anebo pseudoparalelizmus. Plánování procesů řeší výběr, kterému následujícímu procesu bude přidělen
procesor a proces tak poběží, přičemž výběr je závislý na prioritách jednotlivých procesů a algoritmu, kterým výběr
proběhne.

### Dlouhodobe planovani

Dlouhodobé plánování (anglicky long-term) se označuje též jako plánování úloh (anglicky job scheduling) je výběr, která
úloha bude spuštěna. Má význam zejména u dávkového zpracování. Jeho účelem je naplánovat spouštění úloh tak, aby byl
počítač maximálně využit, například vhodného mixu úloh, které jsou náročné na I/O nebo CPU. V současné době není obvykle
u desktopových systémů implementován, avšak je velmi důležitý u operačních systémů reálného času, protože systém by v
případě spuštění více procesů, než může bezpečně zvládnout, nemohl plnit garantované limity.

### Strednedobe planovani

Střednědobé plánování (anglicky mid-term) používají systémy s virtuální pamětí. Jde o výběr, který blokovaný nebo
připravený proces bude odsunut z vnitřní paměti na pevný disk, je-li vnitřní paměti nedostatek (anglicky swapping out a
swapping in). Je chybou považovat stránkování paměti za střednědobé plánování, protože v tomto případě se odkládá celý
proces. Důvodem pro odložení procesu může být absence aktivity procesu, nízká priorita, časté výpadky stránek,
odblokovaný proces, který již nečeká na systémové prostředky nebo alokace příliš velké části paměti, když je potřeba
paměť pro jiné procesy.

### Kratkodobe planovani

Krátkodobé plánování (anglicky short-term) se označuje též jako plánování procesoru (anglicky CPU scheduling – viz další
odstavec), při němž se vybírá, kterému z připravených procesů bude přidělen procesor. Používá se ve všech víceúlohových
systémech.
Při plánování procesoru se v operačním systému plánovač (anglicky scheduler) rozhoduje, kterému procesu bude přidělen
procesor, a tedy který proces v následujícím časovém úseku bude procesor počítače využívat pro svůj běh. K plánování
procesoru dochází v následujících situacích (podrobnosti o stavech procesu viz článek o procesech):

- pokud nektery bezici proces prejde do stavu blokovany
- pokud nektery proces skonci
- pokud je bezici proces preveden do stavu pripraveny
- pokud je nektery proces preveden ze stavu blokovany do stavu pripraveny

### Pseudoparalelismus

Ve víceúlohových systémech je obvykle k dispozici méně procesorů, než je procesů, které by měly zároveň běžet. Proto se
u takových systémů využívá pseudoparalelismus, který umožňuje mít zdánlivě spuštěno zároveň více procesů. Procesy čekají
ve frontě a postupně je jim na určitou dobu (tzv. časové kvantum) přidělován procesor. Je-li přepínání dostatečně
rychlé, vzniká dojem, že procesy běží zároveň. K přepínání dochází zhruba 100–1000krát za sekundu (podle výkonu počítače
nebo podle výše režie přepínání, kterou chceme obětovat ve prospěch plynulosti). Při přepínání procesů je nutné, aby
proces po opětovném spuštění pokračoval od stejného místa, ve kterém byl přerušen a aby v procesu až na časové zpoždění
nebylo poznat, že k přerušení došlo. Z tohoto důvodu je nutné při přerušení vykonávání procesu (mezi dvěma libovolnými
strojovými instrukcemi) uschovat kompletní stav procesoru a při opětovném přidělení procesoru stejnému procesu tento
stav kompletně obnovit. Kompletní uložení stavu procesu označujeme jako uložení kontextu (anglicky context save) a
obnovení kontextu (anglicky context restore). Při výměně procesů na procesoru dochází k uložení kontextu jednoho a
obnovení kontextu druhého. Tuto činnost označujeme souhrnně jako změna kontextu (anglicky context switch).

### Tabulka popisu procesu (PCB)

Tabulka popisu procesů (anglicky process control block, zkratka PCB) je datová struktura v jádře operačního systému,
která uchovává data potřebná k běhu procesu. Každý proces má svoji PCB, která je využívána při změně kontextu(anglicky
context switch) k uložení stavu procesu.
