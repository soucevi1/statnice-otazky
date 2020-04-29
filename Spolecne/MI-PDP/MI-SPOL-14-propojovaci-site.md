#  MI-SPOL-14	
**Přímé ortogonální a hyperkubické propojovací sítě paralelních počítačů (definice, vlastnosti, vnořování).**

---

#### Teorie grafů
*(pouze jednoduché souvislé grafy bez smyček)*

* **Množina uzlů a hran grafu $G$:** $V(G), E(G)$
* **Velikost** grafu $G$: $N = |V(G)|$
* **Sousední uzly** $u$ a $v = $ **hrana** $\left< u, v \right>$
* **Stupeň uzlu** $u$: $\deg_G(u) = \# \text{sousedů uzlu } u$
* **Množina stupňů grafu $G$:** $\deg(G) = \{deg_G(u): u \in V(G)\}$
* **Maximální stupeň grafu $G$:** $\Delta(G) = \max (\deg(G))$
* **Minimální stupeň grafu $G$:** $\delta(G) = \min(\deg(G))$
* **$k$-regulární graf $G$:** $\Delta (G) = \delta(G) = k$

**Topologie:**
* **Tolopogie $G_n$:** množina grafů (= instancí topologie), jejichž velikost a struktura je definovaná parametrem $n$ (= velikostí dimenze).
Může být **vícedimenzionální.**
* **Hierarchicky rekurzivní topologie:** instance menších dimenzí jsou podgrafy instancí větších dimenzí
* **Inkrementálně škálovatelná topologie:** definovaná $\forall n$
* **Částečne škálovatelná topologie:** definovaná pro některá, ale $\infty$ mnoho $n$
* **Řídká topologie:** $|E(G_n)| = O(|V(G_n)|)$ (stupně uzlů omezeny konstantou)
* **Hustá topologie:** $|E(G_n)| = \omega(|V(G_n)|)$ (stupně uzlů roustoucí funkcí $n$)

**Kartézský součin:** $G = G_1 \times G_2$
$V(G) = \{[x,y]: x \in V(G_1), y \in V(G_2)\}$
$E(G) = \{ \left<[x_1, y], [x_2, y]\right> : \left<x_1, x_2\right> \in E(G_1) \} \cup \{ \left<[x, y_1], [x, y_2]\right> : \left<y_1, y_2\right> \in E(G_2) \}$
![](karts.png)
**Komutativní** a **asociativní**
Značení: $G \times G = G^2$

**Uzlově symetrický graf:** 
$\forall u_1, u_2 \in V(G) \exist$ automorfismus $f$ t.ž. $f(u_1) = u_2$
$G_1, G_2$ uzlově symetrické $\Rightarrow G = G_1 \times G_2$ také uzlově symetrický
Každý uzlově symetrický graf je regulární
Kružnice a klika uzlově symetrické

**Vzdálenosti a průměr:**
* **Délka cesty $P(u,v)$:** $\text{len}(P(u,v)) = \#$ hran v $P(u,v)$
* **Vzdálenost uzlů $u,v$:** $\text{dist}_G(u,v) = $ délka nejkratší $P(u,v)$
* **Průměrná vzdálenost** v $N$-uzlovém $G$: $\bar{\text{dist}}(G) = \frac{1}{N-1}\sum_{u,v: u \neq v}\text{dist}_G(u,v)$
* **Excentricita uzlu $u$:** $\text{exc}(u) = \max_{v \in V(G)} \text{dist}_G(u,v)$ *(vzdálenost od nejvzdálenějšího vrcholu)*
* **Průměr grafu $G$:** $\text{diam}(G) = \max_{u,v} \text{dist}_G(u,v) = \max_u \text{exc}(u)$ *(největší vzdálenost mezi dvěma vrcholy)*
* **Poloměr grafu $G$:** $r(G) = \min_u \text{exc}(u)$
* **Uzlově disjunktní cesty:** $V(P_1(u,v)) \cap V(P_2(x,y)) = \{u,v\} \cap \{x,y\}$
* **Hranově disjunktní cesty:** $E(P_1(u,v)) \cap E(P_2(x,y)) = \emptyset$

