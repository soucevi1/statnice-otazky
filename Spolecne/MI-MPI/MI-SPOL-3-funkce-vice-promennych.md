# MI-SPOL-3	
**Funkce více proměnných: gradient, Hessián, definitnost matic, extrémy funkcí více proměnných bez omezení a s rovnostními omezeními.**

---

**Norma** na vektorovém prostoru $V$ (nad $\R$ nebo $\mathbb{C}$) je zobrazení $||\cdot ||: V \rightarrow \R_0^+$ splňující $\forall \mathbf x, \mathbf y \in V, \alpha$:
* $||\mathbf x|| = 0 \Rightarrow \mathbf x = 0$
* $|| \alpha \mathbf x|| = |\alpha|\cdot ||\mathbf x ||$
* $||\mathbf x + \mathbf y|| \leq ||\mathbf x|| + || \mathbf y||$ (trojúhelníková nerovnost)

Příklad: 
* Eukleidovská norma: $||\mathbf x||_2 = \sqrt{\sum_{i=1}^n |x_i|^2}$
* Maximová: $||\mathbf x||_\infty = \max\{|x_i|\}, i \in \{1,...,n\}$
* Součtová: $||\mathbf x||_1 = \sum_{i=1}^n |x_i|$

---

**Reálná funkce více reálných proměnných** je zobrazení $D_f \rightarrow \R$ pro $D_f \subset \R^n$
* $D_f$ je definiční obor
* $f(D_f)$ je obor hodnot

Pro $\mathbf x \in \R^n$ a $\delta \in \R^+$ je **$\delta$-okolí bodu $\mathbf x$** množina $H_\delta(\mathbf x) = \{\mathbf b \in \R^n: ||\mathbf x - \mathbf b|| < \delta\}$

Množina $M \subset \R^n$. Bod $\mathbf x \in \R^n$ je **hromadným bodem $M$**, pokud pro všechna $r>0$ platí $H_r(\mathbf x) \setminus \{\mathbf x\} \cap M \neq \emptyset $ 
Bod, který není hromadný, je **izolovaný**

Funkce $f: D_f \rightarrow \R, D_f \subset \R^n$, má **limitu $L\in \bar{\R}$ v hromadném bodě $\mathbf b$ množiny $D_f$**, pokud:
$$ \forall H(L) \exist H(\mathbf b) \forall x \in D_f \setminus \{\mathbf b\}: \mathbf x \in H(\mathbf b) \Rightarrow f(\mathbf x) \in H(L) $$
Značení: $\lim_{x\rightarrow b}{f(x)} = L$

Funkce $f: D_f \rightarrow \R, D_f \subset \R^n$ je **spojitá v bodě** $x_0 \in D_f$, pokud $\forall \epsilon > 0 \exist \delta >0 \forall x \in D_f: x \in H_\delta(x_0) \Rightarrow f(x) \in H_\epsilon(f(x_0))$
NEBO: pokud pro všechny neizolované body $x_0 \in D_f$ platí: $\lim_{x\rightarrow x_0} f(x) = f(x_0)$

Funkce je spojitá, pokud je spojitá ve všech bodech.

---

Reálná funkce $f$ má v bodě $\mathbf b \in D_f$:
* **lokální minimum**, pokud $\exist \delta>0, \forall \mathbf x \in H_\delta(\mathbf b), f(\mathbf x) \geq f(\mathbf b)$
* **ostré lokální minimum**, pokud $\exist \delta>0, \forall \mathbf x \in H_\delta(\mathbf b) \setminus \{\mathbf b\}, f(\mathbf x) \gt f(\mathbf b)$
* **globální minimum**, pokud $\forall \mathbf x \in D_f, f(\mathbf x) \geq f(\mathbf b)$

Spojitá funkce obsahuje globální minimum i maximum, pokud je $D_f$:
* omezená (je podmnožinou otevřené koule)
* a uzavřená (obsahuje i svou hranici)

---

**Parciální derivace funkce $f$ ve směru $x_i$ v bodě $\mathbf b=(b_1,b_2,...,b_n) \in D_f$** takovém, že $\exist H(\mathbf b) \subset D_f$, je
$$
\lim_{h\rightarrow 0} \frac{f(b_1,b_2,...,b_i + h,...,b_n) - f(b_1,b_2,...,b_i,...,b_n)}{h} = L
$$
Značení: $\frac{\delta f}{\delta x_i}(\mathbf b) = L$

