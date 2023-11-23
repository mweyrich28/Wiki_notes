# Beschränkte & abgeschlossene & kompakte Mengen
:abgeschlossenheit:bescränktheit:kompaktheit:

## Definition
$\text{Sei } A \subseteq \mathbb{C}$:

- $A$ heißt *beschänkt*, g.d.w
	- $A \neq \emptyset \text{ oder } \{|z|: z \in A\} \text{ beschänkt in } \mathbb{R} \text{ d.h. g.d.w:} $
	- $\exists_{M \in \mathbb{R}^{+} A \subseteq B_{M}(0)}$
	- Bsp: so ist $M:=]0,1] \text{ nicht abgeschlossen, da: } a_{n}:= \frac{1}{n} \text{ Folge in } M \text{ aber } \lim_{n \to \infty} a_{n} = 0 \notin M$

- $A$ heißt *abgeschlossen* g.d.w der Grenzwert jeder Folge in $A$, die in $\mathbb{C}$ konvergiert, in $A$ liegt. (so ist auch $\emptyset$ abgeschlossen) 

- $A$ heißt *kompakt*, g.d.w $A$ *abgeschlossen* und *beschänkt*

- Weitere Beispiele:
	1. Endliche Kompakte Menge: $ \{0\}$
	2. Unendliche Kompakte Menge: $[0,1]$
	3. Beschränkte Menge mit $\infty$ vielen HP: $]0,1[$
	4. Unbeschrämkt und abgeschlossen: $\mathbb{N}$

## Beispiele
- $\emptyset $ ist *kompakt*, $\forall_{x \in \mathbb{C}}\{x\}$ ist *kompakt*, $\mathbb{C} \land \mathbb{R}$ sind *abgeschlossen aber nicht beschränkt*

- Intervalle wie: $[a,b], [a, \infty[, ]-\infty,b]$ sind *abgeschlossen:* So folgt aus Folge $x_{n}$ in $[a,b]$ mit $x = \lim_{n \to \infty} x_{n}$, dass $x \in [a,b]$

- Offene und halboffene Intervalle sind *nicht abgeschlossen:* 
	- So ist z.B. $(b- \frac{1}{n})_{n}$ Folge in $[a,b[$, aber $\lim_{n \to \infty} (b- \frac{1}{n}) = b \notin [a,b[$

- Nur Intervalle der Form $[a,b]$ sind *Kompakt*
