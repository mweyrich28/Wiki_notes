# Kapitel 4 - Relationen Kalkül
**SLIDES:** [Datenbanken Relationen Kalkül](file:///home/malte/OneDriver/01_Studium/3.Semester/Datenbanken/Slides/dbs1_04.pdf)

## Begriff
Mathematische Prädikatenlogik kann verwendet werden um Datenbankabfragen zu formulieren.

Z.B:
$$
\left\{t| \underbrace{\text{Städte}(t)}_{t \in \text{Städte}} \land t[\text{Land}] = \text{Bayern} \land t[\text{SEinw}] \ge 500.000\right\}
$$
## Unterschied zur Relationalen Algebra
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
- **Formeln**: $\Psi(t)$
- **Ausdrücken**: $\left\{t| \Psi(t)\right\}$

> :memo: **Note:** Ein Ausdruck beschreibt also immer die Menge aller 
> Tupel, die die Formel $\Psi$ erfüllen.

> :memo: **Note:** Ein Kalkül besteht immer aus:
> - **Syntax**: Wie sind die Ausdrücke aufgebaut?
> - **Semantik**: Was bedeuten die Ausdrücke?

#### Tupelvariablen
... haben definiertes Schema:
- Schema(t) = $(A_{1}:D_{1}, A_{2}:D_{2}, \dots)$
- Schema(t) = $R$ ( $t$ hat das selbe Schema wie die Relation)

Zugriff auf die Komponenten:
- $t[A]$ oder $t.A$ für einen Attributennamen $A \in \text{Schema}(t)$
- oder auch $t[1], t[2]$ usw.

**Tupelvariable** kann in einer Formel $\Psi$ **FREI** oder **GEBUNDEN** sein

#### Atome
Es gibt drei Arten von Atomen:
- $R(t)$ →  $R$ ist Relationsname, $t$ Tupelvariable →  "$t$ ist ein Tupel von $R$"
- $t.A \boxdot s.B$ → $t$ und $s$ Tupelvariablen, $A$ und $B$ Attributnamen, $\boxdot$ ist ein Vergleichsoperator →  "$t.A$ und $s.B$ steht in Beziehung zu"
- $t.A \boxdot c$ →  t ist Tupelvariable und c eine passende Konstante
- $\boxdot$ ist ein Vergleichsoperator: $\left\{=, \neq, <, \leq, >, \geq\right\}$
![3_DBS_4_Formeln](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_Formeln.png)

### Belegung von Variablen
Gegeben:
- Eine Tupelvar $t$ mit Schema $(A_{1}:D_{1}, A_{2}:D_{2}, \dots)$
- Eine Formel $\Psi(t)$ in der $t$ frei vorkommt
- Ein beliebiges konkretes Tupel $r$ (mit Werten)

→  Bei der Belegung von $t$ mit $r$ wird jede freie Vorkommnis von $t$ in $\Psi$ durch $r$ ersetzt.

→  Insbesondere wird der Attributen Wert $r.A$ für $t.A$ eingesetzt.

→  Man schreibt $\Psi(r|t)$

Beispiel:

![3_DBS_4_Belegung_Var](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_Belegung_Var.png)

### Interpretation von Ausdrücken

> :memo: **Note:** Interpretation von Ausdruck $I(\left\{t|\Psi(t)\right\})$ stützt sich
> - auf Belegung von Variablen
> - und Interpretation von Formeln

**Gegeben:**

----------------------------------------------------------------------------------------------------------------------------------------
- $E = \left\{t|\Psi(t)\right\}$ 
- $t$ ist die einzige freie Variable in $\Psi(t)$
- Schema$(t)$ = $D_{1} \times D_{2} \times \dots$
- Dann ist der Wert von $E$ die Menge aller (denkbaren) Tupel $r \in D_{1} \times D_{2} \times \dots$, für die gilt: $I(\Psi(r|t)) == true$

Bsp

![3_DBS_4_Anfragen_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_Anfragen_Bsp_1.png)


### Sicherer Ausdruck
> :warning: **Note:** Die momentane Definition ermöglicht es, unendliche Relationen zu beschreiben
> - z.B. Schema(t) = {String, String} (Schema ist unendlich)
> - Das Ergebnis kann nicht gespeichert werden, da es unendlich ist.
> - Ergebnis kann nicht ein endlicher Zeit berechnet werden, da es unendlich ist.

> :eight_spoked_asterisk: **Definition:** Ein Ausdruck heißt **SICHER**, wenn jede Tupelvariable sich nur auf Werte bezieht, die 
> einer gespeicherten Relation annehmen kann, also positiv in einem Atom $R(t)$ vorkommt

### Bereichskalkül
- **Tupelkalkül:** Tupelvariablen $t$ (ganzer Tupe)
- **Bereichskalkül:** Bereichsvariablen $x_{1}:D_{1}, x_{2}:D_{2}, \dots$ (einzelne Attribute) 
  →  (Bereich=Wertbereich=Domäne)

**Ein Ausdruk hat die Form:**
$$
\left\{x_{1}, x_{2}, \dots | \Psi (x_{1}, x_{2}, \dots)\right\}
$$
**Atome** haben die From:
- $R_{1}(x_{1}, x_{2}, \dots)$: Tupel (x1, x2, ...) tritt in Rlation $R_{1}$ auf
- $x \boxdot y$: $x,y$ Bereichsvariablen bzw. Konstanten, $\boxdot$ Vergleichsoperator $\in \left\{=, \neq, <, \leq, >, \geq\right\}$

**Formeln** analog zum Tupelkalkül

#### Beispiel
![3_DBS_4_Bereichskalkül_Bsp](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_Bereichskalkül_Bsp.png)

> In welchem Land liegt Passau?:
$$
\left\{x_{3} | \exists_{x_{1}, x_{2}}: Städte(x_{1},x_{2},x_{3}) \land x_{3} = Passau)\right\}
$$
> Oder auch
$$
\left\{l | \exists_{e}: Städte(Passau, e, l))\right\}
$$
→  D.h Konstanten dürfen direkt in die Relation eingetragen werden.
> Finde alle Länder in denen die CDU regiert:
$$
\left\{x_{1} | \exists_{x_{2}, x_{3}, y_{2}}: Städte(x_{1},x_{2},x_{3}) \land Länder(x_{3}, y_{2}, CDU))\right\}
$$
→  D.h. "Equijoin" direkt über Verwendung derselben Bereichsvariable.
> Welche Länder weden von der SPD allein regiert?
$$
\left\{x_{1} | \exists_{x_{2}}: Länder(x_{1}, x_{2}, SPD) \land \neg \exists_{y_{3}}:(Lander(x_{1}, x_{2}, y_{2})) \land y_{3} \not = SPD\right\}
$$

