# DNS, funkce, hierarchie DNS (od souboru po globální DNS servery), konfigurace

## DNS (TPC/53, UDP/53) RFC1035
Domain name system je hierarrchycký, decentralizovaný systém doménových jmen, který je realizován servery DNS a protokolem stejného jména, kterým si vyměnují informace. Jeho hlavním úkolem a přčinou vzniku jsou vzájmené převody doménových jmen a IP adres uzlů sítě. Později ale přibral další funkce (např. pro elektronickou poštu či IP telefonii) a slouží dnes de facto jako distribuovaná databáze síťových informací.

Jména domén umožňuje lepší orientaci lide, adresy pro stroje jsou však vyjádřeny pomocí 32bitových(IPv4) A nebo 128 bitových (IPv6) AAAA záznamů. Systém DNS umožňuje efetkivně udržovat decentrilozované databáze doménových jmen a jejich překlad na IP adresy. Stejně tak zajištťuje zpětný překla IP adresy na doménové jméno = PTR záznam.

## DNS Server
- Autorirativní server: je ten, na němž jsou trvale uloženy záznamy k dané doméně/zóně. Autorirativních serverů je obcykle více (minimálně dva - primární a sekundární, ale běžně i více) a až na velmi specialni pripady se na vsech udrzuji totozne zaznamy, tzn. kazdou zmenu v zaznamech je potreba propagovat na vsechny autoritrativni servery. Autorirativni DNS server y jsou obvykle provozovany registratorem domeny nebo poskytovatelem webhostingu.
- Rekurzivni (caching only) server je server, na ktery se se svymi dotazy obraceji klientska zarizeni (pocitac, mobil etc.). Server pro ne prislusny zaznam ziska rekurzivnimi dotazy u autoritativnich DNS serveru a po stanovenou dobu (definovanou pomoci parametru TTL(Time to live)) je ma ulozeny v cache, aby mohl odpovidat klientu rychleji a setril zatizeni serveru autoritativnich. Na tomto serveru nejsou zadne zony ulozeny trvale. Rekurzivni DNS server se take stara o validaci DNSSEC, pokud tuto technologii podporuje. Rekurzivnich serveru muze byt na klientu definovano vice na ruznych IP adresach, ale v praxi se spise yajistuje vzsoka dostupnost serveru na prvni definovane IP adrese. Informaci o DNS serverech na dane siti klient zjistuje necjasteji pres protokol DHCP, na IPv6 pres NDP
- Root server korenove servery predstavuji zasadni cast technicke infrastruktury internetu, na ktere zavisi spolehlisvost, spravnost a bezpecnost operaci na internetu. Tyto servery poskituji korenovy zonovy soubor (root zone file) ostatnim DNS serverum. Jsou soucasti DNS, celosvetove distibuovane databaze ktera slouzi k prekladu unikatnich domenovych jmen na ostatni identifikatory
  - Korenovy zonovy soubor popisuje, kde se nachazeji autoritativni servery pro domeny nejvyssi urovne. Tento korenovy zonovy soubor je relativne velmi maly a casto se nemeni - operatori root serveru ho pouze zpristupnuji, samotny soubor je vytvaren a menem organizaci IANA.

![domain-explained.png](domain-explained.png)

### Zpusob ziskavani IP adresy
1. Uzivatel zadal do sveho WWW klienta domenove jmeno www.wikipedia.org. Resolver v pocitaci se obratil na lokalni DNS server s dotazem na IP adresu pro www.wikipedia.org.
2. Lokalni DNS server tuto informaci nezna. Ma vsak k dispozici adresy korenovych serveru. Na jeden z nich se obrati (rekneme na 193.0.14.129) a dotaz mu preposle.
3. Korenovy server take nezna odpoved. Vi vsak, ze existuje domena nejvyssi urovne org a jake jsou jeji autoritativni servery, jejich adresy tazateli poskytne.
4. Lokalni server jeden z nich vybere (rekneme, ze zvoli tld1.ultradns.net s IP adresou 204.74.112.1) a posle mu dotaz na IP adresu ke jmenu www.wikipedia.org.
5. Osloveny server informaci opet nezna, ale poskytne IP adresy autoritativnich serveru pro domenu wikipedia.org. Jsou to ns0.wikimedia.org(207.142.131.207), ns1.wikimedia.org(211.115.107.190) a ns2.wikimedia.org(145.97.39.158).
6. Lokalni server opet jeden z nich vybere a posle mu dotaz na IP adresu ke jmenu www.wikipedia.org.
7. Jelikoz toto jmeno se jiz nachazi v domene wikipedia.org, dostane od jejiho serveru nepochybne autoritativni odpovedm ze hledana IP adresa zni 145.97.39.155.
8. Lokalni DNS server tuto odpoved preda uzivatelskemu pocitaci, ktery se na ni ptal.

![getting-address-from-dns.png](getting-address-from-dns.png)

