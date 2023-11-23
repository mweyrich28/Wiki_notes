# Potenzreihen
:potenzreihen:konvergenz_radius:kriterium:leibnizkriterium:harmonische_reihe:geometrische_reihe:

## Reihen Einführung (Renate)
*Kriterien:*

- Worum geht es:
	- 1m + 50cm + 25cm + 12,5cm + ... wird niemals 2m erreichen! So gibt es Reihen mit Reihengliedern > 1, welche trotzdem konvergieren und nicht divergieren
	- Zahlen müsse "schnell" genug kleinwerden, sonst divergiert die Reihe:
		- $\sum_{n = 1}^{\infty} \frac{1}{n} = \infty \text{ aber  } \sum_{n = 1}^{\infty} 1//2^{n} \text{ konvergiert }$
		- Mit Quotientenkriterium: $\frac{ \frac{1}{2^{n+1}} }{ \frac{1}{2^{n}} } \iff \frac{1}{2^{n+1}} \cdot  \frac{2^{n}}{1} \text{ da  } \lim_{n \to \infty} (\underbrace{\frac{1}{2}}_{\text{ < 1 }} )^{n+1} = 0  \text{ so konvergiert das Produkt, also auch die Reihe }$

## Potenzreihen
Sei $\emptyset \neq M \subseteq f_h: M \to \mathbb{K}$

(a) $\sum_{j = 1}^{\infty} f_j \text{ konvergiert gleichmäßig gegen }  f \text{ gdw. alle}  \sum_{j = n + 1}^{\infty} f_j(z) \text{ konvergent gegen }  r_n(z) \in \mathbb{K} \text{ und:}$ 

$\forall_{\epsilon \in \mathbb{R}^+} \exists_{N \in \mathbb{N}}\forall_{n > N} \forall_{z \in M} |r_n(z)| < \epsilon$


## Konvergenzkriterien
- *Folgenkriterium*
$f \text{ stetig in  } x_{0} \implies \forall_{\text{ Folgen} a_{n} \in A} \lim_{n \to \infty} a_{n} = x_{0} \implies \lim_{n \to \infty} f(a_{n}) = x_{0}$

- *Wurzelkriterium*

$$
\begin{align}
\exists_{0 <q < 1}  (\sqrt[n]{|a_n|} &\le q < 1 \text{ für fast alle} n \in \mathbb{N})  \\
\implies  \sum_{j = 1}^{\infty} a_j &\text{ absolut. konvergent} \\
\{n \in \mathbb{N}: \sqrt[n]{|a_n|} &\ge 1\} = \infty \implies \sum_{j = 1}^{\infty} a_j \text{ divergent.}
\end{align}
$$

- *Quotientenkriterium*
Seien alle $a_n \not = 0$.

$\Big(\exists_{0 < q < 1} \big( |\frac{a_{n+1}}{a_n}| \le q < 1 \big)\Big)$ (für fast alle $n$) $\implies \sum_{n=1}^{\infty} a_n$ absolut konvergent.

Falls: $|\frac{a_{n+1}}{a_n}| \ge 1$ für fast alle $n \implies \sum_{n=1}^{\infty} a_n$ divergent.

- *Leibnizkriterium*
- *Majorantenkriterium*

*Allgemein:*

Damit eine Reihe konvergieren kann, muss die innere Folge konvergieren, jedoch kann aus dieser Definition nicht gefolgert werden, dass eine Reihe konvergiert, nur weil die innere Folge das macht: Bsp:
$S_{n} := \underbrace{\sum_{n = 1}^{\infty} \underbrace{\frac{1}{n}}_{\text{innere Folge konv.}}}_{\text{insgesamt divergiert die Reihe}}$


## Konvergenz Radien

*Für jede Potenzreihe* $\sum_{j = 0}^{\infty} a_{j}z^{j}$ *gibt es:*
$r \in [0, \infty]:= \mathbb{R}_{0}^{+} \cup \{\infty\}$ *, genannt Konvergenzradius (KR) der Reihe so, dass*
$$
\begin{align}
\Big(z \in \mathbb{K} \land |z| < r \Big)  &\implies  \sum_{j = 0}^{\infty} a_{j}z^{j} \text{ konvonvergiert absolut in } \mathbb{K}  \\
\Big( z \in \mathbb{K} \land |z| > r \Big) &\implies  \sum_{j = 0}^{\infty} a_{j}z^{j} \text{ divergiert in } \mathbb{K} \\
\end{align}
$$

### r bestimmen

*Entwerder:*

a) $r = \frac{1}{L} \text{ , mit  } L := lim sup \sqrt[n]{|a_{n}|}$
	- *lim sup := Größter HP, falls* $\sqrt[n]{|a_{n}|}$ *beschränkt*
	- *sonst* $\infty$
b) $r = \lim_{n \to \infty} |\frac{a_{n}}{a_{n+1}}|$

### Reihe abs. konvergent

$\sum_{j = 1}^{\infty} a_j$ absolut konvergent $\iff \sum_{j = 1}^{\infty} a_j$ *konvergent*
	- d.h. $|\sum_{j = 1}^{\infty} a_j | \le \sum_{j = 1}^{\infty} |a_j|$ 


## Wichtige Reihen

### Harmonische Reihe

$\sum_{k = 1}^{\infty} \frac{1}{k} = \infty$ hier konvergieren die Summanden zwar gegen 0 aber die Reihe *divergiert*

### Geometrische Reihe

- $\sum_{n=0}^{\infty} q^n$ für $|q| < 1$

- $s_n = \sum_{n=0}^{n} q^n = \frac{1-q^{n+1}}{1-q}$

- *Limes:*
	- $\boxed{\forall_{|q| < 1} \sum_{n=0}^{\infty} q^n = \lim s_n = \lim  \frac{1-q^{n+1}}{1-q} = \frac{1}{1-q}} $
