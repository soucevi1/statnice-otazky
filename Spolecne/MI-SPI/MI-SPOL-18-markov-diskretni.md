# MI-SPOL-18
**Markovské řetězce s diskrétním časem. Jejich limitní vlastnosti.**

---

**Náhodný proces:** $(\Omega, \mathcal F, P)$ pravděpodobnostní prostor a $T \subseteq \R$ indexová množina. Systém náhodných veličin $\mathbf X = \{X_t | t \in T\}, X_t: \Omega \rightarrow\R$ je **reálný náhodný proces.**

$T$ lze chápat jako **čas:** pokud $T$ nejvýše spočetná, jde o diskrétní čas, jinak spojitý čas

**Množina stavů $S$:** minimální podmnožina $\R$, pro kterou platí $P(X_t \in S) = 1$ pro každé $t \in T$ -- množina $S$ je společná množina hodnot veličin $X_t$

$\mathbf X = \{X_t | t \in T\}$ náhodný proces a $\omega \in \Omega$ elementární jev. Funkce $f: T \rightarrow \R$, kde $\forall t \in T: f(t) = X_t(\omega)$ je **trajektorie** nebo **realizace** náhodného procesu $\mathbf X$

**Rozdělení v čase $n \in \N$** charakterizované pravděpodobnostní funkcí: $\mathbf p_i(n) = P(X_n = i)$, $\mathbf p(n) = \left( \mathbf p_1(n), \mathbf p_2(n), ... \right)$
*(vektor pravděpodobností pro jednotlivé stavy v čase $n$)*

**Matice pravděpodobností přechodu za čas mezi $n$ a $m \geq n$:** $\mathbf P_{ij}(n,m) = P(X_m = j| X_n = i)$, $\mathbf P(n,m) = \left( \mathbf P_{ij}(n,m) \right)_{i,j \in S}$

---
#### Markovský řetězec

Náhodný proces $\{X_n | n \in \N_0\}$ s nejvýše spočetnou množinou stavů $S$ je **markovský řetězec s diskrétním časem**, pokdu splňuje **markovskou podmínku:** *(zapomínání historie)* $\forall n \in \N, \forall s, s_0, ..., s_n-1 \in S$ platí:
$$
P(X_n = s |X_{n-1} = s_{n-1}, ..., X_1 = s_1, X_0 = s_0) = P(X_n = s | X_{n-1} = s_{n-1})
$$

**Ekvivaltentní formulace markovské podmínky:**
* $P(X_{n+m} = s|X_m = s_m, ..., X_1 = s_1, X_0 = s_0) = P(X_{n+m} = s| X_m =s_m)$
* $\forall k \in \N, \forall n_0 < n_1 < ... < n_k \in \N_0, \forall s_0, ..., s_k \in S$ platí: $P(X_{n_k} = s_k | X_{n_{k-1}} = s_{k-1}, ..., X_{n_0} = s_0) = P(X_{n_k} = s_k | X_{n_{k-1}} = s_{k-1})$

**Ekvivalentní definice markovského řetězce:**
Náhodný proces $\{X_n | n \in \N_0\}$ s nejvýše spočetnou množinou stavů $S$ je markovský, právě když $\forall k \in \N, \forall n_0 < n_1 < ... < n_k \in \N_0, \forall s_0, ..., s_k \in S$ platí:
$$
P(X_{n_0} = s_0, ..., X_{n_k} = s_k) = \mathbf p_{s_0}(n_0) \cdot \mathbf P_{s_0s_1}(n_0,n_1) \cdot \mathbf P_{s_1s_2}(n_1,n_2)\cdot...\cdot \mathbf P_{s_{k-1}s_k}(n_{k-1}, n_k)
$$

**Chapman-Kolmogorova rovnice:** Pro matice přechodu markovského řetězce platí $\forall n \leq m \leq r \in \N_0$:
$$
\mathbf P(n,r) = \mathbf P(n,m) \cdot \mathbf P(m,r)
$$

---

#### Homogenní markovský řetězec

Markovský řetězec je **homogenní**, pokud $\forall n \in \N, \forall i,j \in S$ platí:
$$
P(X_{n+1} = j|X_n = i) = P(X_1 = j | X_0 = i)
$$

**(Jednokroková) matice přechodu:**
$$
\mathbf P = \mathbf P(0,1) = \left( P(X_1 = j | X_0 = i) \right)_{i,j \in S}
$$