**Uzlový (hranový) řez:** Množina uzlů (hran), jejichž odebráním se rozpojí graf
**Uzlová (hranová) souvislost grafu $G$:** $\kappa(G) (\lambda(G)) = $ velikost minimálního uzlového (hranového) řezu

**Hranová bisekční šířka:** $\text{bw}_e(G)$ -- velikost nejmenšího hranového řezu **na 2 poloviny**

---

#### Požadavky na propojovací sítě
* **Konstantní stupěň uzlu:** univerzální a levné směrovače, řídká topologie (malá souvislost, velké vzdálenosti)
* **Malý průměr a malá průměrná vzdálenost:** snižuje komunikační zpoždění
Spodní mez průměrů $k$ uzlové řídké sítě: $\Omega(\log N)$
* **Uzlová symetrie a hierarchická rekurzivita:** snazší návrh algoritmů (nezáleží, kde algoritmus začne), částečná škálovatelnost, induktivní návrh
* **Vysoká souvislost:** redundantní cesty pro případ výpadku, dělení paketů a posílání paralelními cestami
* **Vnořitelnost do jiných topologií:** simulace jiné topologie
* **Podpora pro směrování a kolektivní komunikační operace:** permutačín směrování, operace jeden-všem, všichni-všem

---

#### Základní přímé propojovací sítě
* **Ortogonální:** (konstruktor = kartézský součin)
    * Binární hyperkrychle
    * Mřížky
    * Toroidy
* **Hyperkubické**: (odvozené od hyperkrychle rozvinutím každého uzlu hyperkrychle do více uzlů)
    * Motýlci

---

#### Binární hyperkrychle dimenze $n$ $(Q_n)$
![](hyperk.png)
$V(Q_n) = \mathcal B^n$, $|V(Q_n)| = 2^n$
$E(Q_n) = \{x, \text{neg}_i(x): x \in V(Q_n), 0\leq i \lt n\}$, $|E(Q_n)| = n2^{n-1}$
$\text{diam}(Q_n) = n$
$\deg(Q_n) = \{n\}$
$\text{bw}_e(Q_n) = 2^{n-1}$

* **regulární** graf
* logaritmický stupeň uzlů $\Rightarrow$ **není řídká** (škálování pouze po mocninách dvojky -- v praxi hyperkrychle vzácné)
* **hierarchicky rekurzivní:** $Q_n \equiv Q_p \times Q_{n-p} \equiv Q_p \times Q_q \times Q_{n-p-q} \equiv Q_1^n$
    * Podkrychle: $s_{n-1}...s_1s_0$, kde $s_i \in \{0,1,*\}$ ($*$ -- neutrální symbol) *(termy v booleovské algebře)*
* **uzlová symetrie:** $Q_n \equiv Q_1^n$
* **automorfismy:** $2^n \times n!$
    * **přeložení $u \rightarrow v$:** $\forall x \in V(Q_n): x \rightarrow x \oplus_2 (u \oplus_2 v)$ 
    * **permutace (přejmenování) dimenzí**
* optimální souvislost: $\lambda(Q_n) = \kappa(Q_n) = n$
* největší možná bisekční šířka -- vyvážený bipartitní graf
* $\#$ uzlů ve vzdálenosti $i$ je $n \choose{i}$ $\Rightarrow \bar{\text{dist}}(Q_n) = \lceil n/2 \rceil$
* $k!$ různých nejkratších cest mezi uzly ve vzdálenosti $k$ 
* **směrování:** testování bitů v adresách zprava doleva

---

#### $n$-rozměrná mřížka rozměrů $z_1, z_2, ..., z_n: M(z_1, z_2, ..., z_n)$
![](mriz.png)
$V(M(...)) = \{ (a_1,a_2,...,a_n): 0 \leq a_i \leq z_i-1 \forall i \in \{1,...,n\} \}$ *(vrchol má celočíselné souřadnice)*
$|V(M(...))| = \Pi_{i=1}^n z_i$ *(produkt rozměrů)*

$E(M(...)) = \{ \left< (...,a_i,...), (..., a_i+1, ...) \right>: 0 \leq a_i \leq z_i-2 \}$ 
*(hrana mezi vrcholy lišící se v jedné souřadnici o 1)*
$|E(M(...))| = \sum_{i=1}^n(z_i-1)\Pi_{j=1, j \neq i}^n z_j$