Jedná se o **směrnici tečny ke grafu funkce $f$ ve směru osy $x_i$**
![](partial_derivative_as_slope.png)

**Gradient funkce $f$ v bodě $\mathbb b \in D_f$** je vektor
$$
\nabla f(\mathbf b) = \left( \frac{\delta f}{\delta x_1}(\mathbf b) \frac{\delta f}{\delta x_2}(\mathbf b), ..., \frac{\delta f}{\delta x_n}(\mathbf b) \right)
$$
Význam: ukazuje směr (v $D_f$) nejvyššího růstu funkce

Nechť $\mathbf v \in \R^{n,1}, ||\mathbf v || = 1$. **Derivace funkce $f$ ve směru $\mathbf v$ v bodě $\mathbf b \in D_f$** takovém, že $\exist H(\mathbf b) \subset D_f$, je
$$
\nabla_{\mathbf v} f(\mathbf b) = \lim_{h\rightarrow 0} \frac{f(\mathbf b + h \mathbf v) - f(\mathbf b)}{h}
$$
Význam: **směrnice tečny ke grafu funkce $f$ ve směru $\mathbf v$**

Pokud v bodě $\mathbf b$ existuje gradient, pak platí $\nabla_{\mathbf v}f(\mathbf b) = \nabla f(\mathbf b) \cdot \mathbf v$

---

**Nutná podmínka lokálního extrému:** Nechť má funkce $f:D_f \rightarrow \R, D_f \subset \R^n$ v bodě $\mathbf b$ parciální derivaci podle i-té proměnné. Pokud $f$ má v bodě $\mathbf b$ lokální extrém, potom $\frac{\delta f}{\delta x_i}(\mathbf b) = 0$
Důsledek: pokud existuje gradient funkce $f$ v bodě $\mathbf b$, pak existence lokálního extrému implikuje $\nabla f(\mathbf b) = 0$

Body $\mathbf b$ splňující $\nabla f(\mathbf b) = 0$ se nazývají **stacionární**.

Stacionární body a body, kde gradient neexistuje, se nazývají **kritické body**.

---

**Parciální derivace druhého řádu**: $$\frac{\delta^2 f }{\delta x_j \delta x_i} (\mathbf b) = \frac{\delta}{\delta x_j} (\frac{\delta f}{\delta x_i}(\mathbf b))$$

Pokud všechny druhé parciální derivace v bodě $\mathbf b$ existují: **Hessova matice**
$$
\nabla^2 f(\mathbf b) = \left(\begin{array}{ccc} 
 \frac{\delta^2 f}{\delta^2 x_1} (\mathbf b) & ... & \frac{\delta^2 f}{\delta x_1 \delta x_n}(\mathbf b)\\
... & & ...\\
\frac{\delta^2 f}{\delta x_n \delta x_1}(\mathbf b)  & ... & \frac{\delta^2 f}{\delta^2 x_n} (\mathbf b)\\
\end{array}\right)
$$

Pokud existuje $\frac{\delta^2 f}{\delta x \delta y} (\mathbf b)$ a funkce $\frac{\delta^2 f}{\delta x \delta y}$ je v $\mathbf b$ spojitá, potom $\frac{\delta^2 f}{\delta y \delta x} (\mathbf b)$ existuje a $\frac{\delta^2 f}{\delta x \delta y} (\mathbf b) = \frac{\delta^2 f}{\delta y \delta x} (\mathbf b)$

---

**Definitnost matic:**
$\mathbf A \in \R^{n,n}$ je
* **pozitivně semidefinitní**, pokud $\mathbf x^T \mathbf A \mathbf x \geq 0$ pro $\forall \mathbf x \in \R^{n,1}$
* **pozitivně definitní**, pokud $\mathbf x^T \mathbf A \mathbf x \gt 0$ pro $\forall \mathbf x \in \R^{n,1}, \mathbf x \neq 0$
* **negativně semidefinitní**, pokud $\mathbf x^T \mathbf A \mathbf x \leq 0$ pro $\forall \mathbf x \in \R^{n,1}$
* **negativně definitní**, pokud $\mathbf x^T \mathbf A \mathbf x \lt 0$ pro $\forall \mathbf x \in \R^{n,1}, \mathbf x \neq 0$
* **indefinitní**, pokud není pozitivně ani negativně semidefinitní: právě když $\exist x,y \in \R^n, \mathbf x^T \mathbf A \mathbf x > 0$ a $\mathbf y^T \mathbf A \mathbf y < 0$