# Query By Example (QBE)
- Beruht auf Bereichskalkül
- Ausdrücke nicht in Text wie bei SQL
- Ausdrücke werden grafisch dargestellt
- Nach Eintrag von Werten in das Tabellengerüst wird die Abfrage ausgeführt und das System füllt die Tabelle
- Ziel: Benutzerfreundlichkeit

![3_DBS_4_QBE](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE.png)
![3_DBS_4_QBE_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_2.png)

## Anfragen mit Bedingungen
![3_DBS_4_QBE_3](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_3.png)
![3_DBS_4_QBE_4](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_4.png)

## Join Anfragen
![3_DBS_4_QBE_5](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_5.png)
![3_DBS_4_QBE_6](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_6.png)

## Anfragen mit Ungleichungen
![3_DBS_4_QBE_Ungleichungen](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Ungleichungen.png)

## Anfragen mit Negation
![3_DBS_4_QBE_Negation](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Negation.png)

## QBE Einfügen
![3_DBS_4_QBE_Einfügen](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Einfügen.png)

## Löschen eind Ändern
![3_DBS_4_QBE_Löschen_Ändern](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Löschen_Ändern.png)

## Vergleich QBE und Bereichskalkül

| QBE                 | Bereichskalkül                            |
|---------------------|-------------------------------------------|
| Konstanten          | Konstanten                                |
| Bereichsvariablen   | Bereichsvariablen                         |
| leere Spalte        | parrweise verschiedene Bereichsvariablen, |
|                     | $\exists$-quantifiziert                   |
| Spalten mit **P.**  | freie Variablen                           |
| Spalten ohne **P.** | $\exists$-quantifizierte Variablen        |

> :memo: **Note:** QBE ist relational vollständig, jedoch ist für manche Abfragen der relationalen 
> Algebra eine Folge von QBE-Abfragen nötig.


## Umsetzung einer QBE-Anfrage (ohne Negation)
1. Erzeugen aller Attribute $A_{i}$ aller vorkommenden Tabellen-Zeilen der Anfrage eine Bereichsvariable $x_{i}$
2. Steht bei Attribut $A_{i}$ das Kommando <span style="background:#98fb98;">**P.**</span>, dann schreibe $x_{i}$ zu den freien Variablen $(\left\{\dots, x_{i}, \dots | \dots\right\})$, 
   sonst binde $x_{i}$ mit einem <span style="background:#458588;">$\exists$-Quantor</span> $(\left\{\dots | \exists \dots , x_{i}, \dots \right\})$
