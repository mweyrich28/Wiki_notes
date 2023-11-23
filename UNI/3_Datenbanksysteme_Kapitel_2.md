# Das Relationale Datennmodell
**Slides**: [Datenbanken Kapitel 2](file:///home/malte/OneDriver/01_Studium/3.Semester/Datenbanken/Slides/dbs1_02.pdf)

## Domain Definition
- Ein Wertebereich (oder Typ)
- Logisch zusammengehörige Menneg von Werten
z.B:
$$
\begin{align}
	D_{1} &= \text{Integer}\\
	D_{2} &= \text{String}\\ 
	D_{3} &= \text{Date}\\ 
	D_{4} &= \text{\{rot, gelb, grün, blau\}}\\ 
	D_{5} &= \left\{1,2,3\right\}
\end{align}
$$
→  Kann eine endliche oder unendliche **Kardinalität** haben

## Kartesisches Produkt
Das kartesische Produkt zweier Mengen $A$ und $B$ ist die Menge 
aller geordneten Paare $(a,b)$ mit $a \in A$ und $b \in B$ 
(Kombinationen aller Elemente aus $A$ und $B$)

## Relationen
> Relation $R$ ist Teilmenge des kartesischen Produkts von $k$ Domains $D_{1}, D_{2},\dots, D_{n}$
> 
> $R \subseteq D_{1} \times D_{2} \times \dots \times D_{n}$

Beispiel: $\le$ Relation:
$$
R_{1}=\left\{(x,y) \in \mathbb{N} \times \mathbb{N} | x \le y\right\}
$$

Es gibt endliche und unendliche Relationen (wenn mind. eine Domain unendlich ist)

→  In DBS nur endliche Relationen

- Die einzelnen Domains lassen sich als **Spalten einer Tabelle** verstehen und 
  werden als Attribute bezeichnet.
- Für $R \subseteq D_{1}\times \dots \times D_{n}$ ist $n$ der **Grad(Stelligkeit)**
- Reihenfolge der Tupel spielt keine Rolle
- Reihenfolge der Attribute ist wichtig


### Relationen Schema
Alternative Definition in DBS:
**Relation ist Ausprägung einers Schemas**

#### Geordnetes Relationsschema:
- $k$-Tupel aus Domains (Attribute)
- Attribute werden anhand ihrer Position im Tupel referenziert 
- Attribute können zusätzlich einen Attribute-Namen haben
- $R=(A_{1}:D_{1}, \dots, A_{k}:D_{k})$
#### Domänen-Abbildung (ungeordnetes Relationsschema):
- Relationsschema $R$ ist Menge von Attributnamen
- Jedem Attributnamen $A_{i}$ ist Domäne $D_{i}$ zugeordnet
- Attribute werden anhand ihres Namens referenziert
- $R = \left\{A_{1},\dots, A_{k}\right\}$ mit $dom(A_{i}) = D_{i}, 1 \le i \le k$

**BEISPIEL:**
![3_DBS_2_relationsSchema](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_2_relationsSchema.png)


# Schlüssel
## Formale Definition
> Eine Teilmenge $S$ der Attribute eines Relationsschemas $R$
> $S \subseteq R$ heißt **Schlüssel** von $R$, wenn gilt:

1. **Eindeutigkeit:** Keine Ausprägung von $R$ kann zwei 
   verschiedene Tupel erhalten, die sich in allen Attributen von $S$ 
   gleichen
2. **Minimalität:** Keine echte Teilmenge von $S$ erfüllt die Eindeutigkeitseigenschaft: 
   $T \subseteq S \implies T = S$

## Superschlüssel / Minimale Menge
Eine Menge $S \subseteq R$ heißt **Superschlüssel/Superky**, wenn sie 
die eindeutigkeitseigenschaft erfüllt.

Der Begriff des Superschlüssels impliziert keine Aussage über Minimalität.

Minimale Menge $M$ bezüglich Eigenschaft $B$ gdw. es keine echte Teilmenge 
von $M$ gibt, die $B$ erfüllt.

→  Ein Schlüssel ist ein minimaler Superschlüssel

![3_DBS_2_Schlüssel](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_2_Schlüssel.png)
![3_DBS_2_Schlüssel_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_2_Schlüssel_1.png)
![3_DBS_2_Schlüssel_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_2_Schlüssel_2.png)


## Primärschlüssel
- Minimalität bedeutet: Keine überflüssigen Attribute sind enthalten (d.h. solche 
  die zur Eindeutigkeit nichts beitragen)
- Manchmal gibt es mehrere verschiedene Schlüssel:
	- {LNr}
	- {VNr, Semester}
- Man wählt eine dieser Kandidaten als **Primärschlüssel** aus (SQL: Primary Key) aus
- Attribut(e) das auf einen Schlüssel einer anderen Relation verweist 
  heißt **Fremdschlüssel** (SQL: Foreign Key):
  ```sql
  CREATE TABLE Haelt
  (
  	DOZENT INTEGER REFERENCES Dozenten (DNr), -- Verweis auf Schlüssel DNr in Relation Dozenten
  	VNr INTEGER NOT NULL,
  	Semester VARCHAR(20) NOT NULL,
  	PRIMARY KEY (VNr, Semester) -- Zusammengesetzter Schlüssel
  )
  ```

## Schlüssel Semantische Eigenschaft
Die Eindeutigkeit bezieht sich nicht auf die aktuelle Ausprägung der Relation $r$

Sondern immer auf die **Semantik** der realen Welt:

![3_DBS_2_SchlüsselSemankik](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_2_SchlüsselSemankik.png)
# SQL Tabellendefinition
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
## Schlüssel-Definitionen
![2_DBS_2_SchlüsselDefinitionen_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/2_DBS_2_SchlüsselDefinitionen_1.png)
```sql
	PRIAMRY KEY (a1, a2) -- definiert Primärschlüssel
	UNIQUE (a3, a4) -- definiert weiteren Schlüsselkandidat
	FORIEGN KEY (a5, a6) REFERENCES Tabelle (b1, b2) -- definiert Fremdschlüssel
```
Tupel in A ohne gültigen Partner in B nicht erlaubt

> :warning: **Warning:** Ohne weiteren Zusatz nicht möglich, das Tupel in B, auf die durch in Tupel A verwiesen wird, zu löschen oder die Werte von b1,b2 zu verändern.

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

#### Beispiel Tabellendefinition
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
#### Beispiel Tabellendefinition 2
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

> :memo: **Note:** Das Schlüsselwort `ON DELETE CASCADE` in Haelt führt dazu, dass beim Löschen eines Dozenten auch entsprechende Tupel in Haelt gelöscht werden.
> Wenn wir dieses Schlüsselwort nicht angeben, dann ist das Löschen eines Dozenten nicht möglich, solange es noch entsprechende Tupel in Haelt gibt.

### ALTER TABLE: DROP, ADD, MODIFY
```sql
	 DROP TABLE n1 -- Relationen-Schema n1 wird mit allen evtl. enthaltenen Tupeln gelöscht.
	 ALTER TABLE n1 ADD (a1 d1 c1, ...) -- Attribut a1 mit Domäne d1 und Constraints c1 wird zu Relation n1 hinzugefügt.
	 ALTER TABLE n1 DROP (a1, a2, ...) -- Attribut a1, a2, ... wird aus Relation n1 gelöscht.
	 ALTER TABLE n1 MODIFY (a1 d1 c1, ...) -- Attribut a1 wird in Relation n1 geändert.
```