$\text{diam}(M(...)) = \sum_{i=1}^n(z_i-1) = \Omega(\sqrt[n]{|V(M(...))|})$ 
*(Vzdálenost po 1 rozměru: rozměr-1. Ve více rozměrech: suma(rozměr-1))*

$\deg(M(...)) = \{n, ..., n+j\}, j = |\{z_i: z_i >2\}|$ 
*($n$ je v rohu, $j$ je počet rozměrů větších než 2)*

$\text{bw}_e(M(...)) = (\Pi_{i=1}^n z_i)/\max_i z_i$ pro $\max_i z_i$ sudé, $\Omega((\Pi_{i=1}^n z_i)/\max_i z_i)$ pro liché

* *(předpoklad, že dimenze $n$ je konstantní)*
* $M(k,k,...,k)$: **$k$-ární $n$-krychle**
* **není regulární** ani uzlově symetrická
* **velký průměr**
* **počet uzlů ve vzdálenosti $i$** (2D mřížka): od $i+1$ do $4i$
* **hierarchicky rekurzivní:** 
    * $M(z_1, z_2,..., z_n) \equiv M(z_1) \times M(z_2) \times ... \times M(z_n)$
* optimální souvislost
* přesná hodnota bisekční šířky pro obecné $n$ je kombinatorickým problémem
* **směrování:** dimenzně uspořádané (= **XY** a **XYZ** směrování)
* vždy bipartitní

---

#### $n$-rozměrný toroid dimenzí $z_1, z_2, ..., z_n: K(z_1, z_2, ..., z_n)$
**Toroid:** zabalená mřížka = $n$-rozměrná kružnice

![](tor.png)

$V(K(...)) = V(M(...))$ *(vrchol má celočíselné souřadnice)*

$E(K(...)) = \{ \left< (...,a_i,...), (..., a_i\oplus_{z_i}1, ...) \right>: 0 \leq a_i \leq z_i \}$ 
*(hrana mezi vrcholy lišící se v jedné souřadnici o modulo 1)*
$|E(K(...))| = n \times \Pi_{i=1}^n z_i$

$\text{diam}(K(...)) = \sum_{i=1}^n \lfloor z_i/2 \rfloor$ 
*(Vzdálenost po 1 rozměru: maximálně rozměr/2.)*

$\deg(K(...)) = \{2n\}$ 

$\text{bw}_e(K(...)) = 2 \text{bw}_e(M...))$

* $K(k,k,...,k)$: $k$-ární $n$-toroid
* **regulární**
* **uzlově symetrický** (automorfismy = přeložení)
* **hierarchicky rekurzivní:**
    * $K(z_1, z_2, ..., z_n) \equiv K(z_1) \times K(z_2) \times ... \times K(z_n)$
    *  Na rozdíl od mřížek nelze rozdělit na stejnorozměrné podtoroidy
* Bipartitní $\Leftrightarrow$ všechny délky stran jsou sudé

---
#### Porovnání hyperkrychlí, mřížek a toroidů
* $M(2,2,..., 2) \equiv Q_n$
* $n$-rozměrné mřížky a toroidy jsou zobecněním $Q_n$
* Pro určitá $k,n, k < n$, $k$-rozměrná mřížka/toroid může být podgrafem $Q_n$
* $K(4,4) \equiv Q_4$

---

#### Hyperkubické sítě
Grafy odvozené od hyperkrychle rozvinutím všech uzlů hyperkrychle do více uzlů
**Spolčené vlastnosti:**
* $O(1)$ stupeň  
* $O(\log N)$ průměr
* škálovatelné hůř než hyperkrychle
* bisekční šířka $\Omega(N/\log N)$

**Normální hyperkubický algoritmus:** v každém kroku algoritmu použity pouze hrany jedné dimenze hyperkrychle, v po sobě jdoucích krocích používány po sobě jdoucí dimenze

---

#### Zabalený motýlek dimenze $n$: $wBF_n$
![](wbf.png)

$V(wBF_n) = \{ (i,x): 0 \leq i \lt n \wedge x \in \mathcal B^n \}$ *(souřadnice v kružnici a v krychli)*
$|V(wBF_n)| = n2^n$ *(kružnice x krychle)*

