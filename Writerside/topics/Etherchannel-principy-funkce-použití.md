# Etherchannel, principy, funkce, použití

## Etherchannel
Dovoluje redundantni spoje mezi zarizenimi, ktere nebude blokovat STP protocol.

Jedna se o port link agregaci vyuzivanou prevazne na switchych od znacky Cisco. Kazdy switch znacky Cisco by mel Etherchannel podporovat. Funguje na zpusobu shluknuti vice fyzickych portu do jedne logicke link. Poskytuje nam odolnost proti chybam, zvysuje prenos a samotnou rychlost prenosu, zajistuje redundanci mezi switchy, routery, servery

Nejvetsim plusem ktery ether channel poskytuje bude bandwith. Za pouziti 8 aktivnich portu coz je tedy take maximum moznych pouzitych portu muzeme dosahnout prenosu 8000Mbit/s, 8Gbit/s nebo 80Gbit/s zalezi pouze na samotnych portech.

Port channel se nazyva vysledny virtualni interface pote co ether channel nakonfigurujem.

Etherchannel spojuje traffic na vsech volnych portech v channel. Porty jsou vybrany za pomoci Cisco proprietarniho algoritmu na zaklade source or destination MAC addresses, IP addresses or TCP and UDP port numbers. Tabulka ukazuje jak je 8 rozdeleno mezi 2 az 8 porty. 2,4 a 8 portu jsou vyvazene v prenosu na kazdem z portu v channel.

| Number of Ports<br/>in the EtherChannel | Load Balancing<br/>ratio between Ports |
|-----------------------------------------|----------------------------------------|
| 8                                       | 1:1:1:1:1:1:1:1                        |
| 7                                       | 2:1:1:1:1:1:1                          |
| 6                                       | 2:2:1:1:1:1                            |
| 5                                       | 2:2:2:1:1                              |
| 4                                       | 2:2:2:2                                |
| 3                                       | 3:3:2                                  |
| 2                                       | 4:4                                    | 


Pokud jeden z porů vypaden (přestane fungovat) EtherChannel by měl automaticky předistribuovat na zbylé linky (porty). Tento process zabere méně než jednou vteřinu a je transaprentní aplikace nebo klientovy na druhé straně. Dělá to zněj velmi pružný a žádoucí protocol v kritických apliakcí kde si výpadky nemůžeme dovolit.

Nemůže shlukovat porty s rozdílnou přenosovou rychlostí jako jsou Fast Ethernet a Gigabit Ethernet v jednom Ethernetchannelu. Nastavené Ethernetchannel porty se musí ve svém nastavení shodovat na obou stranách pokud je na jedné straně trunk na druhé straně musí být také s stejnou nativní vlanou. Navíc všechny porty musí být nastavené jako Layer 2 porty.

LACP allows for up to 8 active and 8 standby links, whereas PAgP only allows for 8 active links. Stand by link se satne aktivím pokud nějaký z osmi odpadne.

Vyuzivaji se dav protokoly pro nastaveni Ethernetchannelu
- PAgP (Port Aggregation Protocol) Cisco protocol
- LACP (Link Aggregation Control Protocol) IEEE Ethernet standards

### PAgP
Pokud používá tento protokol porty se domlouvají(vyjednávají) na Etherchannelu za pomocí PAgP paketů. Pokud se porty na obou stranách domluví, vytvoří Etherchannel sekupením portů. I po vytvoření Etherchannelu PAgP pakety jsou posílány každých 30 vteřin, aby zkontrolovaly konzistenci konfigurace a vyřešil nastanete nedostatky nebo výpadky.
Dopomáhá vytvářet EtherChannel link pomocí detekce konfigurace na obou stranách, aby se ujistil, že jsou kompatibilní a že Etherchannel může vzniknout. Možnosti nastaveni:
- On: tento mód nutí interface vytvoření channelu i bez PAgP. Interface nakonfigurovaný v tomto módu nevyměňuje PAgP pakety.
- PAgP desirable: Tento mód umístí zařízení do aktivního vyjednávacího stavu ve kterém vyjednává s ostatními zařízeními posíláním PAgP paketů
- PAgP auto: Tento mód umístí zařízení do pasivního vyjednávacího stavu ve které zařízení odpovídá PAgP paketům které dostal ale sám přímo nevyjednává.
Nastavené módy musí odpovídat na obou stranách. Aby vznikl Etherchannel jak je vidět v tabulce.

