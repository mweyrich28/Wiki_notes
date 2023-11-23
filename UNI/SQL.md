# SQL 

## CREATE TABLE

```sql
CREATE TABLE n
(
	a1, d1, c1,
	a2, d2, c2,
	...
	an, dn, cn,
)
```
- $n$ ist der Name der Relation
- $a_{i}$ ist der Name des $i$-ten Attributs
- $d_{i}$ ist der Name der Domäne (also des Typs) des $i$-ten Attributs
- $c_{i}$ ist eine Liste von Constraints (Einschränkungen) für das $i$-te Attribut
Bsp:

```sql
CREATE TABLE Student
(
	MatrikelNr INTEGER NOT NULL,
	Name VARCHAR(30) NOT NULL,
	Vorname VARCHAR(30) NOT NULL,
	Geburtsdatum DATE,
	PRIMARY KEY (MatrikelNr)
)
```
Zusätzliche Constraints:

```sql
CREATE TABLE T
(
	Attribut1 Typ1 NOT NULL, -- NOT NULL: Wert darf nicht NULL sein
	Attribut2 Typ2 UNIQUE, -- UNIQUE: Wert muss eindeutig sein
	Attribut3 Typ3 DEFAULT Wert, -- DEFAULT: Wert wird gesetzt, wenn kein Wert angegeben
	Attribut4 Typ4 CHECK (Bedingung), -- CHECK: Wert muss Bedingung erfüllen
	Attribut5 Typ5 REFERENCES Tabelle (Attribut) -- REFERENCES: Wert muss in Tabelle Attribut vorkommen
	Attribut6 Typ6 PRIMARY KEY -- PRIMARY KEY: Wert muss eindeutig sein (nicht bei zusammengesetzten Schlüsseln)
)
```
## SQL Integritätsbedingungen
Zusätze, die keinem einzelen Attribute zugeordnet sind, stehen mit Komma abgetrennt in extra Zeile:

```sql
CREATE TABLE T
(
	...
	PRIMARY KEY (Attribut1, Attribut2, ...), -- Zusammengesetzter Primärschlüssel
	UNIQUE (Attribut1, Arrtibut2, ...), -- Zusammengesetzter Schlüsselkandidat 
	FOREIGN KEY (Attribut1, Atttribut2, ...) REFERENCES T1 (B1, B2, ...) -- Verweis auf zusammengesetzten Schlüssel in Relation T1
															   -- Fehlt (B1, B2, ...) hinter T1 so wird automatisch (Attribut1, Attribut2, ...) verwendet
	CHECK f
)
```
Wenn Tabelle A einen Fremdschlüssel hat, der auf Tabelle B verweist und die Option "ON DELETE CASCADE" festgelegt ist, bedeutet dies, dass beim Löschen eines Datensatzes in Tabelle B automatisch auch alle zugehörigen Datensätze in Tabelle A gelöscht werden.
In diesem Fall hat Tabelle A einen Fremdschlüssel, der auf das Attribut "KNr" in Tabelle B verweist. Wenn ein Datensatz in Tabelle B gelöscht wird, werden alle zugehörigen Datensätze in Tabelle A automatisch gelöscht, um die referenzielle Integrität zu gewährleisten.
Dieser Mechanismus ist nützlich, um sicherzustellen, dass keine verwaisten Datensätze in der Datenbank verbleiben und die Beziehungen zwischen den Tabellen konsistent bleiben.


## Schlüssel-Definitionen
```sql
	PRIAMRY KEY (a1, a2) -- definiert Primärschlüssel
	UNIQUE (a3, a4) -- definiert weiteren Schlüsselkandidat
	FORIEGN KEY (a5, a6) REFERENCES Tabelle (b1, b2) -- definiert Fremdschlüssel
```
Tupel in A ohne gültigen Partner in B nicht erlaubt

:warning: Warning: Ohne weiteren Zusatz nicht möglich, das Tupel in B, auf die durch in Tupel A verwiesen wird, zu löschen oder die Werte von b1,b2 zu verändern.

