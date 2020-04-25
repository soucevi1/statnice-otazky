# MI-SPOL-9	
**Princip genetických algoritmů, význam selekčního tlaku pro jejich funkci.**

---

#### Principy:
* **více stavů najendou** $\Rightarrow$ menší šance uváznutí v lokálním minimu, konstantní počet stavů po celý výpočet
* **operátory:** 
$S \rightarrow S$ (unární)
$S\times S \rightarrow S, S \times S \rightarrow S \times S$ (binární)
* **definice operátorů:** nad reprezentacemi X problémově nezávislé

---

#### Analogie

* konfigurace = jedinec
* kódování konfigurace = genetická reprezentace jedince
* proměnná kódování = gen
* hodnota proměnné = alela
* aktuální množina konfigurací = generace, populace
* unární operátor = mutace
* binární operátor = křízení
* optimalizační kritérium = zdatnost (fitness)
* rozšíření konfigurace uvázlé v lokálním minimu = degenerace
* rozšíření kvalitní konfigurace = konvergence
* biodiverzita = diverzita populace

---

#### Kostra simulované evoluce

![](kgen.png)

---
#### Evoluční algoritmy
**Společné rysy:**
* více individuí
* diverzifikace: mutace atd.
* intenzifikace: selekce pro rekombinaci nebo další generaci

**Charakteristické rysy jednotlivých algoritmů:**
* reprezentace
* unární, binární operátory
* způsob selekce pro rekombinaci a konstrukci následující generace

##### Klasická podoba genetických algoritmů

| Kódování     | Operátory     | Řízení populace |
|--------------|---------------|------|
| Binární řetěz| Binární: křízení (1-bodové, 2-bodové, uniformní), Unární: mutace, inverze | nová generace nahradí původní
  
##### Evoluční strategie
| Kódování | Operátory | Řízení populace |
|---|---|---|
|Vektor (reálných) čísel. Strategické parametry: $\sigma$ mutace, interakce mezi složkami | mutace (dominuje): přičtení Gaussova rozložení, Křízení: diskriminující, průměrující | Z $\mu$ rodičů a $\lambda$ potomků se vybere $\mu$ členů nové generace, nebo náhrada vcelku

##### Genetické programování
|Kódování | Operátory | Řízení populace |
|---|---|---|
| Rozkladový strom výrazu | Křízení, mutace, definice stavebního bloku, editace | Nová populace nahradí starou |

##### Evoluční programování
|Kódování | Operátory | Řízení populace |
|---|---|---|
| Automat | Změna výstupního symbolu, změna přechodu, přidání/vypuštění stavu, změna počátečního stavu| Z $\mu$ rodičů a $\lambda$ potomků se vybere $\mu$ členů nové generace|

----

#### Genetické algoritmy
**Kódování:**
* klasická formulace: binární řetěz
* vektor proměnných obecně různých domén
* permutace řetězce z dané abecedy

**Operátory:** 
* **Křížení (rekombinace):**
    * Jednobodové: 
    ![](jednobod.png)
    * Dvoubodové:
    ![](dvoubod.png)
    * Uniformní:
    ![](unif.png)
    * Permutační:
    ![](permk.png)
* **Inverze:** Každý bit náhodně buď invertovat, nebo ne
* **Mutace:** Z celé populace náhodně vybrat bod (bit v řetězci), který se invertuje

**Selekce:**
* **Účel:** způsobit, aby početní zastoupení jedince v populaci odpovídalo jeho zdatnosti
* = převod informace obsažené ve zdatnosti na informaci početnosti
* **Selekční tlak:** pravděpodobnost výběru nejlepšího jedince
    * Velký $\Rightarrow$ nebezpečí **degenerace** populace
    * Malý $\Rightarrow$ pomalá konvergence
    * Šum vnesený mutací může převážit nad pomalou konvergencí $\Rightarrow$ **divergence**

---

#### Způsob selekce
* **Ruletový výběr:** 
    * Pro každého jedince políčko v ruletě 
    * Rozevření políčka odpovídá žádané pravděpodobnosti výběru
    * $m$ náhodných voleb, $m$ prvků, jeden může být vybrán vícekrát
* **Univerzální stochastické  vzorkování:**
    * Ruleta stejná jako výše
    * Odměří se náhodný úhel a vybere se prvek
    * Dále se od tohoto bodu odměří $(m-1)$-krát úhel $\frac{2\pi}{m}$ a vždy se vybere prvek

U rulety často hrozí **degenerace** -- potřeba nadržovat slabším:
Přepočítání zdatnosti lineární funkce (**scaling**)
Použití pořadí ve zdatnosti místo zdatnosti (**ranking**)

* **Turnajový výběr:**
    * Náhodně vybrat $r$ jedinců (turnaj) a z něj nejlepšího
    * Opakovat až do naplnění populace
    * Selekční tlak řízen velikostí turnaje:
        * jeden jedinec: žádný tlak
        * celá populace: jistota výběru nejlepšího
* **Zkrácený výběr:**
    * Dán práh $0\lt p \lt 1$
    * Z populace $M$ jedinců vybráno $pM$ nejzdatnějších
    * Každý vstupuje do rekombinace $1/p$-krát
    * Informace obsažená ve zdatnosti redukována na jediný bit

---

#### Řízení populace

* **Náhrada en bloc:** nová generace vzniklá křížením nahradí starou
* **Částečná náhrada:** z $\mu$ rodičů a $\lambda$ potomků se vybere $\mu$ členů nové populace
* **Ustálená populace:** po křížení potomek (potomci) nahradí nejslabší(ho) jedince
* **Přechodové formy:** mezi en bloc a ustálenou populací

**Elitismus:** několik málo nejlepších jedinců automaticky přejde do další generace

Nutná **velikost populace** roste exponenciálně s velikostí problému
Malá populace (10 jedinců) -- ztráta diverzity
Obtížné problémy: 100 jedinců

---

#### Podmínky ukončení
* Prvný počet generací
* Příznaky konvergence -- změna průměrné zdatnosti mezi generacemi, rozložení zdatnosti v generaci

---

#### Omezující podmínky

Co když výsledek genetického algoritmu není řešením?

* **Relaxace:** omezující podmínky převedeny na penalizaci
    * Velikost penalizace: každé řešení lepší než ne-řešení VS minimální penalizace zabraňující akceptaci ne-řešení
    * Způsob: vzdálenost od řešení, odhad ceny opravy, počet porušených podmínek
* **Trest smrti:** zahození výsledku
    * Sníží dostupnost stavového prostoru
* **Dekodéry:** volba reprezentace tak, aby každý genotyp byl řešením

---

#### Reprezentace stavebních bloků

**Schéma:** To, co mají chromozómy společné (výběr bitů z řetězce)
$n$ genů $\Rightarrow 2^n$ schémat 
Jiný pohled: populace jako množina schémat

**Fast Messy GA:** Jedinec (schéma) kódován jako `pozice:hodnota | pozice:hodnota | ...`.
Zbytek nespecifikovaných informací doplněn z **referenčního jedince**