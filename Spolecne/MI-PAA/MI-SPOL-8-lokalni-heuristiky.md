# MI-SPOL-8	
**Princip lokálních heuristik, pojem globálního a lokálního minima, obrana před uváznutím v lokálním minimu.**

---

**Princip globálních metod:** řešení zadané instance je konstruováno z řešení dílčích instancí

**Princip lokálních metod:** Věnuje se jedné aktuální konfiguraci a vybírá se příští z jejích sousedů

---

#### Stavový prostor

**Stav algoritmu:** 
$X = \{x_1, x_2, ..., x_n\}$ konfigurační proměnné problému $\Pi$
$Z = \{z_1, z_2, ..., z_m\}$ vnitřní proměnné algoritmu $A$ řešícího instanci $I$ problému $\Pi$
Každé ohodnocení $s$ proměnných $X \cup Z$ je **stav algoritmu $A$ řešícího $I$**

**Stavový prostor:**
$S = \{s_I\}$ množina všech stavů algoritmu $A$ řešícího $I$
$Q = \{q_J\}$ množina operátorů $S\rightarrow S$ t.ž. $\forall s_I,q_J: q_J(s_I) \neq s_I$
Dvojice $(S,Q)$ je **stavový prostor algoritmu $A$ řešícího $I$**

Nechť $S \in S$ stav a $q \in Q$ operátor. Aplikace $q$ na $s$ je **akce**.

Nechť $(S,Q)$ staovvý prostor algoritmu řešícího instanci problému. Pak se orientovaný graf $H = (S,E)$, kde hrana $(e_I, e_J) \in E$ odpovídá akci $s_J = q(s_I)$ pro $q \in Q$, nazývá **grafem stavového prostoru algoritmu**.

**Okolí stavu $s \in S$:** množina stavů dosažitelných z $s$ aplikací některé operace $q \in Q$

**$k$-okolí stavu $s \in S$:** množina stavů dosažitelných z $s$ aplikací nejméně jedné a nejvýše $k$ operací $q \in Q$

Stavy z okolí $s \in S$ jsou **sousední stavy** stavu $s$.

Příklad: Hamiltonova kružnice v grafu $G$:
* jedna konfigurace = podgraf $G$
* uzel stavového prostoru = podgraf $G$
* operátor = např. dvojzáměna na hranách

![](stp.png)

---

#### Prohledávací prostor
Ve stavovém prostoru co stav, co jedna aktuální konfigurace: $(000), (010), ...$

V **prohledávacím prostoru** se začíná od "nic nevím": $(???), (??0), ...$

---

#### Pohyb stavovým prostorem

**Aktuální stav:** konfigurace příslušející aktuálnímu stavu

**Transformace** aktuálního stavu pomocí operátorů (pohyb)
Nutno řídit: **strategie** prohledávání

**Úplná strategie:** navštívit všechny stavy kromě těch, o kterýmch víme, že nedávají (optimální) řešení

**Systematická strategie:** úplná, ale navštívit každý stav nejvýše jednou
Vlastnosti:
* nejhorší případ = hrubá síla
    * nastane i pokud neexistuje řešení
* řešení existuje $\Rightarrow$ je nalezeno
* nalezne optimální řešení

**Lokální metody:**
* **Pouze nejlepší:** jako následující stav je zvolen nejlepší ze sousedních (pokud je lepší než aktuální).
Pořadí procházení neovlivní výsledek.
* **První zlepšení:** Následující stav je první, který je lepší než aktuální.
Pořadí procházení ovlivní výsledek -- nutno randomizovat

**Prořezávání:** Cesty prohledávání, které nevedou na validní nebo optimální řešení nejsou prohledávány

---

#### Pohyb v prohledávacím prostoru
* typicky ne úplné ani systematické strategie
* krok prohledávání: vyber proměnnou, vyber její hodnotu
* možnost odvolat nastavení proměnné

---

**Globální minimum:** optimální řešení instance, žádný ze stavů není lepší

**Lokální minimum:** Všechny jeho souední stavy mají horší hodnotu optimalizačního kritéria.

**Únik z lokálních minim** -- balanc mezi:
* **diverzifikace:** rovnoměrný průzkum stavového prostoru *(ochota připustit akci vedoucí k horšímu řešení)*
* **intenzifikace:** konverence k finálnímu řešení *(neochota připouštět horší řešení)*