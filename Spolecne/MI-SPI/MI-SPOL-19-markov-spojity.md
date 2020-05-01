# MI-SPOL-19
**Markovské řetězce se spojitým časem. Souvislost s Markovskými řetezci s diskrétním časem a s Poissonovým procesem.**

---

#### Poissonův proces

Náhodný proces $\{N_t | t \geq 0\}$ je **čítací proces**, pokud jsou jeho trajektorie nezáporné, celočíselné a neklesající, tj:
* $N_t \geq 0$
* $N_t \in \Z$
* $s \leq t \Rightarrow N_s \leq N_t$

Pro $s < t$ udává $N_t-N_s$ počet událostí, které nastaly během časového intervalu $(s,t]$

**Binomický proces:** čítací proces takový, že časy mezi událostmi nezávislé, geometricky rozdělené

**Poissonův proces:** čítací proces s nezávislými exponenciálně rozdělenými časy mezi událostmi
**Definice:** $\{X_j|j \in \N\}$ i.i.d náhodné vličiny s rozdělením $\text{Exp}(\lambda)$. Definujeme $\{T_n|n \in \N\}$:
$$
T_n = T_{n-1} + X_n = \sum_{j=1}^nX_j
$$
kde $n \geq 1, T_0 = 0$
Náhodný proces $\{N_t|t\in [0, \infty)\}$, kde 
$$
N_t(\omega) = \max \{n \in \N_0 | T_n(\omega) \leq t\}
$$
je **Poissonův proces**
![](poitr.png)

**Ekvivalentní definice:**
Proces $\{N_t|t \in [0,\infty)\}$ je Poissonův, pokud:
* $N_0 = 0$ skoro jistě
* $N_t - N_s \sim \text{Poisson}(\lambda(t-s))$ pro všechna $t > s \geq 0$
* $\{N_t\}$ má nezávislé přírůstky

---

#### Exponenciální rozdělení
$T \sim \text{Exp}(\lambda)$
* **hustota pravděpodobnosti:** $f_T(t) = \lambda e^{-\lambda t}$ pro $t \geq 0$
* **distribuční funkce:** $F_T(t) = 1-e^{-\lambda t}$ pro $t \geq 0$
* **funkce přežití:** $P(T>t) = e^{-\lambda t}$ pro $t \geq 0$
* **Momenty:** $ET = \frac{1}{\lambda}$, $varT = \frac{1}{\lambda^2}$

**Bezpaměťovost exponenciálního rozdělení:** Pokud $T \sim \text{Exp}(\lambda)$, pak pro všechna $t,s \geq 0$:
$$
P(T> t+s | T>t) = P(T>s)
$$

**Silná bezpaměťovost exponenciálního rozdělení:** Pokud $T \sim \text{Exp}(\lambda)$ a $A$ spojitá nezáporná náhodná veličina nezávislá na $T$, pak pro všechna $s \geq 0$:
$$
P(T> A+s | T>A) = P(T>s)
$$

---

#### Markovský řetězec se spojitým časem

Náhodný proces $\{X_t | t \geq 0\}$ s nejvýše spočetnou množinou stavů $S$ je **markovský řetězec se spojitým časem**, pokud splňuje **markovskou podmínku:** $\forall k \in \N, \forall 0\leq t_0 < t_1 < ... < t_k \in \R_0^+, \forall s_0, ..., s_k \in S$ platí
$$
P(X_{t_k} = s_k | X_{t_{k-1}} = s_{k-1}, ..., X_{t_0} = s_0) = P(X_{t_k} = s_k | X_{t_{k-1}} = s_{k-1})
$$

**Rozdělení v čase $t \in [0, \infty)$** pro $i \in S$: 
$$
\mathbf p_i(t) = P(X_t = i)$$ $$\mathbf p(t) = \left( \mathbf p_1(t), \mathbf p_2(t),... \right)$$

**Matice pravděpodobností přechodu** za čas mezi $s$ a $t\leq s$:
$$
\mathbf P_{ij}(t,s) = P(X_s = j| X_t = i)
$$
$$
\mathbf P(t,s) = \left(\mathbf P_{ij}(t,s)\right)_{i,j \in S}
$$

Náhodný proces $\{X_t| t\geq 0\}$ s nejvýše početnou množinou stavů $S$ je markovský právě když $\forall k \in \N, \forall 0\leq t_0 < t_1< ... < t_k, \forall s_0, ..., s_k \in S$ platí:
$$
P(X_{t_0} = s_0, ..., X_{t_k} = s_k) = \mathbf p_{s_0}(t_0)\cdot \mathbf P_{s_0s_1}(t_0,t_1) \cdot ... \cdot \mathbf P_{s_{k-1}s_k}(t_{k-1},t_k)
$$

