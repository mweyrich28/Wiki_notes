**SLIDES:**
[Datenbanken Relationale Algebra](file:///home/malte/OneDriver/01_Studium/3.Semester/Datenbanken/Slides/dbs1_03.pdf)

# Anfragesprachen
Wichtigste Bespiele:
- Relationale Algebra
- Relationale Kalkül

> :memo: **Note:** Sie dienen als theoretisches Fundament für konkrete Anfragesprachen wie SQL oder QBE (Query by Example)


## Grundoperationen 
- Vereinigung $R = S \cup T$
- Differenz $R = S - T$
- Kartesisches Produkt $R = S \times T$
- Selektion $R = \sigma_{\text{Bedingung}}(S)$
- Projektion $R = \pi_{\text{Attributliste}}(S)$

> :warning: **Warning:** Diese Operationen sind nur anwendbar auf Relationen mit gleicher Relationenschemata (Name und Domäne.

### Selektion
Mit einer Selektion $R = \sigma_{\text{F}}(S)$ wird eine Teilmenge der Tupel aus $S$ ausgewählt, die eine durch
die logische Formel $\text{F}$ definierte Eigenschaft erfüllen:
$$
R = \color{red} \sigma_{F}(S) = \left\{t < t \in S \land F(t)\right\}
$$
- $R$ bekommt das gleiche Schema wie $S$.
- Die Formel $F$ besteht aus:
	- Konstanten ("Meier")
	- Attributen: Als Name PNr oder Nummer ($1)
	- Vergleichsoperatoren: $=, \neq, <, \leq, >, \geq$
	- Logischen Operatoren: $\land, \lor, \lnot$
- Formel $F$ wird für jedes Tupel von S ausgewertet.

**Beispiel:**

![3_DBS_3_Selektion_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Selektion_1.png)

![3_DBS_3_Selektion_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Selektion_2.png)

### Projektion
Die **Projektion** $R = \pi_{A,B,\dots}(S)$ erlaubt es:
- Spalten einer relation auszuwählen
- bzw. nicht ausgewählte Spalten zu verändern
- die Reihenfolge der Spalten zu ändern

In den Indizes sind die selektierten Attribut-Namen oder Attribut-Nummern ($1) aufgeführt.

Für die Anzahl der Tupel des Ergebnisses gilt:
$$
\left| \pi_{A,B,\dots}(S) \right| \leq \left| S \right|
$$

> :warning: **Warning:** *Nach dem Steichen von Spalten können Duplikate entstanden sein, die eleminiert werden,
damit wieder eine Relation entsteht.*

![3_DBS_3_Projektion_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Projektion_1.png)

#### Duplikat Eliminierung
Sind erforderlich nach:
- Vereinigung 
- Projektion

→  Das sind eigentlich billige Operationen

**ABER:**
- Die Duplikat-Eliminierung ist sehr teuer ($\mathcal{O}(n^{2})$)
- Besserer Algorithmus mit Sortierung: $\mathcal{O}(n \log n)$

# Beispiel Abfragen
![3_DBS_3_BSP_Abfragen_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_BSP_Abfragen_1.png)
![3_DBS_3_BSP_Abfragen_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_BSP_Abfragen_2.png)

# Abgeleitete Operationen
Eine Reihe nützlicher Operationen lassen sich mit Hilfe 
der 5 Grundoperationen ausdrücken:

## Durchschnitt
$$
R = S \cap T
$$
→  Finde zwei gemeinsame Tupel in $S$ und $T$.

$S \cap T = \left\{t | t \in S \land t \in T\right\}$

Der Durchschnitt wird mit Hilfe der Grundoperation "**Differenz**" implementiert:
$$
A \cap B = A - (A - B)
$$
![3_DBS_3_Durchschnitt](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Durchschnitt.png)

## Quotient
Dient zur Simulation eines Allquantors:

Z.B: Welche Programmierer programmieren in aller Sprachen
$$
A  = R_{1} \div R_{2}
$$
![3_DBS_3_Quotient](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Quotient.png)

## Join
Selektion über Kreuzprodukt zweier Relationen:
- Theta-Join ($\theta$-Join): $R$ $\bowtie\atop A \theta B$ $S$
  
  Allgemeiner Vergleich:
  
  $A$ ist ein Attribut von $R$ und $B$ ist ein Attribut von $S$. 
  Dabei ist $\theta$ ein Vergleichsoperator. (z.B. $=, \neq, <, \leq, >, \geq$)
- Equi-Join: $R$ $\bowtie\atop A = B$ $S$
- Natural Join: $R$ $\bowtie$ $S$:
	1. Ein Equi-Join über alle **gleich benannten** Attribute, die in $R$ und $S$ vorkommen.
	2. Gleiche Spalten werden gestrichen. (Projektion)

#### Implementierung mit Hilfe der Grundoperationen
$$
R \bowtie_{A \theta B} S = \sigma_{A \theta B}(R \times S)
$$
![3_DBS_3_Join_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Join_1.png)

# SQL
![3_DBS_3_SQL_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_SQL_1.png)

Hauptunterschied zwischen SQL und rel. Algebra:
- Operationen bei SQL nicht beliebig schachtelbar
- Jeder Operator hat seinen festen Platz
Trotzdem:
- Man kann zeigen, dass jeder Ausdruck in SQL in einen Ausdruck der relationalen Algebra übersetzt werden kann.
- Die feste Anordnung der Operatoren ist also keine wirkliche Einschränkung.
- **SQL ist relational vollstänfig**
Weitere Unterschiede:
- Nicht immer werden Duplikate eliminiert
- zus. Auswertungsmöglichkeiten (z.B. Sortierung, Aggregate)

## SELECT
- Entspricht der **Projektion**
- Aber: Duplikateliminierung nur, wenn das Schlüsselwort **DISTINCT** angegeben ist.
- Syntax: 
  ```sql
	SELECT * FROM... -- Keine Projektion
	SELECT A1, A2, ... FROM... -- Projektion ohne Duplikateliminierung
	SELECT DISTINCT A1, A2, ... FROM... -- Projektion mit Duplikateliminierung
  ```
- Bei der 2. Abfrage kann die Ergebnisrelation also Duplikate haben →  Grund →  Performance 
- Bei den Attributen A1, A2, .. lässt sich angeben...:
	- Ein Attributname einer beliebigen Relation, die in der `FROM`-Klausel angegeben ist.
	- Ein **skalarer Ausdruck**, der Attribute und Konstanten mittels arithmetischer und logischer Operatoren verknüpft.
	- Im Extremfall nur eine Konstante.
	- Aggregationsfunktionen (z.B. `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)
 	- Ein Ausdruck der Form A1 `AS` B1: A2 wird der neue Attributname (Spaltenüberschrift)
**Beispiel**

![3_DBS_3_SQL_SELECT_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_SQL_SELECT_1.png)

## FROM
- Enthält mindestens einen Eintrag der Form $R_{1}$
- Enthält die `FROM`-Klausel mehrere Eintrage, so wird ein kartesisches Produkt gebildet.
- Enthalten zwei versch. Relationen R1, R2 ein Attribut mit gleichem Namen, 
  dann ist dies in der `SELECT`- und `WHERE`-Klausel mehrdeutig.
- Eindeutigkeit durch vorangestellten Relationsnamen: 
  ```sql
	SELECT Mitarbeiter.Name , Abteilung.Name 
	FROM Mitarbeiter, Name 
	WHERE ... 
  ```
- Man kann Schreibarbeit sparen, indem man den Relationsnamen durch ein Kürzel ersetzt:
  ```sql
	SELECT m.Name , a.Name 
	FROM Mitarbeiter m, Name a 
	WHERE ... 
  ```
- Dies lässt sich in der `SELECT`-Klausel auch mit der Sternchennotation kombinieren:
  ```sql
	SELECT m.* , a.Name AS Abteilungsname
	FROM Mitarbeiter m, Abteilung a
	WHERE ... 
  ```
## WHERE

- Entspricht der Selektion der relationalen Algebra
- Enthält genau ein logisches Prädikat $\Phi$ (gibt true oder false zurück)
- Das logische Prädikat besteht aus:
	- Vergleiche zwischen Attributwerten und Konstanten
	- Vergleiche zwischen verschiedenen Attributen
	- Vergleichsprädikate: $=, <, \leq, >, \geq, <>$
	- Test auf *Wert undefiniert*: A1 `IS NULL`/`IS NOT NULL`
	- Inexakter Stringvergleich: A1 `LIKE` ´Datenbank%´
	- A1 `IN` (Werteliste)
- Innerhalb eines Prädikates: Skalare Ausdrücke:
	- Numerische Werte/Attribute mit +.-,*,/ verknüpfbar
	- Strings: char_length, Konkatenation mit ||, substrings
	- Spezielle Operatoren für Datum und Zeit
	- Übliche Klammerregeln
- Einzelne Prädikate können  mit `AND`, `OR`, `NOT` verknüpft werden.
- Idee der Anfrage Auswertung: Alle Tupel des Kartesischen Produktes aus der 
  `FROM`-Klausel werden getestet, ob sie $\Phi$ erfüllen
- Inexakte Stringsuche: A1 `LIKE` ´Datenbank%´:
	- Bedeutet: Alle Datensätze, bei denen Attribut A1 mit dem Präfix "Datenbank" beginnt.
	- % steht für beliebige Zeichenfolge
	- _ steht für ein beliebiges Zeichen

## JOIN
Normalerweise wird der join wie bei der relationalen Algebra als Selektionsbedinung
über dem Kreuzprodukt der beiden Relationen angegeben:
```sql
SELECT * FROM R, S WHERE R.A = S.Ba -- hier wird das Kreuzprodukt gebildet

-- neuer SQL Dialekt:
SELECT * FROM Mitarbeiter m JOIN Abteilung a ON a.ANr = m.ANr
SELECT * FROM Mitarbeiter JOIN Abteilung USING (ANr)
SELECT * FROM Mitarbeiter NATURAL JOIN Abteilung
```
Nach diesem Konstrukt können mit einer `WHERE`-Klausel weitere Bedingungen angegeben werden.

![3_DBS_3_Join_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Join_2.png)

**Beispiele Self-Join:**

![3_DBS_3_SelfJoin_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_SelfJoin_1.png)
![3_DBS_3_SelfJoin_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_SelfJoin_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_SelfJoin_2.png)

## OUTER JOIN
*PROBLEM:*
Beim gewöhnlichen "inner" `JOIN` gehen diejendigen Tupel verloren,
die in einer der beiden Relationen keine Entsprechung haben/keinen Join-Partner haben.

*BEISPIEL:*

![3_DBS_3_OuterJoin_Problem](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_OuterJoin_Problem.png)

*IDEE:*
- Ein Outer Join ergänzt das Join-Ergebnis um die Tupel, die keinen Join-Partner in der anderen Relation haben.
- Das Ergebnis wird mit NULL-Werten aufgefüllt:

![3_DBS_3_OuterJoin_Problem_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_OuterJoin_Problem_1.png)

Aufstellung aller Möglichkeiten:
```sql
[INNER] JOIN -- Nur die Tupel, die einen Join-Partner haben; keine verlustfreie Verknüpfung
LEFT [OUTER] JOIN -- Alle Tupel der linken Relation sind im Ergebnis enthalten und verlustfrei verknüpft
RIGHT [OUTER] JOIN -- Alle Tupel der rechten Relation sind im Ergebnis enthalten und verlustfrei verknüpft
FULL [OUTER] JOIN -- Alle Tupel beider Relationen sind im Ergebnis enthalten und verlustfrei verknüpft
```
![3_DBS_3_OuterJoin_Szenarien](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_OuterJoin_Szenarien.png)

## UNION; INTERSECT; EXCEPT
Üblicherweise werden mit diesen Operationen die Ergebnisse zweier `SELECT-FROM-WHERE`-Blöcke verknüpft.
```sql
SELECT * FROM Mitarbeiter WHHERE Name LIKE 'A%'
UNION
SELECT * FROM Student WHERE Name LIKE 'A%'
```
Es gibt folgende Mengenoperationen:
- `UNION` entspricht der Vereinigung **MIT DUPLIKATEN**
- `UNION ALL` entspricht der Vereinigung **OHNE DUPLIKATE**
- `INTERSECT` entspricht dem Durchschnitt/der Schnittmenge
- `EXCEPT` entspricht der Differenz/Mengendifferenz

Während die relationale Algebra verlangt, dass die beiden Relationen, die verknüpft werden,
das gleiche Schema haben (Name und Wertebereich), ist dies bei SQL nicht der Fall.
SQL verlangt nur **kompatible Wertebereiche**, d.h:
- beide Wertebereiche sind character (Länge usw. egal)
- beide Wertebereiche sind numerisch (Genauigkeit ist egal)
- oder beide Werte sind gleich

Die Namen der Attribute müssen nicht übereinstimmen.

Befinden sich Attribute gleichen Names auf unterschiedliche Positionen,
sind trotzdem nur Positionen maßgeblich.
Mit anderen Worten bedeutet das, dass wenn du zwei Attribute mit dem gleichen Namen in einer SELECT-Anweisung hast, der Ausdruck an der ersten Position im SELECT-Block das Attribute von Bedeutung ist. Wenn es an einer späteren Position wiederholt wird, hat dies keine Auswirkung auf das Ergebnis der Abfrage.

Hier ist ein Beispiel in SQL:
```sql
SELECT id, name, age, name
FROM employees;
```
In diesem Beispiel ist das Attribut name an verschiedenen Positionen in der SELECT-Anweisung, aber nur das erste name wird im Ergebnis zurückgegeben. Der zweite name wird ignoriert.


Mit dem Schlüsselwort `CORRESPONDING` beschränken sich die Operationen automatisch auf die gleich benannten Attribute.

![3_DBS_3_Cooresponding](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Cooresponding.png)

Bei `CORRESPONDING` wird vor der Vereinigung automatisch eine Projektion
bezüglich aller **gleich benannten** Attribute durchgeführt.

Dies kann man besser durch explizites Aufzählen der Attribute in der `SELECT`-Klausel erreichen:

![3_DBS_3_Cooresponding_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Cooresponding_1.png)

Bei `CORRESPONDING` ist ggf. die Reihenfolge der Attribute der erstgenannten Teilanfrage **maßgeblich**:

![3_DBS_3_Cooresponding_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Cooresponding_2.png)

# Änderungsoperationen
- modifizieren den Inhalt eines oder mehrerer Tupel
- Wir unterschieden: 
  ```sql
  INSERT -- Einfügen neuer Tupel in Relation
  DELETE -- Löschen von Tupeln aus Relation
  UPDATE -- Ändern von Attributwerten in Tupeln
  ```
- Diese Operationen sind verfügbar als...
	- Einzeloperationen (Ein Tupel Operationen) →  Erfassung  neues Mitarbeiters
	- Batch-Operationen (Mehr Tupel Operationen) →  Erhöhung aller Gehälter um 5%

## UPDATE
Syntax
```sql
UPDATE relation
set attribut1 = ausdruck1
	[ , attribut2 = ausdruck2, ...]
[WHERE bedingung]
```

→  In allen Tupeln der Relation, die die Bedingung erfüllen, werden die angegebenen Attribute geändert.

> :memo: **Note:** `UPDATE` ist eine Mehr Tupel Operation:
```sql
UPDATE Angestellte
SET Gehalt = Gehalt * 1.05
```

Um sich auf ein einzelnes Tupel zu beschränken benutzt man das Schlüsselwort `WHERE`:
```sql
UPDATE Angestellte
SET Gehalt = Gehalt * 1.05
WHERE PNr = 7
```
Der alte Attribut Wert kann bei der Berechnung des neuen Attribut Wertes verwendet werden:
```sql
UPDATE Angestellte
SET Gehalt = Gehalt * 1.05
WHERE Gehalt < 1000
```

## DELETE
Syntax
```sql
DELETE FROM relation
[WHERE bedingung]
```

Löscht alle Tupel, die die Bedingung erfühlen. Ohne Bedingung werden alle Tupel gelöscht.

## INSERT
Zwei unterschiedliche Formen:
- Einfügen konstanter Tupel (Ein Tupel Operation)
- Einfügen berechneter Tupel (Mehr Tupel Operation)

Syntax
```sql
INSERT INTO relation (attribut1, attribut2, ...)
VALUES (ausdruck1, ausdruck2, ...)
```
oder
```sql
INSERT INTO relation
VALUES (ausdruck1, ausdruck2, ...)
```

**Wirkung:**
Ist die optionale Anzahl hinter dem Relationennamen angegeben, dann...
- können unvollständige Tupel eingefügt werden: 
  nicht aufgeführte Attribute erhalten den Wert `NULL` belegt.
- werden die Werte durch die Reihenfolge in der Attributsliste zugeordnet

![3_DBS_3_Insert_Beispiel](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Insert_Beispiel.png)
![3_DBS_3_Insert_Beispiel_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_Insert_Beispiel_1.png)

### Einfügen berechneter Tupel
Syntax
```sql
INSERT INTO relation  [(attribut1, attribut2, ...)]
	(SELECT  ... FROM ... WHERE)
```
**Wirkung:**
- Alle Tupel des Ergebnisses der `SELECT`-Anweisung werden in die Relation eingefügt.
- Die optionale Attributliste hat dieselbe Bedeutung wie bei der Ein Tupel Operation.

![3_DBS_3_INSERT_Berechneter_Tupel](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_3_INSERT_Berechneter_Tupel.png)
