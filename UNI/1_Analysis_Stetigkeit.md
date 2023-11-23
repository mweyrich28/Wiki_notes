# Stetigkeit
:stetigkeit:

## Einführung in die Dtetigkeit (Renate)
» "Man kann die Funktion mit einem Strich zeichnen, ohne je abzusetzen"
- Hängt von $\mathbb{D}_{f}$ ab

*Beispiel für Stetigkeit:*
- In der Natur sind die meisten Funktionen stetig (in der Regel)
- Wachstum von Pflanzen: "stetig"
- Achtzehn werden: "sprunghaft (also nicht stetig)"


*Übersetzt in Mathe:*
- Funktion hat an Stelle $f(5) = 8$, was ist es bei $f(4.999999999999) \text{ und } f(5.00000001) \text{?} $, ist es nahe bei $8$?
- Was ist Nähe:
	- In der Nähe von $8$, wie nahe wollen wir denn an die $8$?
	- $\implies 8 - \epsilon \land 8 + \epsilon $
	- Stetigkeit bei $x = 5$: *"Für jedes Epsilon (>0) muss es ein Delta geben, so dass für alle x, die näher als Delta an 5 dran sind sicher gilt, dass f(x) zwischen 8 - Epsilon und 8 + Epsilon liegt"*

- Beispiel:
$$
\begin{align}
f(x) &= x^{2} \\
f(5) &= 25 \\
\epsilon &= 0,01 \\
|x^{2}-25| &< 0,01 \\
x^{2} &< 25,01 \\
x^{2}-25 &> -0,01
\end{align}
$$


## Stetigkeit
Sei $M \subseteq \mathbb{C}, \zeta \in M$, Fkt. $f:M \to \mathbb{K}$ heißt *stetig* in $\zeta$, gdw:

- $\boxed{\forall_{\epsilon > 0} \exists_{\delta > 0} \forall_{z \in M} (|z - \zeta| < \delta \implies |f(z) - f(\zeta)| < \epsilon)}$

So ist jede affine Fkt. (Polynom): $f: \mathbb{K} \to \mathbb{K}, f(z) := az + b$ stetig: wähle $\delta := \frac{\epsilon}{|a|}$


## Folgenkriterium
$M \subseteq \mathbb{C}, f : M \to \mathbb{K}, x_0 \in M$
- $f$ stetig in $x_0 \iff \boxed{\forall_{(z_{n}) n \in \mathbb{N}}\big( \lim_{n \to \infty} z_n = x_0 \implies \lim_{n \to \infty} f(z_n) = f(x_0)\big)}$

Funktionen die in die $\mathbb{C}$ abbilden: $f: M \to \mathbb{C}, M \subseteq \mathbb{C}$ *stetig* in $x_{0} \in M$ g.d.w:
	- $\text{Re } f \text{ und Im } f \text{ beide stetig in} x_{0}$

## Linksseitige und rechtsseitige Stetigkeit
$$
\text{Funktion }  f: \mathbb{R} \to \mathbb{R}  \text{ ist linksseitig  (bzw. rechtsseitig) stetig in } a \text{ ,wenn die Funktionen:}\\
g: ]-\infty,a] \to \mathbb{R}\\
h: [a, \infty[  \to \mathbb{R}\\
\text{stetig in } a \text{ ist }\\
\text{Beweis: }\\
\text{Sei } \epsilon > 0 \text{ so gibt es ein  } \delta_{1} > 0  \text{(da g in a stetig) so, dass }\\
\forall_{x \in \mathbb{R}} \Big( a - \delta_{1} < x \le a \implies |f(x)- f(a)| = |g(x)-g(a)| < \epsilon  \Big)\\
\text{Da auch } h \text{ stetig in  } a \text{ ist, gibt es auch } \delta_{2} > \text { so, dass }\\
\forall_{x \in \mathbb{R}} \Big( a \le x < a + \delta_{2} \implies |f(x)- f(a)| = |h(x)-h(a)| < \epsilon  \Big)\\
\text{Sei nun } \delta =  max\{ \delta_{1}, \delta_{2}\} \text{ Ist dann } |a-x| < \delta \text{ so folgt  } |f(x) - f(a)| < \epsilon