**Chapman-Kolmogorova věta:** Pro matice přechodu markovského řetězce platí $\forall t \leq s \leq r \in \N_0$:
$$
\mathbf P(t,r) = \mathbf P(t,s) \cdot \mathbf P(s,r)
$$

---

#### Homogenní markovský řetězec
MArkovský řetězec $\{X_t|t geq 0\}$ je **homogenní**, pokud $\forall t, s \geq 0$:
$$
\mathbf P(t, t+s) = \mathbf P(0,s) := \mathbf P(s)
$$

---

#### Matice skokových intenzit

**Matice skokových intenzit:** Pokud pro všechna $i,j \in S$ existují konečné limity
$$
\mathbf Q_{ii} = \lim_{h \rightarrow 0+}\frac{\mathbf P_{ii}(h)-1}{h}
$$ 
$$
\mathbf Q_{ij} = \lim_{h \rightarrow 0+}\frac{\mathbf P_{ij}(h)}{h}
$$
Je matice $\mathbf Q = (\mathbf Q_{ij})_{i,j \in S}$ **maticí skokových intenzit.** 

$$
\mathbf Q = \frac{d}{dt}\bigg\rvert_{t = 0} \mathbf P(t) = \mathbf P'(0)
$$

**Vlastnosti:**
* $\mathbf Q_{ii} \leq 0$, $\mathbf Q_{i,j}\geq 0$ pro  $i \neq j$
* $\mathbf Q_{ii} = - \sum_{j \neq i}\mathbf Q_{ij}$
* $\mathbf P_{ij}(h) = \mathbf Q_{ij}\cdot h + o(h)$

---

#### Spojitý řetězec jako diskrétní řetězec časovaný Poissonem

Homogenní markovský řetězec se spojitým časem $X_t$ s maticí intenzit $\mathbf Q$.
Existuje ekvivaltentní vyjádření $X_t$ jako:
$$
X_t = Y_{N_t}
$$
kde $\{N_t\}$ a ${Y_n}$ jsou nezávislé procesy:
* $\{N_t|T \geq 0\}$ je **Poissonův proces** s intenzitou $\lambda_M$
* $\{Y_n|n \in \N_0\}$ je **homogenní markovský řetězec s diskrétním časem** a maticí přechodu $\mathbf D$, kde 
$$
\mathbf D = \frac{1}{\lambda_M}\mathbf Q + \mathbf E
$$

**Simulace trajektorie $X_t$:**
* Začátek v náhodném $i \in S$
* Vygenerovat náhodný čas $\tau_i \sim \text{Exp}(\lambda_M)$, kde $\lambda_M = \sup_{i \in S}(-\mathbf Q_{ii})$
* "Posunout hodiny" o $\tau_i$: nastavit $\forall s \in [t, t+\tau_i): X_s = X_t$ 
* Krok v diskrétním řetězci: $Y_n \rightarrow Y_{n+1}$
* $X_{t+\tau_i} = Y_{n+1}$
* $t = t+\tau_i$, 
$n = n+1$

---
#### Stacionární rozdělení

**Kolmogorova dopředná rovnice:** $\mathbf P'(t) = \mathbf P(t) \cdot \mathbf Q$
**Kolmogorova zpětná rovnice:** $\mathbf P'(t) = \mathbf Q \cdot \mathbf P(t)$

**Rozdělení $\mathbf p(t)$** je řešením soustavy diferenciálních rovnic $\mathbf p'(t) = \mathbf p(t)\mathbf Q, \mathbf p(0) = \mathbf p_{initial}$

${X_t|t \geq 0}$ markovský řetězec s pravděpodobnostmi přechodu $\mathbf P(t)$. Vektor $\mathbf \pi$ je **stacionární rozdělení**, pokud pro všechna $t \geq 0$:
$$
\mathbf \pi \mathbf P(t) = \mathbf \pi
$$
$\Rightarrow$ Vektor $\mathbf \pi $ je stacionární rozdělení, právě když 
$$
\mathbf \pi \mathbf Q = \mathbf 0
$$

Markovský řetězec **nerozložitelný**, pokud se z každého stavu $i \in S$ mohu dostat do libovolného stavu $j \in S$ v konečně mnoha krocích

Existuje-li stacionární rozdělení $\mathbf \pi$, pak je **jednoznačné** a pro všechna $i,j \in S$: 
$\lim_{t \rightarrow \infty}P_{ij}(t) = \mathbf \pi_j$
Pokud stacionární rozdělení neexistuje, pak pro všechna $i,j \in S$:
$\lim_{t \rightarrow \infty} P_{ij}(t) = 0$

Množina stavů $S$ **končená** $\Rightarrow$ stacionární rozdělení **existuje**

Pokud rozdělení $\mathbf \pi$ splňuje **detailní rovnováhu**: $\forall i \neq j \in S$:
$$
\mathbf \pi_j \mathbf Q_{ji} = \mathbf \pi_i \mathbf Q_{ij}
$$
pak je stacionárním rozdělením