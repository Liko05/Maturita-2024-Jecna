# OSI model sítí, rodina protokolů TCP/IP a porovnání s OSI modelem, pojmy: rámec, paket, zapouzdření dat na jednotlivých vrstvách, spojovaná a nespojovaná služba

## ISO/OSI a TPC/IP

- OSI - Open Systems interconnection, vytvořil International Standard Organization IEEE
- TCP/IP - Vytvořil ARPNET (Advanced Research Project Agency Network)

![OSI-TCP-LAYERS.PNG](OSI-TCP-LAYERS.PNG)

![OSI-MODEL.PNG](OSI-MODEL.PNG)

![osi-examples.png](osi-examples.png)

## ISO/OSI:

- Aplikační vrstva = Účelem vrstvy je poskytnout aplikacím přístup ke komunikačnímu systému a umožnit tak jejich
  spolupráci.
- Prezentační vrstva = Funkcí vrstvy je transformovat data do tvaru, který používají aplikace (šifrování, konvertování,
  komprimace).Formát dat (datové struktury) se může lišit na obou komunikujících systémech, navíc dochází k transformaci
  pro účel přenosu dat nižšími vrstvami. Vrstva se zabývá jen strukturou dat, ale ne jejich významem který je znám jen
  vrstvě aplikační.
- Relační vrstva = Smyslem vrstvy je organizovat a synchronizovat dialog mezi spolupracujícími relačními vrstvami obou
  systémů a řídit výměnu dat mezi nimi. Umožňuje vytvoření a ukončení relačního spojení, synchronizaci a obnovení
  spojení, oznamování výjimečných stavů.
- Transportní vrstva = Tato vrstva zajišťuje přenos dat mezi koncovými uzly. Jejím účelem je poskytnout takovou kvalitu
  přenosu, jakou požadují vyšší vrstvy. Vrstva nabízí spojově (TCP) a nespojově orientované (UDP) protokoly.
- Síťová vrstva = Tato vrstva se stará o směrování v síti a síťové adresování. Poskytuje spojení mezi systémy, které
  spolu přímo nesousedí. Obsahuje funkce, které umožňují překlenout rozdílné vlastnosti technologií v přenosových
  sítích.
- Linková vrstva = Poskytuje spojení mezi dvěma sousedními systémy. Uspořádává data z fyzické vrstvy do logických celků
  známých jako rámce (frames). Seřazuje přenášené rámce, stará se o nastavení parametrů přenosu linky, oznamuje
  neopravitelné chyby. Formátuje fyzické rámce, opatřuje je fyzickou adresou a poskytuje synhcronizaci pro fyzickou
  vrstvu.
- Fyzická vrstva = Specifikuje fyzickou komunikaci. Aktivuje, udržuje a deaktivuje fyzické spoje (např. komutovaný spoj)
  mezi koncovými systémy. Fyzické spojení může být dvoubodové (sériová linka) nebo mnohobodové (Ethernet). Fyzická
  vrstva definuje všechny elektrické a fyzikální vlastnosti zařízení. Obsahuje rozložení pinů, napěťové úrovně a
  specifikuje vlastnosti kabelů, stanovuje způsob přenosu "jedniček a nul". Huby, opakovače, síťové adaptéry a
  hostitelské adaptéry (Host Bus adapters používáme v síťových úložištích SAN) jsou právě zařízení pracující na této
  vrstvě.
    - Navazování a ukončování spojení s komuniakčním médiem.
    - Spolupráce na efektivním rozložení všech zdrojů mezi všechny uživatele.
    - Modulace neboli konverze digitálních dat na signály používané přenosovým médiem (a zpět) (A/D, D/A převodníky).

## PDU

- protocol data unit - obecný název pro jednotky dat na jednotlivých vrstvách
- Na aplikační vrstvě se vyskytují Data.
- Na transportní vrstvě se vyskytuje Segment (TCP) a Datagram (UDP).
- Na internetové vrstvě Packet.
- Na linkové vrstvě Frame.
- Na fyzické vrstvě bits, light (Fyzická data přenášené po některém médiu).

