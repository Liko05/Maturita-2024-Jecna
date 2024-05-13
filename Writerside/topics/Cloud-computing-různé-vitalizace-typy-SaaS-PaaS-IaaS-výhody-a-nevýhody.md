# Cloud computing - různé vitalizace typy (SaaS, PaaS, IaaS), výhody a nevýhody

## Cloud computing

je na internetu založený model vývoje a používání počítačových technologií. Lze ho také charakterizovat jako poskytování
služeb či programů servery dostupnými z internetu s tím, že uživatelé k nim mohou přistupovat vzdáleně, kupř. pomocí
webového prohlížeče nebo klienta elektronické pošty. Za předpokladu, že služba je placená, uživatelé neplatí za vlastní
software, ale za jeho užití na měsíční či roční bázi, nebo zaplatí jednorázový poplatek.
Principem u služeb a produktů v cloud computingu je to, že uživateli propůjčují výpočetní výkon serverů. V mnoha
případech se tak děje formou specializovaných aplikací, jejichž nabídka se pohybuje od kancelářských aplikací přes
systémy pro distribuované výpočty až po operační systémy provozované v prohlížečích

### Technologie cloud computingu se vyznacuje nasledujicimi atributy:

- Multitenancy: tento pojem lze volne prelozit jako "vice najmu". Jedna se o to, ze pocitacove zdroje jsou sdilene mezi
  vsemi uzivateli.
- Obrovska skalovatelnost a elasticita: umozni uzivatelum dle potreby operativne zmeni vypocetni zdroje.
- Pay as you go: cenovy tarif zalozeny na principu "Kolik toho uzivatel spotrebuje, tolik zaplati"
- Aktualnost (up-to-date): poskytovatel garantuje ze vsechen software je vzdy aktualizovany; uzivatel nemusi do tohoto
  procesu nijak zasahovat
- Pristup pres internet: uzivatele se mohou ke svemu softwaru pripojit z jakekoli casti sveta.

### V zasade existuje dvoji deleni cloud computingu:

- kriterium toho, jak jsou sluzby cloudu poskytovany
- charakter sluzby kterou cloud poskytuje.

### Typy cloudu

#### Verejny cloud

Veřejný cloud je nejčastějším servisním modelem cloudových služeb a je zároveň modelem, který umožňuje nejjednodušší
škálování výpočetního výkonu a dalších zdrojů pro potřebu zákazníka. Jedná se o službu dodavatele cloudových služeb, kdy
tento dodavatel vybuduje jedno nebo více datových center, která spadají pod jeho plnou správu a v nich provozuje
cloudové služby (v různých modelech – od infrastruktury až po hotové aplikace) přístupné zákazníkům přes internet.
Dostupnost služeb zákazníkům je pak určena pomocí SLA. Tyto služby jsou zákazníkům dodávány zadarmo či za poplatek
nejčastěji spjatý s objemem využitých služeb – PAYG. Jelikož v jednom prostředí nad jedním hardwarem mohou běžet služby
a prostředky více zákazníků, bavíme se o takzvané multitenant architektuře.
Jeden tenant si můžeme představit jako prostředí jednoho zákazníka – například všichni uživatelé řešení cloudového
úložiště dat a jejich data a nastavení v rámci jedné firmy. Data těchto uživatelů mohou být poté uložena na stejném
hardwaru jako data jiných zákazníků, nicméně jednotliví zákazníci si do dat svých uživatelů navzájem nevidí – právě díky
multitenant architektuře. Ta přináší výhody snížení nákladů na službu, ale také jednoduchou škálovatelnost.
Ekonomické principy cloudu vycházejí z předpokladu, že ve veřejném cloudu může zákazník získat nejlevnější výkon.[8]
Toto je zapříčiněno tím, že velkoodběratel hardwaru a služeb dokáže stlačit cenu níže než každý jednotlivý uživatel
zvlášť. Díky tomu může poskytovat služby za nižší cenu, než které by jednotliví zákazníci mohli dosáhnout sami.

#### Privatni cloud

Oproti veřejnému cloudu se privátní cloud liší tím, že jsou veškeré prostředky tohoto nasazení dedikovány a používány
pouze jedním uživatelem/zákazníkem – nad prostředky tedy běží jediný tenant. Hardware i software běží na dedikované
privátní síti a zároveň na hardwaru nikdy neběží služby pro jiného zákazníka. Služby privátního cloudu poskytuje buď
přímo poskytoval cloudových služeb ze svého hardwaru (za dodržení podmínek výše o plném dedikování tohoto hardwaru
jedinému zákazníkovi), nebo přímo na serverech/v datacentru zákazníka.
Důvodem nasazení privátního cloudu je často důraz na bezpečnost nebo regulatorní omezení u zákazníka – setkáváme se tak
s ním především u finančních a státních institucí. Mezi výhody, které získává uživatel privátního cloudu, patří právě
bezpečnost a kontrola nad daty a zároveň jednoduchá škálovatelnost a řízení prostředků. Nevýhodou oproti veřejnému
cloudu je pak ztráta flexibility zdánlivě neomezeného množství výpočetního výkonu a případné další náklady na agendu
spojenou se správou vlastního hardwaru, rovněž je privátní cloud často spojen s vyššími počátečními náklady.

#### Hybridni cloud