Pro homogenní markovský řetězec platí $\forall m,n \in \N_0$:
$$
\mathbf P(m, m+n) = \mathbf P(0,n) = \mathbf P^n
$$

Matice $\mathbf P^n$ se značí i $\mathbf P(n)$.
Pravděpodobnost přechodu z $i \in S$ do $j \in S$ během $n$ kroků: $P(X_n = j | X_0 = i) = \mathbf P_{ij}(n) = (\mathbf P)_{ij}$

Chapman kolmogorova rovnice pro homogenní řetězec: $\mathbf P(n+m) = \mathbf P(n) \cdot \mathbf P(m)$, jinými slovy $\mathbf P^{n+m} = \mathbf P^n \cdot \mathbf P^m$

**Rozdělení náhodné veličiny $X_n$:**
Pro homogenní řetězec platí: $\mathbf p(n) = \mathbf p(m) \cdot \mathbf P^{n-m} = \mathbf p(0) \cdot \mathbf P^n$
*(vektor pravděpodobností pro jednotlivé časy v čase 0 $n$-krát vynásobený maticí)*

---

#### Stochastická matice

Matice přechodu $\mathbf P$ je **stochastická:**
* $\forall i,j \in S: P_{ij} \geq 0$
* $\forall i \in S: \sum_{j \in S}\mathbf P_{ij} = 1$ *(součet řádku = $1$)*

Součin stochastický matic je opět stochastická matice

$\Rightarrow$ k libovolné čtvercové stochastické matici $\mathbf P$ existuje **homogenní markovský řetězec s diskrétním časem** takový, že $\mathbf P$ je jeho maticí přechodu 

**Stacionární rozdělení:**
$\{X_n | n \in \N_0\}$ homogenní markovský řetězec s maticí přechodu $\mathbf P$. Pokud existuje vektor $\mathbf \pi$ t.ž.:
* $\forall i \in S: \mathbf \pi_i \geq 0$
* $\sum_{i \in S} \mathbf \pi_i = 1$

Pro který platí, že  $\mathbf \pi \cdot \mathbf P = \mathbf \pi$, nazývá se **stacionárním rozdělením** řetězce.
*(rozdělení, ze kterého neuteču)*

Pokud existuje stacionární rozdělení, pak
$$
\mathbf p(0) = \mathbf \pi \Rightarrow \mathbf p(n) = \mathbf \pi \mathbf P^n = ... = \mathbf \pi \mathbf P = \mathbf \pi
$$

Potom platí, že 
$$
P_{\mathbf \pi}(X_n = i) = \mathbf \pi_i
$$
*($P_{\mathbf \pi}$ je šance při počátečním rozdělení $\mathbf \pi$)*

---
#### Klasifikace stavů

Stav $i \in S$ je:
* **Trvalý (rekurentní):** $P(\exist n \in \N: X_n = i | X_0 = i) = 1$
*(každá trajektorie začínající v $i$ se do něj někdy v budoucnu stoprocentně vrátí)*
* **Přechodný (transientní):** $P(\exist n \in \N: X_n = i | X_0 = i) < 1$
*(existují trajektorie, které se do stavu $i$ už nikdy nevrátí)*

---
#### Časy návštěv

**Čas první návštěvy stavu $i \in S$:** $\tau_i = \min\{n \in \N | X_n = i\}$, pokud množina neprázdná. Jinak $\tau_i = +\infty$

První návštěva  $j$ při startu v $i$ nastane právě v $n$-tém kroku: 
$$
f_{ij}(n) = P(\tau_j = n | X_0 = i), n \geq 1, f_{ij}(0) = 0
$$

Pravděpodobnost, že řetězec někdy navštíví $j$, pokud začal v $i$: 
$$
f_{ij} = P(\tau_j < +\infty | X_0 = i) = \sum_{n=1}^\infty f_{ij}(n)
$$

**Důsledek:**
* $i \in S$ **trvalý** $\Leftrightarrow f_{ii} = P(\tau_i < +\infty | X_0 = i) = 1$
* $i \in S$ **přechodný** $\Leftrightarrow f_{ii} = P(\tau_i < +\infty | X_0 = i) < 1$

**Střední doba návratu do stavu $i \in S$:**
$$
\mu_i = E(\tau_i|X_0 = i) = \begin{cases} \sum_{n=1}^\infty n f_{ii}(n) & \text{pokud }i \text{ trvalý} \\ +\infty  & \text{pokud }i \text{ přechodný}  \end{cases}
$$