Symetrické matice:
* PSD: všechna vlastní čísla nezáporná
* PD: všechna vlastní čísla kladná
* NSD: všechna vlastní čísla nekladná
* ND: všechna vlastní čísla záporná
* indefinitní: alespoň jedno kladné a alespoň jedno záporné vlastní číslo

**Sylvestrovo kritérium určení definitnosti:**
V *symetrické* matici $\mathbf A \in \R^{n,n}$ se nachází matice $A_1, A_2, ..., A_n$, kde $A_k \in \R^{k,k}$ je čtvercová matice v levém horním rohu matice $\mathbf A$. Potom:
* Matice $\mathbf A$ je pozitivně definitní $\Leftrightarrow$ determinant všech matic $A_1,...,A_n$ kladný
* Matice $\mathbf A$ je negativně definitní $\Leftrightarrow$ determinant matic $A_k$ záporný pro lichá $k$ a kladný pro sudá

Pokud má čtvercová matice na diagonále dva prvky s různým znaménkem, pak je **indefinitní**

---

Stacionární bod, který není minimem ani maximem, na jehož okolí má $f$ spojité všechny parciální derivace, je **sedlový bod**

**Postačující podmínka existence extrému a sedlového bodu:**
$\mathbf b \in D_f$ stacionární bod funkce $f:D_f \rightarrow \R, D_f \subset \R^n$
Existuje okolí $H(\mathbf b) \subset D_f$ t.ž. $f$ má na něm spojité všechny druhé  parciální derivace, potom:
* pokud $\nabla^2 f(\mathbf b)$ pozitivně definitní, pak $\mathbf b$ je ostré lokální minimum
* pokud $\nabla^2 f(\mathbf b)$ negativně definitní, pak $\mathbf b$ je ostré lokální maximum
* pokud $\nabla^2 f(\mathbf b)$ indefinitní, pak $\mathbf b$ je sedlový bod

**Nutná podmínka existence lokálního extrému:**
* pokud $\mathbf b$ je lokální minimum, pak $\nabla^2 f(\mathbf b)$ je pozitivně definitní
* pokud $\mathbf b$ je lokální maximum, pak $\nabla^2 f(\mathbf b)$ je negativně definitní


Funkce se spojitými druhými parciálními derivacemi **konvexní**, právě když je její Hessián PSD ve všech bodech vnitřku $D_f$


---

#### Kuchařka na hledání extrémů
* najít podezřelé (kritické) body (body, kde neexistuje aspoň jedna parciální derivace, nebo kde gradient je 0)
* najít Hessián v podezřelém bodě -- pokud je:
    * PD, pak bod je ostré lokální minimum
    * ND, pak bod je ostré lokální maximum
    * IND, pak je sedlovým bodem

---

#### Vázané extrémy s rovnostními omezeními

Úloha vázaného extrému s rovnostními omezeními je minimalizování $f(x)$ za podmínek $g_j(x) = 0, j \in \hat m$, kde $f,g$ jsou funkce $D \rightarrow \R, D \subset \R^n$

 **Přípustná řešení:**
 $M = \{x \in \R^n: (\forall j \in \hat m)(g_j(x)=0)\}$
 (množina řešení, kde jsou splněny podmínky)

 Funkce $L: M \times \R^m \rightarrow \R$ definovaná jako
 $$
L(x;\lambda) = f(x) + \sum_{j=1}^m \lambda_jg_j(x)
 $$

 je **Lagrangeova funkce**.
 Koeficienty $\lambda = (\lambda_1, ..., \lambda_m)$  jsou **Lagrangeovy multiplikátory**

#### Postačující podmínka existence ostrého lokálního minima při rovnostních omezeních
Nechť $f, g_j, j \in \hat m$ mají spojité všechny druhé parciální derivace na nějaké otevřené nadmnožině $M$. Pokud dvojice $(x^*, \lambda^*) \in M \times \R^m$ splňuje následující podmínky, potom je $x^*$ bodem ostrého lokálního minima
Podmínky:
* *(optimalita)* $\forall i, \frac{\delta L}{\delta x_i} (x^*, \lambda^*)=0$ (nulový gradient Lagrangeovy funkce podle $x$)
* *(podmínka 2. řádu)* pro každý vektor $0 \neq z \in \R^n$ splňující 
$z^T \nabla g_j(x^*)= 0 (\forall j \in \hat m)$
platí 
$z^T \nabla^2_x L(x^*;\lambda^*) z > 0$ (PD Hessián za určitých podmínek).
