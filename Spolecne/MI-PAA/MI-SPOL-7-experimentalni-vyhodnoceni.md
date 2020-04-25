# MI-SPOL-7	
**Experimentální vyhodnocení algoritmů, zejména randomizovaných.**

---

#### Experiment:
* **plán experimentu** 
    * *co chci zjistit?*
    * spuštění algoritmu:
    instance$_1 \rightarrow$ výsledek$_1$
    instance$_2 \rightarrow$ výsledek$_2$
    ...
    * *otázka:* závislost výstupních veličin na vstupních veličinách
    *odpověď:* kvantitativní výrok (vzorec) o té závislosti
* **provedení experimentu**
veličina$_a$ instance$_1\rightarrow$ veličina$_b$ výsledku$_1$
veličina$_a$ instance$_2\rightarrow$ veličina$_b$ výsledku$_2$
...
* **interpretace výsledků** 
    * odpověď různé kvality
    * veličina$_b = F($veličina$_a)$

**Prakticky použitelná odpověď:**
* vyžaduje zobecnění (extrapolaci)
* nezávislá na veličinách, které v ní nejsou zahrnuty (vyloučení ostatních vlivů, předpoklad jejich statistického rozložení)
* musí vypovídat o významné závislosti (testy hypotéz)

Veřejně dostupné zkušební sady (benchmarks)

---

#### Obecné vyhodnocení algoritmu:

![](exper.png)

**Statistika:** jedna hodnota zadané charakteristiky, např. průměr, medián

**Srovnání:** $A$ je systematicky lepší než $B$: dominance
Hlubší analýza: charakteristika instancí, kde je $A$ lepší

---

#### Randomizovaný algritmus

![](experr.png)

**Dva zdroje variance** (generátor instancí a sám algoritmus) -- dva stupně zpracování
Statistické rozložení nemusí být stejné

**Srovnání na jedné instanci:**
* přes inicializaci RNG
* $A$ systematicky lepší než $B$: dominance (na zkoušených instancích)
Pro které hodnoty RNG dělat hlubší analýzu?

---

**Robustnost heuristiky:** závislost práce heuristiky na lexikálním uspořádání dat, které nemění význam
*(zpřeházení klauzulí SAT -> jiné řešení v jiném čase, 
zpřeházení pořadí deklarace proměnných -> rychlejší program)*

**Měření robustnosti:**
![](rob.png)

---

#### Inženýrská algoritmika

![](inza.png)

* žádná známá standardní sada instancí **nemá zaručenou statistickou reprezentativnost:** 
    * neplatí statistické předpoklady
    * nefunguje průměrování
    * nelze eliminovat neznámé zdroje šumu
    * ze statistiky zbyl pouze existenční kvantifikátor (existuje instance, na které...)
* srovnání: **vzhledem k dané sadě** instancí
* **relevantnost pro praxi:** otázka na autora sady

---

#### Vizualizace

Pro heuristiky pracující iterativně s **jednou aktuální konfigurací**

Nejčastěji **vývoj optimalizačního kritéria** s pořadím iterace

**Lze odpozorovat některé vlastnosti:**
* heuristika skončí u **nejbližšího trochu dobrého** řešení a jiná ani nezkoumá
* heuristika **bezcílně bloudí** prostorem konfigurací
* heuristika nachází **čím dál horší** řešení
* heuristika hledá správně, ale **skončí moc brzy**

---

#### Práce s heuristikou

* **white box evaluation:**
    * omezená sada instancí
    * detailní měření
    * vhled, porozumění
    * modifikace heuristiky
* **black box evaluation:**
    * plná sada instancí
    * měření výsledků
    * ověření kvality a výkonu
    * žádné modifikace heuristiky

**Více parametrů heuristiky:**
* obecně nejsou nezávislé -- nutno ověřit
* nastavování více parametrů = cesta prostorem konfigurací heuristiky

---

#### Praktické nasazení heuristik
* praktické požadavky: rychlost, kvalita, žádná intervence koncového uživatele
* heuristiky:
    * výměnné části, parametry, vzájemná závislost
* práce s heuristikou a experimentální vyhodnocení:
    * vhled do činnosti heuristiky
    * white box, black box
    * standardní zkušební úlohy
    * otázka, plán, experiment
* vizualizace