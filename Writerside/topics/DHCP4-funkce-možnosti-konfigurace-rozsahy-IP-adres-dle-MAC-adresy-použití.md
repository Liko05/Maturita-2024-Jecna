# DHCP4 - funkce, možnosti konfigurace (rozsahy IP adres, dle MAC adresy), použití

## DHCPv4
Dynamic Host Configuration Protocol v4 (DHCPv4) přiřazuje IP adresu, subnet mask, default gateway, DNS záznam. Jedná se o jednodužší konfiguraci pro administrátory sítí. Menší sítě nepotřebují ani specialozavný server protože častokrát tuto funkci může zastoupit router.

DHCP drží pool adres které rozděluje mezi klienty na určitou časovou dobu dokud ji klient bude potřebovat poté až si její trvanlivost klient neprodlouží bude adresa znovu k dispozici.

### Proces získání ip adresy:
- DHCP Discover (DHCPDISCOVER): Klient začne broadcastovat DHCPDISCOVER zprávu za použití (255.255.255.255) broadcast nebo specifického subnetu broadcastu. Za použití vlastní MAC adresy z důvodu nalezení DHCP serveru.
- DHCP Offer (DHCPOFFER): Po obdržení DHCPDISCOVER DHCPv4 server rezervuje jednu z volných IP adres aby ji mohl vypůjčit klientovy. Server si také vytvoří ARP záznam skládající se z MAC adresy z DHCPDISCOVER message a vypujčené IPv4 adresy. Následně posílá zpátky klientovy DHCOFFER která obsahuje MAC adresu klienta (client id) (který žádal o IPv4 adresu), IPv4 adresu kterou mu zarezervoval, subnet mask, dobu vypůjčení a IP adresu DHCPv4 serveru který posílá DHCPOFFER.
- DHCP Request (DHCPREQUEST): Využívá se jak pro lease origination a leas renewal. Lease orgination slouží origination slouží jako oznámení o přijetí informací a parametru které server nabízí a jasně odmítá jakékoliv jiné servery které by se snažily klientovy poskytnout své údaje.
- DHCP Acknowledgment (DHCPACK): Po obdržení DHCPREQUEST se ještě může server ujistit a poslat ICMP ping message aby zjistil jestli danou ip adresu ještě nepoužívá někdo jiný, (vytvoření nový ARP záznam pro klienta) a posílá klientovy DHCPACK. Je totožná s DHCPOFFER až na změnu v message type field. Když klient obdrží DHCPACK message uloží si konfigurační údaje a pošle následně ARP message aby se ujistil že nikdo neexistuje se stejnou IP adresou. Pokud nedostane odpověď ví že je jediný s touto IP adresou v  síti a začne jí používat jako svojí.
### Obnovení adresy
- DHCP Request (DHCPREQUEST): Předtím než dojde platnost vypůjčení adresy clien posílá DHCPREQUEST pro lease renewal přímo na DHCPv4 server, pokud klient nedostane DHCPACK není obdržena po oběhnutí nějakého specifického času klient začne broadcastovat DHCPREQUEST, aby nějaký jiný DHCPv4 server prodloužil jeho zapůjčení.
- DHCP Acknowledgement (DHCPACK): Server potvrdí lease informace posláním DHCPACK message.
### Konfigurace
1. Exclude IPv4 addresses.
    - `Router(config)# ip dhcp excluded-address low-address [high-address]`
2. Define a DHCPv4 pool name.
   - `Router(config)# ip dhcp pool pool-name`
3. Configure the DHCPv4 pool.

| Task                                   | IOS command                                                   |
|----------------------------------------|---------------------------------------------------------------|
| Define the address pool .              | <code>network network-number [mask or /prefix-length] </code> |
| Define the default router or gateway.  | default-router address [address2...address8]                  |
| Define a DNS server.                   | dns-server address [address2...address8]                      |
| Define the domain name.                | domain-name domain                                            |
| Define the duration of the DHCP lease. | lease {days [hours [minutes]] or infinite}                    |
| Define the NetBIOS WINS server         | netbios-name-server address [addres2...address8]              |

example:
```Console
R1(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.9 
R1(config)# ip dhcp excluded-address 192.168.10.254 
R1(config)# ip dhcp pool LAN-POOL-1 
R1(dhcp-config)# network 192.168.10.0 255.255.255.0 
R1(dhcp-config)# default-router 192.168.10.1 
R1(dhcp-config)# dns-server 192.168.11.5 
R1(dhcp-config)# domain-name example.com 
R1(dhcp-config)# end 
```

### Podle mac adresy
`address <ip-address> hardware-address <mac-address>`
```Console
R1(config)# ip dhcp pool Test-Pool
R1(dhcp-config)# network 192.168.17.0/24
R1(dhcp-config)# address 192.168.17.137 hardware-address 0100.71cc.02XX
```