**Stav $i \in S$ je:**
* **Nenulový:** $\mu_i < + \infty$
* **Nulový:** $\mu_i = +\infty$

---
#### Periodicita
**Perioda stavu $i \in S$:** $d(i) = \gcd\{n \in \N| \mathbf P_{ii}(n)>0\}$
*(gcd časů, kdy se řetězec vrátí do stavu $i$)*
Stav $i$ **periodický**, pokud $d(i) >1$, jinak **aperiodický**

Pro libovolný aperiodický stav $i \in S$ platí:
$$
\lim_{n \rightarrow \infty} \mathbf P_{ii}(n) = \frac{1}{\mu_i}
$$

Pro jakýkoliv jiný stav $j \in S$:
$$
\lim_{n \rightarrow \infty} \mathbf P_{ji}(n) = \frac{f_{ji}}{\mu_i}
$$

Pro **periodický stav** $i \in S$:
$$
\lim_{n \rightarrow \infty} \mathbf P_{ii}(f\cdot d(i)) = \frac{d(i)}{\mu_i}
$$

---

#### Klasifikace stavů pomocí matice přechodu
Stav $i \in S$ je:
* **přechodný:** $\sum_{n=0}^\infty \mathbf P_{ii}(n)< + \infty$
* **trvalý nulový:** $\sum_{n=0}^\infty \mathbf P_{ii}(n) = + \infty \wedge \lim_{n \rightarrow \infty} \mathbf P_{ii}(n) = 0$
* **trvalý nenulový aperiodický:** $\lim_{n \rightarrow \infty} \mathbf P_{ii}(n) = \frac{1}{\mu_i} > 0$
* **trvalý nenulový periodický:** Má periodu $d(i)$ a $\lim_{n \rightarrow \infty} \mathbf P_{ii}(k \cdot d(i)) = \frac{d(i)}{\mu_i} > 0$

---
#### Dosažitelnost

Stav $j$ je **dosažitelný ze stavu** $i$ ($i \rightarrow j$), pokud se lze dostat z $i$ do $j$ v konečném čase: $\exist n \in \N_0: \mathbf P_{ij}(n)>0$

Stavy $i$ a $j$ jsou **vzájemně dosažitelné** ($i \leftrightarrow j$), pokud $i \rightarrow j$ a $j \rightarrow i$ 

Pokud $i \leftrightarrow j$, pak jsou **oba stejného typu**

---

#### Množiny stavů

Množina $C \subseteq S$ je **uzavřená**, pokud $\forall i \in C \forall j \notin C: \mathbf P_{ij} = 0$

Pokud uzavřená množina tvořena jedním stavem, je tento stav **pohlcující (absorpční)**

Množina stavů $C \subseteq S$ je **nerozložitelná (ireducibilní)**, pokud pro všechna $i,j \in C$ platí $i \leftrightarrow j$

Množinu stavů $S$ lze **jednoznačně rozložit** do tvaru $S = T \cup C_1 \cup C_2 \cup...$, kde $T$ je množina všechn přechodných stavů a $C_1, C_2, ...$ jsou vzájemně disjunktní nerozložitelné množiny trvalých stavů

**Matice přechodu po uspořádání stavů:**
Uspořádání: řádek (i sloupec) začíná přechodnými stavy, končí trvalými
$$
\mathbf P = \left(\begin{matrix} \mathbf T & \mathbf R \\ \mathbf 0 & \mathbf C \end{matrix} \right)
$$
Kde:
* $\mathbf T$: čtvercová matice přechodů mezi přechodnými stavy v $T$
* $\mathbf R = \mathbf R_1 \oplus \mathbf R_2 \oplus...$, kde $\mathbf R_i$: matice přechodů z množiny přechodných stavů do množiny trvalých stavů
* $\mathbf C = \mathbf C_1 \oplus \mathbf C_2 \oplus...$, kde $\mathbf C_i$: čtvercová matice přechodů mezi trvalými stavy v $C_i$ 

V řetězci s konečně mnoha stavy **nemohou být všechny přechodné** a **neexistují trvalé nulové**

V končené množině stavů **existuje stacionární rozdělení**

Celkem existuje tolik **lineárně nezávislých** stacionárních rozdělení, kolik existuje nenulových množin $C_r$