## Segmentace

- Probíhá, když stream dat rozdělíme do menších celků pro následný přenos. Po přijmutí všech segmentů si klient znovu
  složí celá data dohromady a pokud některý ze segmentů chybí použije ARQ(Automatic repeat request) pro znovu zaslání
  chybějících dat
    - Zvyšuje rychlost
    - Zvyšuje účinnost (Pokud jeden ze všech segmentů nedojde do cíle stačí poslat znovu jen ten jeden a nemusíme
      posílat všechno odznova)
    - Data jsou moc velká na to, aby se přenášela v celku = je potřeba použít segmentaci
    - Síť je nespolehlivá

## Zapouzdření

- Spočívá ve vložení PDU z vyšší vrstvy do PDU nižší vrstvy. Slouží to k tomu, aby vyšší vrstva mohla používat služby
  nižších vrstev.
    - Application layer -> Encoded application data
    - Transport layer -> destination and source port (process number)
    - Network layer -> Destination and source ip (logical network) address
    - Link layer -> Destination and source mac (physical) address
    - Physical layer -> timing and synchronization bits

![encapsulation-tcp.png](encapsulation-tcp.png)

## Spojová a Nespojová služba

- Nespojovaná služba (anglicky "connectionless service") je typ služby, kde každý datagram je odeslán nezávisle na
  ostatních datagramech a neexistuje mezi nimi žádná přímá spojová vazba. Tento typ služby se obvykle používá pro přenos
  krátkých a rychlých zpráv, jako jsou například dotazy DNS nebo DHCP.
    - Příkladem protokolu s nespojovanou službou je například protokol UDP (User datagram protocol), který se používá
      pro rychlý přenos dat, jako jsou například hlasová nebo video data.
- Na druhé straně spojovaná služba (anglicky "connection-oriented service") vyžaduje, aby bylo mezi komunikujícími uzly
  nejrpve navázáno spojení, které je následně použito pro přenos dat. V tomto případě jsou data odesílána jako
  posloupnost bloků s přidanou řídící informací, která umožňuje přenos dat mezi uzly a jejich správné řazení a
  zabezpečení.
    - Na druhé straně protokol TCP (Transmission control protocol) používá spojovanou službu pro spolehlivý přenos dat,
      jako jsou například emaily nebo webové stránky.

![tcp-udp-header.png](tcp-udp-header.png)

## Charakteristické vlastnosti TCP protokolu:

- Spolehlivost - TCP používá potvrzování o přijetí, opětovné posílání a překročení časového limitu. Pokud se jakákoliv
  data ztratí po cestě, sevrer si je opětovně vyžádá. U TCP nejsou žádná ztracená data, jen pokud několikrát po sobě
  vyprší časový limit, tak je celé spojení ukončeno.
- Zachování pořadí - Pokud pakety dorazí ve špatném pořadí, TCP vrstva příjemce se postará o to, aby se některá data
  pozdržela a finálně je předala správně seřazená.
- Vyšší režie - TCP protokol potřebuje např. tři pakety pro otevření spojení, umožňuje to však zaručit spolehlivost
  celého spojení.

## Charakteristika UDP:

- Jednodušší protokol založený na odesílání nezávislých zpráv.
- bez záruky - Protokol neumožňuje ověřit, jestli data došla zamýšlenému příjemci. Datagram se může po cestě ztratit.
  UDP nemá žádné potvrzování, přeposílání ani časové limity. V případě potřeby musí uvedené problémy řešit vyšší vrstva.
- Nezachovává pořadí - Při odeslání dvou zpráv jednomu příjemci nelze předvídat, v jakém pořadí budou doručeny.
- jednoduchost - nižší režie než u TCP (není zde řazení, žádné sledování spojení atd.).

## Rozsahy portů

- Well-known 0-1023 (2^10 - 1)
- registered ports 1024-49151 (2 ^ 10 to 2^14 + 2 ^ 15 - 1)
- dynamic, private or ephemeral ports - 49152 - 65535 (2^15 + 2^14 to 2^16 - 1)