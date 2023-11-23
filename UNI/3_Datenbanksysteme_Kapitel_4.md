# Slides - Relationen Kalkül
[Datenbanken Relationen Kalkül](file:///home/malte/OneDriver/01_Studium/3.Semester/Datenbanken/Slides/dbs1_04.pdf)

## Begriff
Mathematische Prädikatenlogik kann verwendet werden um Datenbankabfragen zu formulieren.

Z.B:
$$
\left\{t| \underbrace{\text{Städte}(t)}_{t \in \text{Städte}} \land t[\text{Land}] = \text{Bayern} \land t[\text{SEinw}] \ge 500.000\right\}
$$
## Unterschied zur Relationalen Algerbra
> *Relationenalgebra* ist **prozeduale** Sprache →  WIE
> - Ausdruck gibt an, wie Ergebnis berechnet wird (also mit welchen Operationen).

vs

> *Relationen Kalkül* ist **deklarative** Sprache →  WAS
> - Ausdruck beschreibt, welche Eigenschaften die Tupel der 
>   Ergebnisrelation haben müssen, ohne eine Berechnungsprozedur anzugeben.
> 
> Es gibt zwei verschiedene Ansätze:
> - *Tupelkalkül* →  Variablen sind vom Typ Tupel
> - *Bereichskalkül* →  Variablen haben einfachen Typ

### Tupelkalkül
Es wird gearbeitet mit:
- **Tupelvariablen**: $t$
- **Formeln**: $\Phi(t)$
- **Ausdrücken**: $\left\{t| \Phi(t)\right\}$

> :memo: **Note:** Ein Ausdruck beschreibt also immer die Menge aller 
> Tupel, die die Formel $\Phi$ erfüllen.

> :memo: **Note:** Ein Kalkül besteht immer aus:
> - **Syntax**: Wie sind die Ausdrücke aufgebaut?
> - **Semantik**: Was bedeuten die Ausdrücke?
