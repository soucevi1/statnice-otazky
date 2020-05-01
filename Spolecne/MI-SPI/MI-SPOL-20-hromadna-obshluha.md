# MI-SPOL-20
**Systémy hromadné obsluhy a jejich limitní vlastnosti. Souvislost s Markovskými řetězci se spojitým časem.**

---
#### Exponenciální závody 
![](fr.png)
Frontě běží exponenciální hodiny $T$ (časy příchodu požadavků), serveru běží exponenciální hodiny $S$ (zpracování požadavku) -- **exponenciální závody**

Pokud $T \sim \text{Exp}(\lambda)$ a $S \sim \text{Exp}(\mu)$ **nezávislé**, pak $Z := \min\{T,S\} \sim \text{Exp}(\lambda + \mu)$

**Vítez exponenciálních závodů:** Pokud $T \sim \text{Exp}(\lambda)$ a $S \sim \text{Exp}(\mu)$ **nezávislé**, pak
$$
P(T< S) = \frac{\lambda}{\lambda + \mu}
$$

Proces $\{X_t|t \geq 0\}$ je **markovský řetězec se spojitým časem**, právě když mezi jednotlivými stavy probíhají exponenciální závody

---

#### Model hromadné obsluhy
![](hr.png)
* $\lambda$: **intenzita příchodů** 
* $A_i$: náhodný čas mezi příchodem (i-1)-ího a $i$-tého zákazníka 
$A_i \sim F_A$
$EA_i = 1/\lambda$
* $\mu$: **intenzita obsluhy jednoho serveru**
* $S_j$: čas obsluhy jednoho zákazníka
$S_j \sim F_S$
$ES_j = 1/\mu$
* Veličiny $A_1, A_2, ..., S_1, S_2, ...$ **nezávislé**
* Server obsahuje $c$ nezávislých obslužných míst $\Rightarrow$ intenzita obsluhy je nejvýše $c\mu$

---

#### Proces hromadné obsluhy
**Proces hromadné obsluhy:** proces $\mathbf X = \{X_t|t \geq 0\}$, který zaznamenává **počet zákazníků v systému** hromadné obsluhy v čase $t$

Ukazatel $\rho = \frac{\lambda}{c\mu}$:
* $\rho > 1$: počet zákazníků v systému poroste nad všechny meze
* $\rho < 1$: ustálení sysétmu n stabilním rovnovážném rozdělení

**Kendallova notace:** $A|S|c|K|N|D$
$A$ - rozdělení časů příchodu $F_A$
$S$ - rozdělení časů obsluhy $F_S$
$c$ - počet obslužných míst
$K$ - kapacita systému (default $\infty$)
$N$ - velikost populace (default $\infty$)
$D$ - typ obsluhy (default FIFO)

Značení rozdělení $A$ a $S$:
* $M, M(\lambda)$ - exponenciální rozdělení (markovské)
* $D, D(d)$ - degenerované rozdělení, soustředěné v hodnotě $d$
* $G$ - obecné rozdělení

---

#### Systém $M|M|1$
**Proces zrodu a zániku** s parametry:
$\lambda_n = \lambda, n \in \N_0$
$\mu_m = \mu, m \in \N$

**Matice intenzit:**
$$
\mathbf Q = \left( \begin{matrix} 
-\lambda & \lambda & 0 & 0 & \dots \\ 
\mu & -(\lambda + \mu) & \lambda & 0 & \dots \\
0 & \mu & -(\lambda + \mu) & \lambda & \dots \\
0 & 0 & \ddots & \ddots & \ddots
\end{matrix} \right)
$$

**Stacionární rozdělení:**
* Pokud $\rho < 1$, existuje jednoznačné stacionární rozdělení $\mathbf \pi$ a pro všechna $n \in \N_0$ platí
$$
P(X_t = n) \rightarrow \mathbf \pi_n = (1-\rho)\rho^n
$$
* Pokud $\rho \geq 1$, stacionární rozdělení neexistuje a pro všechna $n \in \N_0$ platí
$$
P(X_t = n) \rightarrow 0
$$

**Stacionární vlastnosti:**
Předpoklad: $\rho = \frac{\lambda}{\mu} <1$ a systém je ve stacionárním stavu.
* **Střední počet zákazníků v systému:** $EN := E_{\mathbf \pi} X_t$
Platí, že
$$
EN = \sum_{n=0}^\infty n \mathbf \pi_n = \frac{\rho}{1-\rho}
$$
* $EN = EN_s + EN_f$ *(server + fronta)*
* $EN_s = 1-\mathbf \pi_0 = \rho$
* $EN_f = EN-EN_s = \frac{\rho^2}{1-\rho}$

**Doba čekání ve frontě:** $W$
* Zákazník **nečeká,** pouze pokud je **server prázdný:** 
$P(W=0) = P(X_t = 0) = \mathbf \pi_0 = 1-\rho = 1-\frac{\lambda}{\mu}$
* V době příchodu je v **systému $n > 0$ zákazníků:**
$W$ je součet $n$ exponenciálně rozdělených nezávislých veličin s parametrem $\mu$
$$
(W|W>0) \sim \text{Exp}(\mu-\lambda) \Rightarrow P(W>s) = \rho e^{-(\mu-\lambda)s}
$$

---

#### Systém $M|M|\infty$

Nekonečně obslužných míst -- každý zákazník **okamžitě obsloužen**

Proces zrodu a zániku s parametry:
$\mathbf Q_{n, n+1} = \lambda_n \equiv \lambda$
$\mathbf Q_{n, n-1} = \mu_n = n \mu$

