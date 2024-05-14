# HSRP, principy, funkce, použití, konfigurace

## HSRP (Hot Standby Router Protocol) RFC 2281
Jedna se o Cisco proprietarni redundantni protokol pro zalozani a fault-tolerance default gateway. Verze 1 vznikla jiz v roce 1998 a byla popsana v RFC 2281. Verze 2 protokolu obsahuje nejaka vylepseni a podporu IPv6, ovsem neexistuje pro ni korespondujici RFC notace.
- Verze 2 krom toho ze podporuje IPv6 adresy navic prinasi, stabilitu, skalovatelnost a vylepsenou diagnostiku. Neni kompatibilni s 1 verzi HSRP. Zvysuje pocet HSRP groups z 256 na 4096.

Protokol zalozi spojeni mezi routerama. V pripade ze jedna z default gateway prestane fungovat nahradi jeji funkcionalitu druha. HSRP gateway posila multicast hello message ostatnim gateways aby jim oznamila jejich prioritu (ktera gateway je preferovana) a aktualnim stavu (active nebo standby).

### Princip
Primarni router s nejvysi nastavenou prioritou se bude chovat jako virtualni router s preddefinovanou gateway IP adresou a bude odpovidat ARP a ND requestum od stroju pripojenych k LAN s vyuzitim sve virtualni MAC adresou (primarni gatewaye). Pokud primarni router by mel prestat odpovidat, router s druhou nejvetsi prioritou nez ma primarni router prevezme na sebe funkcionalitu defaultni gateway a sam se stane primarnim routrem. Na ARP a ND requesty bude stale odpovidat s vyuzitim stejne virtualni MAC adresy.

| HSRP version | IP protocol | Group address           | UDP port | Virtual MAC address range |
|--------------|-------------|-------------------------|----------|---------------------------|
| 1            | IPv4        | 224.0.0.2 (all routers) | 1985     | 00:00:0c:07:ac:XX         |
| 2            | IPv4        | 224.0.0.102(HSRP)       | 1985     | 00:00:0c:9f:fX:XX         |
| 2            | IPv6        | ff02::66                | 2029     | 00:05:73:a0:0X:XX         |

Pismeno "X" ve virtualni MAC adrese reprezentuje group ID v hexu. HSRP neni routing protocol protoze zadnym zpusobem nijak nemeni nebo jinak neovlivnuje ip routing table.

HSRP je schopne vyvolat failover pokud jedno nebo vice zarizeni na routeru prestane fungovat.

### Common HSRP problems
- HSRP routers not being on the same network segment
- HSRP routers not configured with IP addresses from the same subnet
- HSRP configuration issues like standby groups and virtual IPs not matching on the HSRP routers.
### HSRP Communication
- Hello: The hello message is sent between the active and standby devices (by default, every 3 seconds). If the standby device does not hear from the active device (via a hello message) in about 10 seconds, it will take over the active role.
- Resign: The resign message is sent by the active HSRP device when it is getting ready to go offline or relinquish the active role for some other reason. This message tells the standby router to be ready and take over the active role.
- Coup: The coup message is used when a standby router wants to assume the active role (preemption).
### HSRP states
- Active: This is the state of the device that is actively forwarding traffic.
- Init or Disabled: This is the state of a device that is not yet ready or able to participate in HSRP.
- Learn: This is the state of a device that has not yet determined the virtual IP address and has not yet  seen a hello message from an active device.
- Listen: This is the state of a device that is receiving hello messages.
- Speak: This is the state of a device that is sending and receiving hello messages.
- Standby: This is the state of a device that is prepared to take over the traffic forwarding duties from the active device.

### Konfigurace
Defaultni priorita HSRP router je 100. Kdo ma vyssi prioritu stane se aktivnim routerem.

| Step number | Description                                                                                                                                                                                                                                                                                                                                                                     | Command                                                                                                             |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| 1           | Enter privileged EXEC mode.                                                                                                                                                                                                                                                                                                                                                     | router>enable                                                                                                       |
| 2           | Enter global configuration mode                                                                                                                                                                                                                                                                                                                                                 | router#configure terminal                                                                                           |
| 3           | Enter interface configuration mode.                                                                                                                                                                                                                                                                                                                                             | router(config)#interface interface                                                                                  |
| 4           | Configure an IP address on the interface.                                                                                                                                                                                                                                                                                                                                       | router(config-if)#ip address address netmask                                                                        |
| 5           | Configure an HSRP virtual IP address.<br/>Note:If the group-numbers is not entered then it will default to a group number of 0.<br/>The ip-address parameter is not required but does need to be entered on at least one HSRP device. The other devices are able to learn the virtual IP address from this device.                                                              | router(config-if)#standy [group-number] ip [ip-address]                                                             |
| 6           | Configure the HSRP priority (optional)<br/>Note: If the group-number is not entered then it will default to a group number of 0.<br/>The valid values for the priority are from 0 trough 255.                                                                                                                                                                                   | router(config-if)#standby [group-number] priority priority                                                          |
| 7           | Configure HSRP preemption (optional).<br/>Preempt forces a router to be active after recovering from a failure.                                                                                                                                                                                                                                                                 | router(config-if)#standby [group-number] preempt                                                                    |
| 8           | Associated a tracked object to the HSRP group (optional).<br/>Note: If the group-number is not entered, then it will default to a group number of 0.<br/>By default, the decrement-value is 10; what this means is that the HSRP priority will go down by 10 if the object is not 'up'.<br/>The shutdown parameter will disable the HSRP group if the tracked object goes down. | router(config-if)#standby [group-number] track [object-number] object-number [decrement decrement-value] [shutdown] |
| 9           | Create a tracked object (optional).<br/>Note: The object-number can be any number between 1 and 1000. <br/> The line-protocol parameter will track the protocol state of the configured interface.<br/>The ip routing parameter will track the IP routing capability of an interface (is it configured with an IP address and operational).                                     | router(config)#track object-number interface interface {line-protocol or ip routing}                                |

[Config guide](https://community.cisco.com/t5/networking-knowledge-base/hsrp-overview-and-basic-configuration/ta-p/3131590)


### Advanced HSRP configuration - Load Balancing
![advanced-hsrp.png](advanced-hsrp.png)