# Grenzwerte und Konvergenz
:folgen:konvergenz:limes:gleichmäßige_konvergenz:punktweise_konvergernz:

## Folgen
- Folge $(z_{n})_{n \in \mathbb{N}} \text{in} \mathbb{K}$ heißt *Konvergent* mit *Limes* $z \in \mathbb{K}$ g.d.w:
	- $\boxed{\lim_{n \to \infty} z_{n} = z \iff \forall_{\epsilon > \mathbb{R}^{+}}\exists_{N \in \mathbb{N}}\forall_{n > N} |z_{n} - z| < \epsilon}$

- Sei Folge $z_{n}$ definiert in $\mathbb{C}$, dann ist $z_{n}$ konvergent, g.d.w $(\text{Re } z_{n}) \text{ und} (\text{Im } z_{n})$ beide konvergent in $\mathbb{R}$
	- $\boxed{\lim_{n \to \infty} z_{n} = z \iff \lim_{n \to \infty} \text{Re } z_{n} = z \land \lim_{n \to \infty} \text{Im } z_{n} = n  }$

## Epsilon Umgebung
- Sei $z \in \mathbb{K}, \epsilon > 0. B_{\epsilon}(z) = \{w \in \mathbb{K}: |w-z| < \epsilon\}$
- $U \subseteq \mathbb{K}$ heißt Umgebung von $z$ g.d.w $\exists_{\epsilon > 0} B_{\epsilon}(z) \subseteq U$

## Grenzwertbegriff
- $\lim_{n \to \infty} z_{n} = z \iff$ jede Umgebung von $z$ enthält fast alle $z_{n}$
- Ist $z_{n}$ konvergent $\implies (z_{n})_{n \in \mathbb{N}}$ beschränkt!

## Einschachtelungssatz
Seinen $(x_{n}), (y_{n}), (a_{n})$ Folgen in $\mathbb{R}$, und gelten $x_{n} \le a_{n} \le y_{n}$ für fast alle $n$, dann:

- $\boxed{\lim_{n \to \infty} x_{n} = \lim_{n \to \infty} y_{n} = x \in \mathbb{R} \implies \lim_{n \to \infty} a_{n} = x}$

## Bestimmte Divergenz ## 
Folge $x_{n}$ heißt *bestimmt divergent* g.d.w einer dieser beiden Fälle eintritt:

- $\lim_{n \to \infty} x_{n} = \infty \iff \forall_{K \in \mathbb{R}} \exists_{N \in \mathbb{N}} \forall_{n > N} x_{n} > K$
- $\lim_{n \to \infty} x_{n} = - \infty \iff \forall_{K \in \mathbb{R}} \exists_{N \in \mathbb{N}} \forall_{n > N} x_{n} < K$

## Häufungspunkte
$z \in \mathbb{K}$ heißt HP der Folge $Z_{n}$ in $\mathbb{K}$ g.d.w:

- $\forall_{\epsilon > 0} \-\{n \in \mathbb{N}: z_{n} \in B_{\epsilon}(z) = \infty \}$
	- So hat beispielsweise $((-1)^{n})_{n \in \mathbb{N}}$ die *HP* bei $-1 \text{ und} 1$

## Cauchyfolge
$(z_n)$ Folge in $\mathbb{K}$ heißt *Cauchyfolge*, g.d.w. 
- $\boxed{\forall_{\epsilon \in \mathbb{R}^+} \exists_{N \in \mathbb{N}} \forall_{n,m > N} |z_n - z_m| < \epsilon}$
- Aus Konvergenz folgt Cauchyfolge


## Sätze
- Konvergente Folgen sind beschränkt
- Nullfolgen sind Folgen die gegen 0 konv.
- Eine Folge, die durch Nullfolge beschr. ist, ist selbst eine Nullfolge
- Produkt einer Nullfolge und einer beschr. Folge ist eine Nullfolge
- Grenzwertsätze (Th. 7.13)
- Einschachtelungssatz
- Isotone Folge konv. bzw. div. bestimmt gegen plus Unendlich

## Wichtig
$f \text{ hat Limes } \mu \in \mathbb{K} \text{ für  } z \to \zeta \text{ g.d.w }$
$\forall_{(z_{n})_{n \in \mathbb{N}} \text{ in } M \backslash \{ \zeta\}} \Big(\lim_{n \to \infty} z_{n} = \zeta \implies \lim_{n \to \infty} f(z_{n}) = \mu\Big)$

## Gleichmäßige Konvergenz:
- $\frac{1}{n} \cdot \sin (x)$ hier kann ich ein gemeinsames n finden, so dass sich $f_{n}$ in allen Punkten gleichmäßig annähert

## Punktweise Konvergenz:
- Zum Beispiel: $f_{n} = \frac{1}{n} \cdot x^{2}$