$E(wBF_n) = \{ \left< (i,x), (i \oplus_n 1, x) \right>, \left< (i,x), (i \oplus_n 1, \text{neg}_i(x)) \right>: (i,x) \in V(wBF_n) \}$ 
*(hrana mezi vrcholy lišící se v krychlové souřadnici o 1 (mod n), případně ještě o jeden bit krychlové souřadnice)*
$|E(wBF_n)| = n2^{n+1}$ 
*($n$ hran v kružnici, $2^n$ kružnic)*

$\text{diam}(wBF_n) = n + \lfloor \frac{n}{2} \rfloor$ 
*(Vzdálenost v krychli a pak v kružnici)*

$\deg(wBF_n) = \{4\}$ 

$\text{bw}_e(wBF_n) = 2^n$

* **řídký** grf s optimálním průměren
* **uzlově symetrický**
* **není** hierarchicky rekurzivní
* vyvážený bipartitní $\Leftrightarrow$ $n$ sudé

---

#### Obyčejný motýlek dimenze $n$: $oBF_n$

Otevřením kružnic vznikl další vrchol a kružnicová souřadnice tak má $n$ hran a $n+1$ vrcholů
Otevřená kružnice = 1D mřížka

![](obf.png)

$V(oBF_n) = \{ (i,x): 0 \leq i \lt n \wedge x \in \mathcal B^n \}$ *(souřadnice v otevřené kružnici a v krychli)*
$|V(oBF_n)| = (n+1)2^n$ *(kružnice x krychle, kružnice se bere jako n+1)*

$E(oBF_n) = \{ \left< (i,x), (i + 1, x) \right>, \left< (i,x), (i + 1, \text{neg}_i(x)) \right>: i < n \}$ 
*(hrana mezi vrcholy lišící se v krychlové souřadnici o 1, případně ještě o jeden bit krychlové souřadnice)*
$|E(oBF_n)| = n2^{n+1}$ 
*($n$ hran v otevřené kružnici, $2^n$ kružnic)*

$\text{diam}(oBF_n) = 2n$ 
*(Vzdálenost v krychli a pak v otevřené kružnici)*

$\deg(oBF_n) = \{2,4\}$ 

$\text{bw}_e(oBF_n) = 2^n$

* uzly organizovány do **sloupců (stupňů)** $0 \leq i \leq n$ a **řad** $0 \leq x \leq 2^n -1$
* dva druhy hran: **přímé** a **křížové (hyperkubické)**
* **není** uzlově symetrický ani regulární
* **hierarchicky rekurzivní:** $oBF_n$ obsahuje dva $oBF_{n-1}$
* bipartitní
* $\forall x,y$ existuje **jediná nejkratší cesta** mezi $(0,x)$ a $(n,y)$

---

#### Vnořování

**Vnoření $G \xrightarrow{\text{emb}} H$** zdrojového grafu $G = (V(G), E(G))$ do cílové sítě $H=(V(H), E(H))$ je **dvojice zobrazení** $(\varphi, \xi)$, kde
$\varphi: V(G) \rightarrow V(H)$ a $\xi: E(G) \rightarrow \mathcal P(H)$
*($\mathcal P(H) =$ množina všech **cest** sítě $H$)*

**Měřítka vnoření:**
* **Maximální zatížení cílového uzlu:** $\text{load}(\varphi, \xi) = \max_{v \in V(H)}|\{u \in V(G): \varphi(u) = v\}|$ 
*(kolik se maximálně zobrazí vrcholů na cílový vrchol)*

* **Expanze vnoření:** $\text{vexp}(\varphi, \xi)= \frac{|V(H)|}{|V(G)|}$

* **Maximální dilatace zdrojových hran v cílové síti:** $\text{dil}(\varphi, \xi) = \max_{e_1 \in E(G)} \text{len}(\xi(e_1))$
*(maximální délka obrazu hrany -- na kolik maximálně hran se zobrazí jedna hrana zdroje)*
Pokud $|V(G)| = |V(H)|$ a $\text{load}(\varphi, \xi) = 1$, pak $\text{dil}(\varphi, \xi) \geq \lceil \text{diam}(H)/\text{diam}(G) \rceil$

* **Maximální zahlcení cílové hrany:** $\text{ecng}(\varphi, \xi) = \max_{e_2 \in E(H)} |\{e_1 \in E(G): e_2 \subseteq \xi(e_1)\}|$
*(kolik maximálně hran je zobrazeno na jednu hranu cíle)*

