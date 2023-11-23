# Binomialkoeffizienten & Binomischer Lehrsatz
:binomial_coefficient:binomeal:binomischer_lehrsatz:

## Pascalisches Dreieck
| n=6 | k | k | k | k  | k | k  | k | k | k |
|-----|---|---|---|----|---|----|---|---|---|
| n=1 |   |   |   |    | 1 |    |   |   |   |
| n=2 |   |   |   | 1  |   | 1  |   |   |   |
| n=3 |   |   | 1 |    | 2 |    | 1 |   |   |
| n=4 |   | 1 |   | 3  |   | 3  |   | 1 |   |
| n=5 | 1 |   | 4 |    | 6 |    | 4 |   | 1 |
| n=6 |   | 5 |   | 10 |   | 10 |   | 5 |   |

*Also gilt:*
- $\underbrace{\binom{n+1}{k}}_{\text{untere Zahl im Dreieck}  = \underbrace{\binom{n}{k-1} + \binom{n}{k}}_{\text{oberen zwei Zahlen}} } $ so ist zum Beispiel $\binom{7}{2} = \binom{6}{1} + \binom{6}{2}$ Das gleiche gilt für $n \in \mathbb{C}$
- $\binom{n}{0} = \binom{n}{n} = 1$
- Sei $n \in \mathbb{C}$ so gilt: $\forall_{n \in \mathbb{C}}\forall_{k \in \mathbb{N}}\binom{n}{k} := \prod_{j = 1}^{k} \frac{n+1-j}{j}$

## Binomischer Lehrsatz
- $\forall_{z,w \in \mathbb{C}}\forall_{n \in \mathbb{N}_{0}} \big(z+w\big)^{n} = \sum_{k = 0}^{n} \binom{n}{k}z^{n-k}w^{k}$	
