# Statické i dynamické směrování na síti. (RIP, OSPF), konfigurace

## Statické směrování
- Při statickém (též neadaptivním) směrování nejsou za běhu stanice záznamy ve směrovací tabulce nijak aktivně měněny. Může je do ní zapsat správce počítače (typicky podle údajů poskytnutých správcem příslušné počítačové sítě) nebo jsou do tabulky zapsány při startu počítače. Záznamy mohou být uchovány v konfiguračním souboru (v Microsoft Windows pak v registrech) nebo poskytovány například pomocí protokolu DHCP.
- Statické směrování používají typicky koncové stanice nebo routery v malých počítačových sítích (LAN), protože záznamy není nutné v průběhu činnosti zařízení měnit a nebo proto, že jsou záznamy jednoduché.

![simple-route-example.png](simple-route-example.png)

### IPv4 konfigurace
```Console
 Router(config)#ip route 192.198.1.0 255.255.255.0 10.1.1.2
```

### IPv6 konfigurace
```Console
    Router(config)#ipv6 unicast-routing
    Router(config)#ipv6 route 2001::/126 200::2
```

> **Notes:**
> - ip route síť maska_sítě ip_kudy

{style="note"}


## Dynamické směrování
- Dynamické směrování (adaptivní) s průběžně reaguje na změny v počítačové síti (přidávání nebo odebírání podsítí) a přizpůsobuje jim obsah směrovací tabulky. Podle způsobu, jakým si jednotlivá zařízení vyměnují informace o změnách v počítačové síti, lze dynamické směrování rozdělit do několika základních skupin (které se vzájemně prolínají a kombinují). Pro distribuci těchto informací mezi směrovači se používají různé směrovací protokoly.

## RIP (Routing Information Protocol)
- je v informatice směrovací protokol umožňující směrovačům (routerům) komunikovat mezi sebou a reagovat na změny topologie počítačové sítě. Ačkoliv tento protokol patří mezi nejstarší doposud používané směrovací protokoly v sítích IP, má stále své uplatnění v menších sítích a to především pro svoji nenáročnou konfiguraci a jednoduchost. Poprvé  byl definován v RFC 1058 (1988).
- je směrovací protokol typu distance-vector (vektor vzdálenosti) využívající Bellmanův-Fordův algoritmus pro určení nejkratší cesty v síti. Metrikou směrování je počet skoků k cílové síti (hop count). Jako ochrana proti směrovacím smyčkám je implementovaný omezený počet směrovačů (hopů) v cestě k cíli, maximální možný počet hopů je 15. Tento limit ovšem také omezuje veůolpst sítí ve kterých lze RIP použít (16 hopů je bráno jako nekonečná vzdálenost a používá se k označení nepřístupných, nepoužitelných tras).
- Původně každý router s RIP vysílal aktualizované směrovací tabulky v intervalu 30 sekund. To z počátku nepředstavovalo žádný problém, jelikož směrovací tabulky nebyly tak rozsáhlé, aby se to nějak výrazněji projevilo na síťovém provozu. Vzhledem k růstu sítí (a tudíž i směrovacích tabulek) se ale toto řešení ukázalo jako nevhodné, jelikož každých 30 sekund by byla síť zahlcena velkým množstvím dat. Moderní implementace RIP toto řeší pomocí různých metod nastavujících časové intervaly každého routeru zvlášť, aby byla data rozprostřena v čase, a nedocházelo nárazově k velikým tokům dat.

![RIP-SCHEMA.PNG](RIP-SCHEMA.PNG)

### RIP Routes for Router0:
```Console
Router0(config)# router rip
Router0(config-router)# network 192.168.10.0
Router0(config-router)# network 10.0.0.0
```

### RIP Routes for Router1:
```Console
Router1(config)# router rip
Router1(config-router)# network 192.168.20.0
Router1(config-router)# network 10.0.0.0
Router1(config-router)# network 11.0.0.0
```

### RIP Routes for Router2:
```Console
Router2(config)# router rip
Router2(config-router)# network 192.168.30.0
Router2(config-router)# network 11.0.0.0
```

## OSPF (Open Shortest Path First)
- Je hierarchický interní směrovací protkol, fungující na bázi link-state, tzn. každý směrovač zná strukturu celé sítě (v případě OSPF přesněji celé oblasti). OSPF je nejpoužívanějším směrovacím protokolem pro směrování uvnitř autonomních systémů. Část sítě, v níž působí OSPF, se nazývá OSPF doména.
- OSPF je tzv. beztřídní (classless) směrovací protokol, pracuje v sítích s různě dlouhými maskami podsítě(Variable-Length Subnet Mask, VLSM). Nepodporuje automatickou sumarizaci (Sumarizaci na hranicích třídních sítí, tuto sumarizaci je v případě potřeby nutno konfigurovat manuálním zásahem). V případě IPv4 se OSPF zprávy vkládají přímo do IP packetu, přičemž hodnota v poli "Protocol" IP záhlaví je 89. U směrovačů firmy Cisco je administrativní vzdálenost protokolu OSPF implicitně 110.
- Činnost OSPF je rozdělena do 3 částí:
  - Správa sousedských relací
  - Šíření směrovacích informací
  - Určování nejkratších (optimálních) cest.

### Configuring Single Area OSPF

![Single-area-ospf.png](Single-area-ospf.png)

#### Router 1
```Console
R1(config-router)#router ospf 1
R1(config-router)#network 10.0.1.0 0.0.0.255 area 0
R1(config-router)#network 172.16.0.0 0.0.255.255 area 0
```

#### Router 2
```Console
R2(config-router)#router ospf 1
R2(config-router)#network 192.168.0.0 0.0.0.255 area 0
R2(config-router)#network 172.16.0.0 0.0.255.255 area 0
```
### Configuring Multiarea OSPF

![ospf-multiare.png](ospf-multiare.png)

#### Router 1 {id="router-1-multiarea"}
```Console
R1(config-router)#router ospf 1
R1(config-router)#network 10.0.1.0 0.0.0.255 area 0
R1(config-router)#network 172.16.0.0 0.0.255.255 area 0
R1(config-router)#router-id 1.1.1.1
```

#### Router 3
```Console
R1(config-router)#router ospf 1
R1(config-router)#network 192.168.0.0 0.0.0.255 area 1
R1(config-router)#network 90.10.0.0 0.0.0.255 area 1
R1(config-router)#router-id 3.3.3.3
```

#### Router 2 {id="router-2-multiarea"}
```Console
R1(config-router)#router ospf 1
R1(config-router)#network 172.16.0.0 0.0.0.255 area 0
R1(config-router)#network 192.168.0.0 0.0.0.255 area 1
R1(config-router)#router-id 2.2.2.2
```