3. Binde alle Variablen der Anfrage mit einem <span style="background:#d79921;">$\exists$-Quantor</span>:

![3_DBS_4_QBE_Umsetzung](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Umsetzung.png)

![3_DBS_4_QBE_Umsetzung_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Umsetzung_2.png)

- Füge für jede vorkommende Relation $R$ ein Atom der Form $R(x_{i}, x_{i+1}, \dots)$ mit $\land$ an die Formel 
  $\Psi$ an.

![3_DBS_4_QBE_Umsetzung_3](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Umsetzung_3.png)

- Steht bei $A_{i}$ ein Zusatz der Form <span style="background:#cc241d;">**Const**</span> bzw <span style="background:#cc241d;">$\le$**Const**</span> etc.,
  dann hänge <span style="background:#cc241d;">$x_{i} = Const$</span> bzw. <span style="background:#cc241d;">$x_{i} \le Const$</span> mit <span style="background:#cc241d;">$\land$</span> an Formel:

![3_DBS_4_QBE_Umsetzung_4](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Umsetzung_4.png)

![3_DBS_4_QBE_Umsetzung_5](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Umsetzung_5.png)

- Gleiches Vorgehen bei Zuständen der Form <span style="background:#cc241d;">\_Variable</span> bzw. <span style="background:#cc241d;">$\le$**\_Variable**</span> usw:

![3_DBS_4_QBE_Umsetzung_6](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Umsetzung_6.png)

- Ggf. wird der Inhalt der Condition-Box mit <span style="background:#cc241d;">$\land$</span> angehängt
- Meist lässt sich der Term noch vereinfachen:

![3_DBS_4_QBE_Umsetzung_7](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_QBE_Umsetzung_7.png)


# Quantoren und Subquereies in SQL
- Quantoren sind Konzept der Relationenkalküls
- In relationaler Algebra nicht vorhanden
- Können zwar simuliert werden:
	- $\exists$ mit Join und Projektion 
	  $\left\{x \in R | \exists_{y} \in S: \dots \right\} \equiv \Pi_{R.\\*}(\sigma\dots(R \times S))$
	- $\forall$ mit Hilfe des Quotienten
	  $\left\{x \in R | \forall_{y} \in S: \dots \right\} \equiv (\sigma\dots(R \times S)) \div S$
- Häufig Formulierungen mit Quantoren natürlicher
- SQL: Quantifizierter Ausdruck wird als **Subquery** formuliert

## Beispiel für ein Subquery
```sql
SELECT * 
FROM Kunde 
WHERE EXISTS (SELECT ... FROM ... WHERE ...)
	           -- ^^^^ Subquery ^^^^
```
- In `WHERE`-Klausel der Subquery auch Zugriff auf Relationen/Attribute der Hauptquery möglich
- Eindeutigkeit ggf. durch Aliasnamen für Relationen (wie bei *Self-Join*): 
  ```sql
  SELECT *
  FROM Kunde K1
  WHERE EXISTS (SELECT * 
                FROM Kunde K2 
                WHERE K1.Ard = k2.Adr AND ...
               )
  ```

### Existenzquantor
- Schlüsselwort `EXISTS` gefolgt von Subquery in runden Klammern
- `EXISTS`-Operator liefert `TRUE`, wenn Subquery nicht leer ist

**Beispiel: KAdr der Kunde, wo Auftrag existiert:**
```sql
SELECT KAdr FROM Kunde k
WHERE EXISTS (
              SELECT * 
              FROM Auftrag a 
              WHERE k.KAdr = a.KAdr
             )
```


### Allquantor
- Keine explizite Unterstützung in SQL
- Allquantor kann durch Negation des Existenzquantors simuliert werden:
  $$
  \forall_{x} \Psi(x) \equiv \neg \exists_{x} \neg \Psi(x)
  $$
- Also Notation in SQL: 
  
  ... `WHERE NOT EXISTS (SELECT ... FROM ... WHERE NOT ...)`

**Beispiel: Die Länder, die von der SPD alleine regiert werden:**

```sql
SELECT * FROM Länder L1
WHERE NOT EXISTS (
                  SELECT * 
                  FROM Länder L2 
                  WHERE L1.LName = L2.Name AND NOT L2.Partei = 'SPD'
                  )
```