Grafy $G$ a $H$ jsou **kvaziizomaterické**, pokud existují vnotření $G \xrightarrow{\text{emb}}H$ i $H \xrightarrow{\text{emb}}G$ s konstantními hodnotami měřítek

**$H$ simuluje $G$ se zpomalením $h$**, pokud jeden krok výpočtu na $G$ může být simulován na $H$ v $O(h)$ krocích

**$G$ a $H$ jsou výpočetně ekvivalentní sítě**, pokud $G$ dokáže simulovat $H$ s konstantním zpomalením a naopak

**Problém vnoření:**
* Problém existence libobolného vnoření stromu $S$ do $Q_n$, kde $n$ je dáno nebo $n = \log|V(S)|$ s dil $=$ ecng $=1$, je **NP-úplný**
* Dán graf $G$ a celá čísla $k,n$. Problém existence vnoření $G$ do $Q_n$ (nebo $n$-rozměrné mřížky) s dilatací $k$ je **NP-úplný**

---

**Hyperkrychle** simuluje optimálně většinu topologií
Je nativní topologií pro realizaci výpočtu **Rozděl-a-polovinu-nech**

$M(z_1, z_2, ..., z_n)$ a $K(z_1, z_2, ..., z_n)$ jsou **kvaziizometrické** $\Rightarrow$ **výpočetně ekvivalentní.**
     $M \subset K \Rightarrow K$ simuluje $M$ bez zpomalení
     Existuje $K \xrightarrow{emb} M$ s load = 1 a dil = ecng = 2: kartézská dekompozice
     ![](kartdec.png)

**Vnoření cest a kružnic do hyperkrychle:**
Binární zrcadlový Grayův kód:
$G_1 = \{0,1\}$, $G_n = \{0G_{n-1}, 1G^R_{n-1}\}$
![](gray.png)

**Vnoření hyperkrychle do mřížky/toroidu:**
* Dolní mez na dilataci s load $= 1$ je $2^k/k$
* **Mortonova křivka:** spojení uzlů v lexikografickém pořadí při dělení střídavě podle osy $x$ a $y$ (sudé bity mapovány na $x$, liché na $y$)
![](morton.png)

**Vnoření 2D toroidu do 1D toroidu:**
![](vntor.png)

**Vnoření čtvercové mřížky do obdélníkové mřížky:**
Jednotlivé sloupce mřížky S bereme zleva doprava a hadovitě zanořujeme do R tak, že sousední sloupce tvoří stejnolehlé hady, rozmísťované tak, aby se nepřekrývaly. Některé uzly v R tedy zůstávají nevyužity, a proto dorazíme k pravému kraji R dříve, než se všechny sloupce S podaří rozmístit. Had, který narazí na kraj R, se jakoby odrazí a nepřerušeně pokračuje ve zpětném směru. Proto budou některé uzly R zatíženy dvěma uzly S, zatímco některé zůstanou volné. 
![](vnmr.png)

**Vnoření obdélníkové mřížky do čtvercové:**
Uzly S blízko vertikálního kraje mají load = 0 nebo load = 2
![](odbct.png)

**Otevřený a kružnicový motýlek jsou kvaziizometrické:**
$oBF_n$ lze triviálně vnořit do $wBF_n$ s load = 2 a dil = 1. Sloučením koncových uzlů $oBF_n$ se získají kružnice $wBF_n$

Vnoření $wBF_n$ do $oBF_n$: 
dil $\leq 3$
![](vnmot.png)
* Při cestě z (0, 1111) do (0, 0000) nutno navštívit každou krychlovou dimenzi (invertovat všechny bity)
* Při triviálním vnoření (a,b) (invertování bitů v pořadí 0,1,2,3) je dil = $\log N$
* Řešení: invertovat bity v jiném pořadí -- inspirace v kartézské dekompozici (přeskakování) -- pořadí 1,3,2,0 a dilatace je 3, zavedení permutace $\pi : {0,1,2,3} \rightarrow {1,3,2,0}$
* Kružnice $wBF_n$ se permutují podle $\pi^{-1}$ (d)
* Permutovaný $wBF_n$ se vnoří do $oBF_n$ (graf d co grafu c)