**Věta o existenci stacionárního rozdělení:** Pro nerozložitelný markovský řetězec platí:
* Pokud všechny stavy přechodné nebo trvalé nulové, stacionární rozdělení neexistuje
* Pokud všechny stavy trvalé nenulové, stacionární rozdělení existuje a je jediné

---

#### Pravděpodobnost pohlcení

**Čas absorpce:** náhodná veličina $\tau_A: \Omega \rightarrow \{0,1,...,+\infty\}$, kde $\tau_A(\omega) = \min\{n \in \N_0| X_n(\omega) \notin T\}$ pokud množina neprázdná, jinak $\infty$
*(minimální čas kdy se opustí množina přechodných stavů)*

Pravděpodobnost, že **řetězec startující v $i \in T$ opustí $T$ přechodem do $j \in C$:** $\mathbf U_{ij} = P(X_{\tau_A} = j|X_0 = i)$
Matice $\mathbf U = (\mathbf U_{ij})_{i \in T, j \in C}$

**Matice pravděpodobností pohlcení $\mathbf U$** je řešením rovnice $\mathbf U = \mathbf R + \mathbf T \mathbf U$, tedy $\mathbf U = (\mathbf E - \mathbf T)^{-1} \mathbf R$ ($\mathbf E$ je jednotková matice)

**Počet návštěv stavu $j \in S$:** $W_j = \sum_{n=0}^\infty \mathbb 1_{\{X_n = j\}}$

**Střední počet návštěv stavu $j \in S$**, když řetězec startuje v $i$: $\mathbf N_{ij} = E(W_j| X_0 = i)$

Matici $\mathbf N$ je **fundamentální matice řetězce** a platí: $\mathbf N = (\mathbf E - \mathbf T)^{-1}$
Potom: $\mathbf U = \mathbf N \mathbf R$

---

#### Limita matice $\mathbf C^n$

Struktura matice $\mathbf C$:
$$
\mathbf C = \left( \begin{matrix} \mathbf C_1 & \mathbf 0 & ... \\ \mathbf 0 & \mathbf C_2 & ... \\ \vdots & \vdots  & \ddots \end{matrix} \right)
$$

Potom:
$$
\mathbf C^n = \left( \begin{matrix} \mathbf C_1^n & \mathbf 0 & ... \\ \mathbf 0 & \mathbf C_2^n & ... \\ \vdots & \vdots  & \ddots \end{matrix} \right)
$$

Pokud všechny trvalé stavy **aperiodické:**
$$
\mathbf C^n \xrightarrow{n \rightarrow \infty} \tilde{\mathbf C} = \left( \begin{matrix} \tilde{\mathbf C_1} & \mathbf 0 & ... \\ \mathbf 0 & \tilde{\mathbf C_2} & ... \\ \vdots & \vdots  & \ddots \end{matrix} \right)
$$
Kde $(\tilde{\mathbf C_r})_{ij} = \tilde{\mathbf \pi}_j^{(r)}$. Matice $\tilde{\mathbf C_r}$ má **v řádcích stacionární rozdělení** pod-řetězce $C_r$

---

#### Limita matice $\mathbf P^n$

Pokud $S = T \cup C$ končená množina stavů, $C$ trvalé aperiodické, potom:
$$
\lim_{n \rightarrow \infty} \mathbf P^n = \lim_{n \rightarrow \infty} \left(\begin{matrix} \mathbf T^n & \mathbf R_n \\ \mathbf 0 & \mathbf C^n \end{matrix} \right) = \left(\begin{matrix} \mathbf 0 & \mathbf U \tilde{\mathbf C} \\ \mathbf 0 & \tilde{\mathbf C} \end{matrix} \right)
$$

---

#### Odhad matice přechodu

**Maximálně věrohodným odhadem** matice přechodu $\mathbf P$ je matice $\hat{\mathbf P}$ s prvky
$$
\hat{\mathbf P}_{ij} = \frac{n_{ij}}{n_{i\bullet}}
$$
Kde $n_{ij}$ počet přechodů z $i$ do $j$ a $n_{i\bullet} = \sum_{j \in S}n_{ij}$

Odhad metodou maximální věrohodnoti je **konzistentní:** $\hat{\mathbf P}_{ij} \xrightarrow{\text{skoro jistě}} \mathbf P_{ij}$ při $n \rightarrow \infty$
