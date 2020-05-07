# MI-PB-10
**Border Gateway Protocol, popis, pravidla a aplikace.**

---

#### Routing protokoly

**Autonomní systém (AS):** skupina směrovačů a IP prefixů pod společnou správou (se společnou směrovací politikou)

**Interior gateway protocol (IGP):** v rámci 1 autonomního systému
Např. Routing Information Protocol (RIP), Open Shortest Path First (OSPF), Enhanced Interior Gateway Protocol (EIGRP), IGRP

**Exterior gateway protocol (EGP):** směrování mezi autonomními systémy (BGP)

---

#### Border Gateway Protocol

**BGP:** routing protokol na aplikační vrstvě

**Princip:** hledání cesty skrz různé AS -- posloupnost čísel (každé pouze jednou).
Nejednoznačná metrika -- každý AS upřednostňuje něco jiného.

**Dvě verze:**
* **EBGP:** mezi AS
* **IBGP:** uvnitř AS (není potřeba redistribuce směrovacích informací do IGP)

**Vlastnosti BGP:**
* **Must be routed:** Nefunguje přes default gateway
* **Pouze unicast:** nutno manuálně definovat sousedy
* Pomalá konvergence
* Autentizace
* 4 GB tabulka
* 12 parametrů, některé tranzitivní, jiné lokální

**BGP table:** Obsahuje všechny cesty od všech sousedů s různými metrikami

**BGP table $\leftrightarrow$ routing table:**
* **$\rightarrow$ routing table:**
    * nejlepší cesta automaticky do RT
    * route redistribuce (nedoporučuje se) -- distribuce směrů mezi směrovacími protokoly: převod metrik 
    * route maps (nedoporučuje se) -- access list pro směrování
* **$\rightarrow$ BGP table:**
    * virtual routing and forwarding -- partition paměti routeru, redistribuce mezi nimi
    * redistribution (nedoporučuje se)
    * manuálně
    * manuálně bez routing table

**BGP nefunguje, když:**
* Nefunguje IGP (sítě nedosažitelné apod.)
* Pouze 1 hraniční router $\Rightarrow$ BGP k ničemu -- radši použít default gateway
* 2 hraniční routery, ale připojené k 1 ISP -- radši 2 default GW
* 1 hraniční router, 2 připojené ISP routery (multihoming)

$\Rightarrow$ **jediné využití:** redundantní multihoming (2 hraniční routery napojené IXI na 2 ISP routery)

**Pravidla BGP:**
* **Golden Rule:** "neříkej mi, jak mám pít svoje latté"
    * Když posílám data přes jiný AS, nemůžu po něm vyžadovat, aby data směroval jinak/jinudy, než by směroval svá vlastní data.
* **Synchronizace:** 
    * Problém u AS bez BGP: na jejich hranicích zahazovány BGP pakety (IGP neznají cesty mimo jejich AS)
    * Synchronizace: IGP vidí stejné sítě jako BGP. IBGP distribuuje ven z AS (do EBGP) pouze ty směry, co cokáže ověřit přes IGP
    * Účel: ochrana před black-holing, když není IBGP full mesh
* **Split horizon:** (IBGP)
    * V BGP jsou zakázány cykly (když je v BGP routě číslo mého AS, zahodit)
    * Route naučená z jednoho směru nebude do tohoto směru propagována znovu
    * Účel: ochrana před loopy při IBGP full mesh
    * Route reflector: 
        * 1 hlavní router, který zná všechny cesty v AS
        * IBGP sousedi: pouze dvojice RR a jiný router (tvoří hvězdu)
        * eliminace potřeby full mesh IBGP
        * umožní naučení všech cest v AS bez tvorby cyklů

**BGP confederation:** 2 různé IBGP AS propojené EBGP -- tvoří AS jako celek

**BGP metriky:**
* **AS_PATH:**
    * tranzitivní
    * cesta přes autonomní systémy -- posloupnost jejich čísel
    * kratší = preferovanější
* **LOCAL PREFERENCE:**
    * lokální pro 1 AS
    * více možných cest z AS, chci jednu preferovat
    * vyšší = preferovanější
* **WEIGHT:**
    * lokální pro 1 router
    * jako LOCAL PREFERENCE, ale v rámci routeru
* **MED (MULTI-EXIT DISCRIMINATOR):**
    * výměna mezi sousedními AS
    * preference cesty pro příchozí provoz
* **NEXT_HOP:**
    * router, kam by se měl paket poslat dál