| S1        | S2             | Channel Establishment |
|-----------|----------------|-----------------------|
| On        | On             | Yes                   |
| On        | Desirable/Auto | No                    |
| Desirable | Desirable      | Yes                   |
| Desirable | Auto           | Yes                   |
| Auto      | Desirable      | Yes                   |
| Auto      | Auto           | No                    |

### LACP
Tento protokol dovoluje switchům se domlouvat za pomocí LACP paketů. Funkcionalita je velmi podobná předchozímu protokolu ale protokol může běžet i na jiných než Cisco zařízeních. Cisco zařízení podporuje i tento protokol.

LACP poskytuje stejné vyjednávací výhody jako PAgP. LACP pomáhá vytvořit vytvářet Etherchannel pomocí zjištění konfigurace na obou stranách a pokud jsou kompatibilní tak je Etherchannel vytvořen.

Moznosti nastaveni:
- On: tento mod nuti interface k vytvoreni channelu i bez LACP. Pokud je interface nastaven v On modu nevymenuje LACP pakety.
- LACP active: Tento mod umisti zarizeni do aktivniho vyjednavaciho stavu ve kterem vyjednava s ostatnimi zarizenimi posilanim LACP paketu.
- LACP passive: Tento mod umisti zarizeni do pasivniho vyjednavaciho stavu ve ktere zarizeni odpovida LACP paketum ktere dostal ale sam primo nevyjednava

Nastavene mody musi odpovidat na obou stranach. Aby vznikl Etherchannel jak je videt v tabulce.

| S1      | S2             | Channel Establishment |
|---------|----------------|-----------------------|
| On      | On             | Yes                   |
| On      | Active/Passive | No                    |
| Active  | Active         | Yes                   |
| Active  | Passive        | Yes                   |
| Passive | Active         | Yes                   |
| Passive | Passive        | No                    |


## Konfigurace
- EtherChannel support- All ethernet interfaces must support EtherChannel with no requirement that interfaces be physically contiguous
- Speed and duplex - Configure all interfaces in an EtherChannel to operate at the same speed and in the same duplex mode.
- VLAN match - all interfaces in the etherChannel bundle must be assigned to the same VLAN or be configured as a trunk 
- Range of VLANs - An EtherChannel supports the same allowed range of VLANs on all the interfaces in a trunking EtherChannel. If the allowed range of VLANs is not the same, the interfaces do not form an EtherChannel, even when they are set to auto or desirable mode.

```Console
S1(config)# interface range FastEthernet 0/1 - 2
S1(config-if-range)# channel-group 1 mode active
Creating a port-channel interface Port-channel 1
S1(config-if-range)# exit
S1(config)# interface port-channel 1
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk allowed vlan 1,2,20
```

### Troubleshooting
- `show interfaces port-channel [number]`
- `show etherchannel summary`
- `show ethercahnnel port-channel`
- `show interfaces etherchannel`

### Common problems
- Assigned ports in the EtherChannel are not part of the same VLAN, or not configured as trunks. Ports with different native VLANs cannot form an EtherChannel.
- Trunking was configured on some of the ports that make up the EtherChannel, but not all of them. It is not recommended that you configure trunking mode on individual ports that make up the EtherChannel. When configuring a trunk on an EtherCHannel, verify the trunking mode on the EtherChannel.
- If the allowed range of VLANs is not the same, the ports do not form an EtherChannel even when PAgP is set to the auto or desirable mode.
- The dynamic negotiation options for PAgP and LACP are not compatibly configured on both ends of the EtherChannel.