### Reverzni dotaz
Tento nesoulad resi DNS tak, ze pri reverznich dotazech obraci poradi bajtu v adrese. K obracene adrese pak pripoji domenu in-addr.arpa a vysledne "jmeno" pak vyhledava standartnim postupem. Hleda-li napriklad jmeno k IP adrese 145.97.39.155, vytvori dotaz  na 155.39.97.145.in-addr.arpa. Obraceni IP adresy umoznuje delegovat spravu reverznich domen odpovidajicich sitim a podsitim spravcum dotycnych siti a podsiti. V prikladu pouzitou sit 145.90.0.0/16 spravuje nizozemsky SURFnet a ten ma take ve sprace ji odpovidajici domenu 97.145.in-addr.arpa. Kdykoli zavede do site novy pocitac, muze zaroven upravit data v reverzni domene, aby odpovidala skutecne situaci.

### Zaznamy
- A (address record) obsahuje IPv4 adresu prirazenou danemu jmenu, napriklad kdyz jmenu cosi.kdesi.cz nalezi IP adresa 1.2.3.4, bude zonovy soubor pro domenu kdesi.cz obsahovat zaznam: `cosi IN A 1.2.3.4`
- AAAA (IPv6 address record) obsahuje IPv6 adresu. Zminenemu stroji bychom dali IPv6 addresu 2001:718::1 priradili zaznamem: `cosi IN AAAA 2001:718::1`
- CNAME (canonical name record) je alias - jine jmeno pro jiz zavedene. Typicky se pouziva pro servery znamych sluzeb, jako je napriklad WWW. Jeho definice pomoci prezdivky umoznuje jej pozdeji snadno prestehovat na jiny pocitac. Pokud nas cosi.kdesi.cz ma slouzit zaroven jako www.kdesi.cz vlozime do zonoveho souboru: `www IN CNAME cosi`
- MX (mail exchange record) oznamuje adresu a prioritu serveru pro prijem elektronicke posty pro danou domenu. Tentokrat jsou parametry dva- priorita (prirozene cislo, mensi znamena vyssi prioritu) a domenove jmeno serveru. Pokud postu pro pocitaci cosi.kdesi.cz prijima nejlepe pocitac mail.kdesi.cz a pripadne jako zalozni i mail.jinde.cz, bude zonovy soubor obsahovat zaznamy (vsimnete si pouziti jmen s teckou a bez tecky): `cosi IN MX 10 mail` a `IN MX 20 mail.jinde.cz`
- NS (name server record) ohlasuje jmeno autoritativniho DNS serveru pro danou domenu. Bude-li mit domena kdesi.cz poddomenu obchod.kdesi.cz, jejimz servery budou ns.kdesi.cz (primarni) a ns.jinde.cz (sekundarni), bude zonovy soubor pro kdesi.cz obsahovat: `obchod IN NS ns` a `IN NS ns.jinde.cz`
- PTR (pointer record) je specialni typ zaznamu pro reverzni zony. Obsahuje na prave strane jmeno pocitace pridelene adrese na strane leve (adresa je transformovana na domanu vyse popsanym postupem). Drzme se naseho prikladu pro zaznam typu A - v souladu s nim by zonovy soubor pro domenu 3.2.1.in-addr.arpa mel obsahovat (zonovy soubor definuje reverzni domenu, proto je treba psat na prave strane kompletni jmeno s teckou, jinak by za ne pripojil reverzni domenu): `4 IN PTR cosi.kdesi.cz`
- SOA record: SOA stand for "start of authority" It's an important DNS record type that stores admin information about a domain. This information includes the email address of the admin and when the domain was last updated.
- TXT record: TXT stands for "text", and this record type lets the owner ofa domain store text values in the DNS. Several servuces use this record to verify ownership of a domain.
- PTR record: A pointer (PTR) record provides a domain name for reverse lookup. It's the opposite of an A record as it provides the domain name linked to an IP address instead of the IP address for a domain.
- SRV record: Using this DNS record type, it's possible to store the IP address and port for specific  services.
- CERT record: This record type stores public keys certificates.
- DCHID: This DNS record type stores information related to dynamic host configuration protocol (DHCP)
- DNAME: The full meaning of DNAME is "delegation name". This record type works very similarly to CNAME; however, it points all the subdomains for the alias to the canonical domain name. That is, pointing the DNAME for secondsite.com to example.com will also applu to staff.secondsite.com and any other subdomain.

Servery DNS jsou organizovany hierarchicky, stejne jako jsou hierarchicky tvoreny nazvy domen.

### DNS on computer file
- /etc/hosts ... on linux dns local file (ip domain)
- /etc/resolve/conf ... definuje se adresa dns a domena
- Hosts windows on dns local file
Nejdrive zadny DNS server neexistoval, jen se udrzoval centralne jako jeden soubor ktery si uzivatele davali do /etc/hosts ale to se v jednu chvili stalo neudrzitelne a proto bylo potreba vymyslet nejakou alternativu. Tedy DNS decentralizovany system vznikl.

### DNS server konfigurace
`sudo apt install dnsmasq`
`sudo nano /etc/dnsmasq.conf`
```
# Never forward plain names (without a domain)
domain-needed
# Turn off DHCP on eth0
no-dhcp-interface=eth0
# Never forward addresses in the non-routable address space (RFC1918)
bogus-priv
# Add domain to host names
expand-hosts
# Domain to be added if expand-hosts is set
domain=zola.home
# Local domain to be served from /etc/hosts file
local=/zola.home/
# Don't read /etc/resolv.conf (I deleted it). Get the external name server from this file, see 'server' below
no-resolv
# External server, works with no-resolv
server=8.8.8.8
```