Löschen eines Tupels in B mit Referenzen nicht möglich.

Es gibt aber verschiedene Zusätze:

```sql
	FOREIGN KEY (a5, a6) REFERENCES Tabelle (b1, b2) 
	ON DELETE CASCADE -- Löschen eines Tupels in B mit Referenzen in A löscht auch Tupel in A
	--
	ON UPDATE CASCADE -- Ändern eines Tupels in B mit Referenzen in A ändert auch Tupel in A
	--
	ON DELETE SET NULL -- Löschen eines Tupels in B mit Referenzen in A setzt Referenz in A auf NULL
```
## Beispiel Tabellendefinition

```sql
CREATE TABEL Lehrveranst
(
	LNr INTEGER 	NOT NULL,
	VNr INTEGER 	NOT NULL,
	Titel VARCHAR(50),
	Semester VARCHAR(20)	NOT NULL,
	PRIMARY KEY (VNr, Semester)
)
-- Alternativ mit einfachen PRIMARY KEYS:
CREATE TABEL Lehrveranst
(
	LNr INTEGER 	PRIMARY KEY,
	VNr INTEGER 	NOT NULL,
	Titel VARCHAR(50),
	Semester VARCHAR(20)	NOT NULL
)
```
## Beispiel Tabellendefinition 2
```sql
CREATE TABLE Dozenten
(
	DNr INTEGER PRIMARY KEY,
	NAme VARCHAR(50),
	Geburt DATE
)
-- Verwendung von Fremdschlüsseln
CREATE TABLE Haelt
(
	DOZENT INTEGER REFERENCES Dozenten (DNr)
				   ON DELETE CASCADE,
	VNr INTEGER NOT NULL,
	Semester VARCHAR(20) NOT NULL,
	PRIMARY KEY (VNr, Semest(Dozent, VNr, Semester), -- Zusammengesetzter Schlüssel
	FORIEGN KEY (VNr, Semester) REFERENCES Lehrveranst -- Verweis auf zusammengesetzten Schlüssel in Relation Lehrveranst
)
```
:memo: Note: Das Schlüsselwort ON DELETE CASCADE in Haelt führt dazu, dass beim Löschen eines Dozenten auch entsprechende Tupel in Haelt gelöscht werden.
Wenn wir dieses Schlüsselwort nicht angeben, dann ist das Löschen eines Dozenten nicht möglich, solange es noch entsprechende Tupel in Haelt gibt.

## ALTER TABLE: DROP, ADD, MODIFY
```sql
	 DROP TABLE n1 -- Relationen-Schema n1 wird mit allen evtl. enthaltenen Tupeln gelöscht.
	 ALTER TABLE n1 ADD (a1 d1 c1, ...) -- Attribut a1 mit Domäne d1 und Constraints c1 wird zu Relation n1 hinzugefügt.
	 ALTER TABLE n1 DROP (a1, a2, ...) -- Attribut a1, a2, ... wird aus Relation n1 gelöscht.
	 ALTER TABLE n1 MODIFY (a1 d1 c1, ...) -- Attribut a1 wird in Relation n1 geändert.
```
Hier ist ein allgemeiner Ansatz, um alle Tabellen zu löschen, ohne die Integrität zu verletzen:
1. Beginne mit der Tabelle, die keine Fremdschlüsselreferenzen hat.
2. Lösche diese Tabelle.
3. Fahre mit den verbleibenden Tabellen fort, wobei du diejenigen zuerst löschst, die auf die bereits gelöschten Tabellen verweisen.
4. Wiederhole Schritt 3, bis alle Tabellen gelöscht sind.
Indem du die Tabellen in der richtigen Reihenfolge löschst, sorgt das "delete on cascade" dafür, dass die referenzierten Datensätze in den anderen Tabellen automatisch gelöscht werden, ohne die Integrität zu verletzen.
Es ist jedoch wichtig, vorsichtig zu sein und sicherzustellen, dass du die richtige Reihenfolge der Tabellenlöschung befolgst, um unerwünschten Datenverlust zu vermeiden. 


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