**Matice intenzit:**
$$
\mathbf Q = \left( \begin{matrix} 
-\lambda & \lambda & 0 & 0 & \dots \\ 
\mu & -(\lambda + \mu) & \lambda & 0 & \dots \\
0 & 2\mu & -(\lambda + 2\mu) & \lambda & \dots \\
0 & 0 & \ddots & \ddots & \ddots
\end{matrix} \right)
$$

**Podmínka detailní rovnováhy** pro $n \in \N$: 
$n \mu \mathbf \pi_n = \lambda\mathbf \pi_{n-1}$
$\Rightarrow \mathbf \pi_n = \frac{\lambda}{n\mu}\mathbf \pi_{n-1} = \frac{1}{n!} \left(\frac{\lambda}{\mu}\right)^n \mathbf \pi_0$

**Stacionární rozdělení:** Poissonovo s parametrem $\frac{\lambda}{\mu}$:
$$
P_{\mathbf \pi}(X_t = n) = \mathbf \pi_n = \frac{1}{n!} \left(\frac{\lambda}{\mu}\right)^n e^{-\frac{\lambda}{\mu}}
$$

---

#### Systém $M|M|c$
Server má $1 < c < \infty$ obslužných míst -- pokud všechna **obsazena,** zákazník jde do **fronty**

Proces zrodu a zániku s intenzitami:
$\mathbf Q_{n, n+1} = \lambda_n \equiv \lambda$
$\mathbf Q_{n, n-1} = \mu_n = \min\{c,n\}\cdot \mu$

**Matice intenzit:**
$$
\mathbf Q = \left( \begin{matrix} 
-\lambda & \lambda & 0 & 0 & \dots & 0 & 0 & \dots\\ 
\mu & -(\lambda + \mu) & \lambda & 0 & \dots & 0 & 0 & \dots \\
0 & 2\mu & -(\lambda + 2\mu) & \lambda & \dots & 0 & 0 & \dots \\
\vdots & \vdots & \ddots & \ddots & \ddots & \vdots & \vdots & \dots\\
0 & 0 & 0 & c\mu & -(\lambda + c\mu) & \lambda & 0 & \dots \\
0 & 0 & 0  & 0 & c\mu & -(\lambda + c\mu) & \lambda & \dots \\
0 & 0 & 0 & 0 & 0 & \ddots & \ddots & \ddots \\
\end{matrix} \right)
$$

**Stacionární rozdělení:**
Pokud $\rho < 1$:
$$
\mathbf \pi_n = \begin{cases} 
\frac{1}{n!} \left(\frac{\lambda}{\mu}\right)^n \mathbf \pi_0 & n \leq c \\
\frac{c^c}{c!} \left(\frac{\lambda}{c\mu}\right)^n \mathbf \pi_0 & n > c \\
\end{cases} 
$$
Jinak psáno:
$$
\mathbf \pi_n = \left(\frac{\lambda}{\mu}\right)^n \frac{1}{\Pi_{k=1}^n \min\{k,c\}} \mathbf \pi_0
$$

Pokud $\rho \geq 1$: stacionární rozdělení neexistuje

**Proces odchodů:**
* Pokud $M|M|c$ ce stacionárním stavu ($\lambda < c\mu$), pak proces odchodů (**počet obsloužených do času $t$**) je Poissonův proces s intenzitou $\lambda$

---

#### Littleho věta

Buď $\{X_t|t \geq 0\}$ striktně stacionární proces hromadné obsluhy. Buďte dále:
* $EN$ - střední počet zákazníků v systému
* $ET$ - střední doba strávená zákazníkem v systému
* $\lambda$ - intenzita příchodů

Jsou-li všechny střední hodnoty konečné, pak 
$$
EN = \lambda \cdot ET
$$

---

#### Systém $G|G|1$
Obecné rozdělení příchodů i obsluhy

**Doba strávená $k$-tým zákazníkem v systému:** 
$T_k = W_k + S_k$, 
kde $W_k$ - doba čekání ve frontě, $S_k$ - doba obsluhy

**Littleho věta:**
Celý sysétm: $EN = \lambda ET_k = \lambda EW_k + \lambda ES_k$
Samotná fronta: $EN_f = \lambda EW_k$

Protože $EN = EN_f + (1-\mathbf \pi_0)$:
$$
\mathbf \pi_0 = 1 - (EN-EN_f) = 1-\lambda (ET_k -EW_k) = 1-\lambda ES_k = 1-\frac{\lambda}{\mu}
$$

---

#### Dva servery $M|M|1$ v sérii

**Stav systému:** vektor $(n_1, n_2) \in \N^2_0$ (počet zákazníků na prvním a druhém serveru)

Ve stacionárním stavu:
$$
P_{\mathbf \pi}(X_t^1 = n_1) = \left( \frac{\lambda}{\mu_1} \right)^{n_1}\left( 1 - \frac{\lambda}{\mu_1} \right)
$$
$$
P_{\mathbf \pi}(X_t^2 = n_2) = \left( \frac{\lambda}{\mu_2} \right)^{n_2}\left( 1 - \frac{\lambda}{\mu_2} \right)
$$

Pro servery $M|M|1$ v rovnovážnném stavu platí, že **proces odchodů** a **proces zaznamenávající počet zákazníků** v sysétmu jsou **nezávislé**
Sdružené stacionární rozdělení potom je:
$$
P(X_t^1 = n_1, X_t^2 = n_2) = \left( \frac{\lambda}{\mu_1} \right)^{n_1}\left( 1 - \frac{\lambda}{\mu_1} \right) \left( \frac{\lambda}{\mu_2} \right)^{n_2}\left( 1 - \frac{\lambda}{\mu_2} \right)
$$

---