### Direkte Subqueries
- An jeder Stelle der `SELECT-`und `WHERE`-Klausel, wo ein konstanter Wert 
  stehen kann, kann auch eine Subquery stehen.
- Einschränkungen:
	- Subquery darf nur ein Attirbut ermitteln (Projektion)
	- Subquery darf nur ein Tupel ermitteln (Selektion)
- Oft schwierig zu erkennen, ob Subquery sinnvoll ist / was er überhaupt macht!


### Weitere Quantoren
- Quantoren bei Standard-Vergleichen in `WHERE`-Klausel:
  - $A_{i} \boxdot$ all(select..from..where...) ($\forall$-Quantor)
  - $A_{i} \boxdot$ some(select..from..where...) ($\exists$-Quantor)
  - $A_{i} \boxdot$ any(select..from..where...) ($\exists$-Quantor)
  - (wobei $\boxdot$ ein Vergleichsoperator $\in \left\{=, \neq, <, \leq, >, \geq\right\}$ ist)
- Bedeutung:
	- $A_{i} \boxdot$ all(subquery) $\equiv$ $\{\dots | \forall_{t} \in \text{Subquery:} A_{i} \boxdot t$
	- ist größer als <span style="color:#cc241d;">alle</span> Werte, die die Subquery liefert
- Einschränkung:
	- Subquery darf nur ein Ergebnis-Attribut ermitteln 
	- Aber mehrere Tupel sind erlaubt
	- → Also Menge und nicht Relation

**Beispiel: Ermittle den Kunde mit dem höchsten Kontostand:**
```sql
SELECT KName, KAdr
FROM Kunde
Where Kto >= all (SELECT Kto FROM Kunde)
```

Äquivalent zu folgendem Ausdruck mit `EXISTS`:
```sql
SELECT KName, KAdr
FROM Kunde
WHERE NOT EXISTS (
				  SELECT * 
				  FROM Kunde K2 
				  WHERE K2.Kto >= Kunde.Kto
				 )
```

### Subquery mit IN
Nach dem Ausdruck <span style="color:#cc241d;">$A_{i} \textbf{ [NOT] } in \dots$</span> kann stehen:
- Explizite Aufzählung von Werten: $A_{i} \textbf{in} (2,3,5,7,11,13)$
- Eine Subquery: 
  
  $A_{i} \textbf{in} (\textbf{ select } wert \textbf{ from } Primzahlen \textbf{ where } wert \le 13)$
  
  Auswertung:
  - Erst Subquery auswerten
  - In explizite Form (2,3,5,7,11,13) umwandeln
  - Dann einsetzen
  - Zuletzt Hauptquery auswerten

**Beispiele:**
- Gegeben:
	- MacigNumbers (Name: String, Wert: Integer)
	- Primzahlen (Zahl: Integer)
- Anfrage: Alle MagicNumbers die Prim sind:
  ```sql
  SELECT *
  FROM MagicNumbers
  WHERE Wert IN (SELECT Zahl FROM Primzahlen)
  ```
- Ist äquivalent zu:
  ```sql
  SELECT *
  FROM MagicNumbers
  WHERE EXISTS (
				SELECT *
				FROM Primzahlen
				WHERE Wert = Zahl
			   )
  ```
- Und mit ANY/SOME/ALL:
  ```sql
  SELECT *
  FROM MagicNumbers
  WHERE Wert = SOME (SELECT Zahl FROM Primzahlen)
  ```
![3_DBS_4_Subqueries_Bsp](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_4_Subqueries_Bsp.png)

## Typische Formen der Subquery
- Bei `EXISTS` bzw `NOT EXISTS` ist für die Hauptquery nur relevant, 
  ob das **Ergebnis die Leere Menge ist** oder nicht.
  - Deshalb muss keine Projektion durchgeführt werden: 
	`SELECT ... FROM ... WHERE EXISTS (SELECT * FROM ...)`

- Bei `SOME`, `ANY`, `ALL` und `IN` ist das Ergebnis der Subquery
  eine Menge von Werten (→ Ein Attribut mehrerer Tupel), die in die Hauptquery eingesetzt werden:
  - Deshalb muss in der **Subquery**eine Projektion durchgeführt werden: 
	`SELECT A FROM ... WHERE A <=  ALL (SELECT B FROM ...)`

- Das Ergebnis der direkten Subquery ist genau ein Wert:
	- Projektion auf ein Attribut, Selektion eines Tupels:
	  `... WHERE A <= (SELECT B FROM ... WHERE schlüssel = ...)`
