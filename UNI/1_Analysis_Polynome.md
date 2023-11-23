# Polynome
:mono:polynom:

## Definition

Sei $n \in \mathbb{N}_{0}$. Jede Folge $\mu : \mathbb{K} \to \mathbb{K}, \mu(x):=x^{n}$ heißt *Monom*, so ist ein Polynom die

Linearkombination mehrerer Monome:
$$
P:\mathbb{K}\to \mathbb{K} \text{ ,} P(x) = \sum_{j = 0}^{n} \underbrace{a_{j}}_{\text{Koeffizient von P}} x^{j}
$$

## Weitere Regeln
- $(\lambda P)(x) = \sum_{j = 0}^{n} (\lambda a_{j})x^{j}$, $\text{deg}(\lambda P = n)$
- $(Q + P)(x) = \sum_{j = 0}^{n} (a_{j} + b_{j})x^{j}$, $\text{deg}(P + Q) \le n = \text{max}\{n,m\}$
- $(Q \cdot  P)(x) = \sum_{j = 0}^{n + m} c_{j}x^{j} $, $\text{deg}(P \cdot  Q) = m + n$ 
	- mit $\forall_{j =0,...,n+m}c_{j} = \sum_{k = 0}^{j} a_{k}b_{j-k}$
