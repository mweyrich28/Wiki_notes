# Komplexität Algorithmen

## Insertion Sort
1. Aktuelles Element mit bereits sortiertem Feld vergleichen
2. An richtiger Stelle einfügen, Rest verschieben

## Bubble Sort
1. Durchlaufe das Array von links nach rechts
	1. compare a[n] to a[n+1]
	2. swap if a[n+1] < a[n]
	3. do until no swaps are necessary anymore

## Big O Notation
:big_o:big_o_notation:

Seien $f: \mathbb{N} \to \mathbb{N}$ und $g: \mathbb{N} \to  \mathbb{N}$ zwei Funktonen

Die Funktion f ist von der Größenordnung O(g), geschrieben $f \in O(g)$, wenn es
ein $n_0 \in \mathbb{N}$ und ein $c \in \mathbb{N}$ gibt, so dass gilt:
$\forall_{n \in \mathbb{N}}(n \ge n_0 \implies f(n) \le c \cdot g(n))$

Also anders gesagt: f wächst höchstens so schnell wie g


## Regeln
* Konstanten werden vernachlässigt
* Bei Summen zählt nur der Summand mit dem höchsten Exponenten
* Basis des Log ist unerheblich


| Komplexitätsklasse             | Sprechweise   | Typische Operationen           |
|--------------------------------|---------------|--------------------------------|
| $\mathcal{O}(1)$               | Konstant      | Zuweisung                      |
| $\mathcal{O}(\log{n})$         | logarithmisch | Suche in Binärbaum             |
| $\mathcal{O}(n)$               | linear        | Lineare Suche                  |
| $\mathcal{O}(n \cdot \log{n})$ |               | gute Sortierverfahren          |
| $\mathcal{O}(n^{2})$           | quadratisch   | primitive Sortierverfahren     |
| $\mathcal{O}(n^{k}), k > 1$    | polynomiell   |                                |
| $\mathcal{O}(2^{n})$           | exponentiell  | Ausprobieren von Kombinationen |

