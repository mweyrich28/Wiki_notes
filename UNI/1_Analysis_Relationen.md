# Relationen
:relationen:

## Definition
Relation $R$ ist Teilemenge $R$ von $A \times B$
Für $A = B$ heißt $R$ Relation auf $A$
Schreibe $aRb: \iff (a,b) \in R$

## Eigenschaften
- *Reflexive* Relationen: $\forall_{x \in A} xRx$
- *Symmetrische* Relationen: $\forall_{x,y \in A}\big(xRy \implies yRx \big)$
- *Antisymmetrische* Relationen: $\forall_{x,y \in A} \big((xRy \land yRx) \implies x = y\big)$
- *Transitive* Relationen: $\forall_{x,y,z \in A}\big((xRy \land yRz) \implies xRz\big)$

## Äquivalenzrelationen
Relation $R$ auf $A$ heißt *Äquivalenzrelation* $\iff R \text{ref., sym. & tran.}$

## Partialordungen
Relation $R$ auf $A$ heißt *Partialordung(PO)* $\iff R \text{ ref., antisym. & tran.}$ Man schreibt $x \le y$
Eine PO heißt *totale Ordnung (TO)*, wenn zusätzlich: $\forall_{x,y \in A}(x \le y \lor y \le x)$

Quasiordnung: PO ohne Antisymmetrie
