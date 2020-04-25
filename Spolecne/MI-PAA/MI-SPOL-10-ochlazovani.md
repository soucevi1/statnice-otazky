# MI-SPOL-10	
**Princip simulovaného ochlazování, význam parametrů a způsoby jejich řízení.**

---

#### Analogie

* stav systému = řešení
* změna stavu = přechod k sousednímu řešení
* energie systému = optimalizační kritérium
* krystalický stav = heuristické řešení
* kinetická energie molekul = ochota přechodu do horšího stavu
* teplota = řídící patametr

---

#### Princip
Při výběru násleudjícího stavu:
* Zvol náhodně souseda
* Pokud je lepší, přijmi ho
* Pokud ne, přijmi jej s pravděpodobností závislou na zhoršení a parametru (teplotě)

```python
T = počáteční teplota
best = null
while not frozen(T,...):
    while not equilibrium(...):
        state = try(state)
        if state.better(best):
            best = state
    T = cool(T, ...)
```

Průběh teploty (**rozvrh ochlazování**) určen funkcemi `frozen`, `equilibrium` a `cool`.

```python
def try(state):
    q = Q.random_choose()
    new = q(state)
    if new.better(state):
        return new
    d = new.cost() - state.cost() # minimalizační problém
    if random(0,1) < exp(-d/T):
        return new
    return current
```

**Zhoršení:**

Pravděpodobnost, že nový bude přijat, je $10^{-d/T}$

* $d \rightarrow 0 \Rightarrow p_{new} \rightarrow 1$ (nepatrné zhoršení přijato častěji)
* $d \rightarrow \infty \Rightarrow p_{new} \rightarrow 0$ (velké zhoršení přijato zřídka)
* $T \rightarrow 0 \Rightarrow p_{new} \rightarrow 0$ (při nízké teplotě zhoršení přijímána zřídka)
* $T \rightarrow \infty \Rightarrow p_{new} \rightarrow 1$ (při vysoké teplotě přijata i velká zhoršení)

**Počáteční stav:** řešení z jiné heuristiky, náhodné řešení

**Vysoké teploty:** velká pravděpodobnost přijetí horšího řešení, převaha diverzifikace

**Nízké teploty:** konvergence k minimu, intenzifikace

---

#### Rozvrh ochlazování

**Funkce `cool`:** změna teploty, např. `T = a*T`, kde `a`$\in (0,1)$

**Funkce `equilibrium`:** povný počet kroků, $N$ přijatých stavů, ...

**Počáteční teplota:**
Známá hloubka lokálních minim $\Rightarrow$ nastavení tepltoy tak, aby pravděpodobnost úniku z minima byla např. 50 %.
Zpětnovazební řízení: zvyšování teploty, sledování četnosti přijatých změn

**Funkce `frozen`:** četnost změn (jakýchkoliv/k lepšímu) klesla pod danou mez, pevná mez teploty

---

#### Omezující podmínky

* **Relaxace:** 
    * Konfigurace, která není řešením, má mnohem horší `cost` než libovolné řešení
        * konvergence vždy k řešení
    * Konfigurace, která není řešením, může mít stejný `cost` jako nějaké řešení
        * lepší vlastnosti stavového prostoru, možná konvergence k ne-řešení
* **Zahození kandidátní konfigurace**
* **Oprava kandidátní konfigurace**