# MI-PB-11
**Architektura, technologie a protokoly IPv6.**

---

#### Rozdíly IPv4 a IPv6

**Délka IPv6 adresy:** 
IPv6: 128 bitů = 8 dvojic bytů 
IPv4: 32 bitů

**Komprese adres:**
IPv6: 0 na začátku dvojice se nepíšou, nulový blok `:0:`, vypuštění nulových bloků `::` (pouze jednou)

1 IPv6 rozhraní -- i **více adres**

**Link-local adresy:**
* Komunikace dvou zařízení v jednom segmentu (neroutovaném -- Ethernet LAN)
* Každé IPv6 rozhraní má link local adresu. Mimo segment nemusí být unikátní
* Prefix `fe80::/10`
* Původně tvořeny na základě MAC adresy, dnes na základě hash

**Unique-local adresy:**
* Lokální použití privátních adres (obdoba privátních IPv4)
* Střídavě je a není standard
* Prefix `fc00::/7`
* Je možnost NAT66, ale není důvod -- ULA k tomu nebyly navrženy
    * 1 rozhraní může mít více IPv6 adres -- unique-local, link-local i global-unicast zároveň, každou adresu může routovat a konfigurovat jinak

**Není ARP:**
* IPv6 nemá broadcast, na kterém ARP stojí
* **Router Discovery Protocol:** 
    * hledání default GW
    * multicast na `ff02::2` -- všechny routery v link-local segmentu
* **Neighbor Discovery Protocol:**
    * Nalezení jiného zařízení v segmentu
    * Multicast na `ff02::1`
    * Funkce:
        * Nalezení routerů, DNS serverů
        * Automatická konfigurace adres
        * Objevování dalších zařízení na lince
        * Informace o dosažitelnosti sousedů uložených v cache

**Zajímavé adresy:**
* Localhost: `::1/128`
* Default GW: `::/0`
* Link Local: `fe80::/10`
* Unique Local: `fc00::/7`
* Multicast: `ff00::/16`

**DHCP:**
* **Stateful:**
    * Existuje DHCP server
    * DORA - discover, offer, request, ACK
    * Server přidělí:
        * IP z poolu
        * masku
        * DNS 1, 2
        * options (např. TFTP server pro telefony)
    * Default GW - nalezení pomocí RDP + router advertisement
* **Stateless:**
    * Existuje DHCP server
    * DORA
    * Server přidělí:
        * síťovou adresu
        * masku
        * DNS 1, 2
        * options
    * Default GW: RDP
    * Každé zařízení si samo určí adresu: `sitova_adresa:EUI-64`, kde EUI-64 je MAC adresa rozdělená napůl, mezi poloviny se vloží `fffe` a 7. bit se invertuje
* **Stateless address autoconfiguration (SLAAC):**
    * Bez DHCP serveru
    * Odposlech provozu: získání síťové adresy
    * síťová adresa + EUI-64 $\Rightarrow$ IPv6 adresa
    * Default GW: RDP + router advertisement

---

#### IPv6 Routing

RIPv3, OSPFv3, EIGRPv6

**Konfigurace protokolu:**
* U rozhraní
* Globální -- jenom aktivace

OSPF a EIGRP potřebují **router ID:**
Vypadá jako IPv4 adresa
Ručně: `router-id 1.2.3.4`, nebo z definované IPv4 adresy
Nedefinovaná IPv4, nenastaveno ručně $\Rightarrow$ nefunguje

---

#### Spolupráce IPv4 a IPv6

**Dual stack:**
* IPv4 + IPv6
* nastavení zvlášť
    * `sh ip route` : IPv4 routy
    * `sh ipv6 route` : IPv6 routy

**Tunelling:**
* IP over IP
* Obyčejně pomocí GRE (generic route encapsulation) tunelu
* IPv6 aket: `dest IPv6 | source IPv6 | data | CRC`
* Enkapsulace do IPv4 paketu: `dest IPv4 | source IPv4 | IPv6 paket | CRC`

**6to4:**
* Přenos IPv6 paketů přes IPv4 síť bez konfigurace specifických tunelů
* **Komunikace IPv4$\rightarrow$IPv6:** Jednoznačné mapování IPv4 na IPv6: 
    * IPv4 adresa `1.2.3.4` $\Rightarrow$ `00000001 | 00000010 | 00000011 | 00000100` = `0x01020304`
    * IPv6: prefix + IPv4 $\Rightarrow$ `prefix:0102:0304/64`
* **Komunikace IPv6$\rightarrow$IPv4:** enkapsulace IPv6 do IPv4
* **Relay router:** mezi IPv4 a IPv6 sítěmi
    * IPv4 6to4 paket $\rightarrow$ relay: rozbalení, routing IPv6 paketu do IPv6 sítě
    * IPv6 paket s 6to4 prexifem adresy $\rightarrow$ relay: Enkapsulace, odeslání do IPv4 sítě (na přeloženou adresu)