Hybridní cloud je řešení, které spojuje výhody veřejného a privátního cloudu, případně spojení veřejného cloudu s jinou
místní infrastrukturou. K takovémuto nasazení obvykle přistupujeme, pokud chceme zachovat kontrolu nad kritickými nebo
citlivými daty a prací nad nimi – takováto data zůstávají na privátním cloudu nebo místních databázích a veřejný cloud
slouží k operacím s menším důrazem na bezpečnost – nebo například pro běh legacy aplikací; při přechodu na cloud z
místní infrastruktury (tzv. on-premise) – jedná se o stav postupné migrace do veřejného cloudu; nebo veřejný cloud
využíváme jako zdroj dodatečné výpočetní síly – běžné operace běží na místní infrastruktuře a při nadstandardním
vytížení jsou dynamicky vytvořeny další výpočetní zdroje ve veřejném cloudu. V hybridním nasazení se tedy schází výhoda
silné kontroly a bezpečnosti, ale i flexibility.

#### Multicloud

Multicloudové řešení je řešení, které využívá služeb více dodavatelů veřejného cloudu (případně může být kombinováno s
hybridním scénářem). Toto uživatelům a zákazníkům přináší výhody jako minimalizace rizik, využívání možností více
cloudových vendorů, snížení závislosti na konkrétním dodavateli nebo vytvoření tlaku na nižší cenu (díky kompetitivnímu
prostředí)[11]. Mezi nevýhody naopak patří potřeba udržování širších znalostí cloudu jednotlivých dodavatelů, bezpečné a
jednotné řízení přístupů a integrace řešení (ačkoliv cloudoví dodavatelé již pracují na jednoduchém provázání a umožnění
multicloudové strategie).

#### Komunitni cloud

Jedná se o model, kdy je infrastruktura cloudu sdílena mezi několika organizacemi, tedy skupinou lidí, kteří ji
využívají. Tyto organizace může spojovat bezpečnostní politika, stejný obor zájmu apod.¨

### Distribucni model

Distribuční model vypovídá o tom, co je v rámci služby nabízeno – zda jde o software, hardware či jejich kombinaci.

- IaaS: infrastruktura jako služba (Infrastructure as a Service) – poskytovatel služeb se zavazuje poskytnout
  infrastrukturu. Typicky se jedná o virtualizaci. Hlavní výhodou tohoto přístupu je, že o veškeré problémy s hardwarem
  se stará poskytovatel. Na druhou stranu, vzhledem k tomu, že hardware se bere jako něco, co vlastníme, na co můžeme
  sáhnout a jsme za to zodpovědní, je někdy nemožné toto akceptovat. IaaS je vhodné pro ty, kteří vlastní software (či
  jejich licence) a nechtějí se starat o hardware. Příklady IaaS jsou Amazon WS, Rackspace nebo Windows Azure. Zkratka
  IaaS může znamenat též integrace jako služba(Integration as a Service).
- PaaS: platforma jako služba (Platform as a Service) – poskytovatel garantuje kompletní prostředky pro podporu celého
  životního cyklu tvorby a poskytování webových aplikací a služeb; to plně na internetu, bez možnosti stažení softwaru.
  Koncepce zahrnuje různé prostředky pro vývoj aplikací, jako jsou IDE nebo API, ale rovněž např. pro údržbu. Nevýhodou
  tohoto přístupu je proprietární uzamčení, kdy různí poskytovatelé mohou používat např. různé programovací jazyky.
  Příklady poskytovatelů PaaS jsou Google App Engine nebo Force.com(Salesforce.com).
- SaaS: software jako služba (Software as a Service) – aplikace je licencována jako služba pronajímaná uživateli.
  Uživatelé si tedy kupují přístup k aplikaci, ne aplikaci samotnou. SaaS je ideální pro ty, kteří potřebují jen běžný
  aplikační software a požadují přístup odkudkoliv a kdykoliv. Příkladem může být sada aplikací Google Apps nebo v
  logistice známý systém Cargopass.

### Vyhody vyuzivani cloudu

- Absence nutnosti nakupu nakladneho HW a znalosti principu funkcnosti SW a HW
- Efektivni rizeni a prace diky dostupnosti dat odkudkoli - rust produktivity prace ve firmach.
- Jednoduchost uzivatelskeho rozhrani
- Principalne vyssi zabezpeceni dat, oproti vetsine On-Premise reseni
- Moznost okamziteho zvyseni vykonu datoveho centra
- Rychle prizbusobeni IT zazemi, rustu a potrebam uzivatele
- Snizeni ceny na porizovani IT infrastruktury.
- Minimalizace provoznich nakladu.

### Nevyhody vyuzivani cloudu

- zavislost na internetovem pripojeni.
- Závislost na poskytovateli – společnosti využívající cloud ztrácí možnost rozhodovat, kterou verzi používat (platí pro
  víceverzovaný SW). Čím větší společností je poskytovatel, tím hůře se s ním komunikuje a vyjednávají podmínky.
- Obavy z cloud computingu – cloud je sice již řadu let standardní řešení, ale stále přetrvává nerelevantní obava z
  uložení dat mimo své prostředí, přestože běžně používáme sociální sítě či přistupujeme na bankovní účet online. Je
  tedy potřeba se zajímat o zabezpečení dat u daného dodavatele a všeobecné podmínky poskytování služby samotné.
- Odlišný právní řád poskytovatele a klienta – poskytovatel cloud computingu může být podřízen jiné jurisdikci než jeho
  klient. Např. společnosti sídlící v USA nebo poskytující službu z USA jsou povinny postoupit data klienta vládě v
  souladu s PATRIOT Actem, což může kolidovat kupř. s povinností ochrany osobních údajů uloženou poskytovateli zákonem.
  Zajímejte se, kde jsou vaše data uložena, mimo EU je to již risk.





