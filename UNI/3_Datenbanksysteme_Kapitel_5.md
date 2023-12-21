# Kapitel 5 - Sortieren, Gruppieren und Views in SQL
**SLIDES:** [Datenbanken 5](file:///home/malte/OneDriver/01_Studium/3.Semester/Datenbanken/Slides/dbs1_05.pdf)

## Sortieren
- In SQL mit `ORDER BY`-Klausel:
	- `SELECT ... FROM ... WHERE ... ORDER BY A1, A2, ...;`
- Bei mehreren Attributen: lexikographische Ordnung: 

  ![3_DBS_5_LexOrdnung](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_LexOrdnung.png)
- Steht am Ende einer Anfrage
- Nach Attribut kann man auch `ASC` (aufsteigend) oder `DESC` (absteigend) angeben
- Nur Attribute der `SELECT ...`-Klausel dürfen in `ORDER BY`-Klausel vorkommen
- **Beispiel auf Slide 3**

## Aggrgation
- Berechnet Eigenschaften ganzer Tupel-Mengen
- Arbeitet also Tupel übergreifend
- Aggregatfunktion in **SQL**:
	- `COUNT` (Anzahl der Tupel bzw. Werte)
	- `SUM` (Summe der Werte einer Spalte)
	- `AVG` (Durchschnitt der Werte einer Spalte)
	- `MIN` (kleinster Wert einer Spalte)
	- `MAX` (größter Wert einer Spalte)
- Aggregate können sich erstrecken:
	- auf das gesamte Abfrageergebnis
	- auf Teilgruppen von Tupeln
- **Aggregatfunktionen stehen in der `SELECT`-Klausel!**
- **Beispiel auf Slide 5**
- Ergebnis ist immer ein einziges Tupel
- Aggregate wie `MIN` und `MAX` sind einfaches Mittel 
  um Eindeutingkeit bei Subqueries herzustellen
- `NULL`-Werte werden ignoriert (auch bei `COUNT`)
- Eine Duplikateliminaton kann erzwungen werden durch:
	- `COUNT (DISTINCT KName)` zählt nur verschiedene Kunden
	- `COUNT (ALL KName)` zählt alle Kunden außer `NULL`
	- `COUNT (KName)` →  indentisch zu `COUNT (ALL KName)`
	- `COUNT (*)` zählt alle Tupel des Abfrageergebnisses (macht nur bei `NULL` Werten einen Unterschied)

## Gruppierung
- Aufteilung der Ergebnis-Tupel in Gruppen
- Ziel: Aggregation
- Beispiel: 
  
  ![3_DBS_5_Gruppierung](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Gruppierung.png) 
  
  ![3_DBS_5_Gruppierung_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Gruppierung_2.png)

- Syntax in SQL: 
  ```sql
  SELECT ...
  FROM ...
  [WHERE ...]
  [GROUP BY A1, A2, ...]
  [HAVING ...]
  [ORDER BY ...]
  ```
- Wegen Relationen Eigenschaft der Ergebnisses Einschränkungen der `SELECT` Klausel. 
  Erlaubt sind:
  - Attribute aus der Gruppierungsklausel
  - Aggregationsfunktionen auch über andere Attribute, z.B. `COUNT(*)`
  - in der Regel `SELECT * FROM ... GROUP BY ...` nicht erlaubt 
	Beispiel nicht möglich: 
	
	![3_DBS_5_Gruppierung_3](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Gruppierung_3.png)
  
### Gruppierung mehrerer Attribute
Etwa sinnvolll in folgener Situation:

![3_DBS_5_Gruppierung_4](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Gruppierung_4.png)

Oft künstlich wegen `SELECT`-Einschränkung:

![3_DBS_5_Gruppierung_5](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Gruppierung_5.png)

- Nicht möglich obwohl **AName** und **ANr** funktional Abhängig: 
  
  ~~`SELECT ANr, AName, SUM(Gehalt) FROM ... WHERE ... GROUP BY ANr`~~
  
  →  In SQL müssen alle nicht-aggregierten Spalten, die in der SELECT-Liste verwendet werden,
  entweder in der GROUP BY-Klausel enthalten sein oder durch eine Aggregatfunktion gruppiert werden. 
  Das liegt daran, dass die GROUP BY-Klausel definiert, wie die Datensätze vor der Anwendung der Aggregatfunktionen gruppiert werden sollen. Wenn Spalten in der SELECT-Liste sind,
  die nicht in der GROUP BY-Klausel enthalten sind und keine Aggregatfunktion auf sie angewendet wird,
  ist es nicht klar, welchen einzelnen Wert SQL für diese Spalten zurückgeben soll,
  da sie potenziell mehrere Werte pro Gruppe haben könnten.

  Um die Abfrage korrekt zu gestalten, müsstest du entweder AName auch in die GROUP BY-Klausel aufnehmen oder eine Aggregatfunktion wie MAX oder MIN auf AName anwenden,
  wenn du sicher bist, dass AName für jede eindeutige ANr immer denselben Wert hat. Alternativ könntest du eine separate Aggregatfunktion auf AName anwenden,
  um einen einzigen repräsentativen Wert zu erhalten,
  der der Gruppe entspricht. 
  
- Aber wegen der funktionalen abh. identisch mit: 
  
  `SELECT ANr, AName, SUM(...) FROM ... WHERE ... GROUP BY ANr, AName`
- Weitere Möglichkeit (ebenfalls wegen Abhängigkeit): 
  
  `SELECT ANr, MAX(AName), SUM(...) FROM ... WHERE ... GROUP BY ANr`

Angenommen, du hast eine Tabelle mit Spalten wie ANr, AName und Gehalt.
Wenn du versuchst, ANr und AName zu selektieren und gleichzeitig SUM(Gehalt) zu verwenden, 
müsstest du normalerweise AName in die GROUP BY-Klausel aufnehmen, da es sich um eine nicht-aggregierte Spalte handelt.

Das Beispiel, das du gegeben hast, zeigt, dass AName und ANr funktional abhängig sind, was bedeutet,
dass für jede eindeutige ANr der Wert von AName eindeutig ist. In solchen Fällen könntest du tatsächlich 
AName weglassen und ANr mit einer Aggregatfunktion wie MAX verwenden, um eine der Regeln für GROUP BY zu erfüllen.


## Die Having-Klausel
> :zap: **Motivaion:**
> Ermittle das Gesamt-Einkommen in jeder Abteilung, die mind. 5 Mitarbaiter hat

So geht es nicht mit SQL:
```sql
SELECT ANr, SUM(Gehalt)
FROM Mitarbeiter
WHERE COUNT(*) >= 5 -- Fehler!!!!!!!!!!!!!!!
GROUP BY ANr
HAVING COUNT(*) >= 5; -- Stattdessen HAVING
```
Grund: Gruppierung wird erst nach `SELECT-FROM-WHERE` durchgeführt.
 
## Auswertung der Gruppierung
Am folgenden Bsp:
```sql
SELECT A, SUM(D)
FROM ... WHERE ...
GROUP BY A, B
HAVING SUM(D) < 10 AND MAX(C) = 4
```
![3_DBS_5_Auswertung](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Auswertung.png)

![3_DBS_5_Auswertung_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Auswertung_2.png)


# Architektur eines DBS

**Drei Ebenen Architektur** zur Realisierung von:
- Physischer Datenunabhängigkeit
- Logischer Datenunabhängigkeit (nach ANSI/SPARC)

![3_DBS_5_Architektur](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_Architektur.png)

## Externe Ebene
- Gesamt-Datenbestand ist angepasst, so dass jede Anwendungsgruppe 
  nur die Daten sieht, die sie...
	- sehen will (**Übersichtlichkeit**)
	- sehen soll (**Datenschutz**)
- Logische Datenunabhängigkeit

In SQL:

Realisierung durch **Sicht**(View):

### Sicht (View)
- Virtuelle Relation
- Was bedeutet virtuell?
	- Die **View** sieht für den Benutzer aus wie eine Relation:
		- `SELECT ... FROM ... View1, Relation2, ... WHERE ...`
		- mit Einschänkung auch `INSERT`, `DELETE`, `UPDATE`
	- Aber die Relation ist nicht **real existent/gespeichert**; 
	  
	  Inhalt ergibt sich durch Berechnung aus anderen Relationen
- Besteht aus 2 Teilen:
	- Relationenschema für die **View** (nur rudimentär)
	- Berechnungsvorschrift, die den Inhalt festlegt: 
	  
	  SQL-Anfrage mit `SELECT ... FROM ... WHERE ...`

### Viewdefinition in SQL
Das folgende DDL-Kommando erzeugt eine View:
- `CREATE [OR REPLACE] VIEW VName [(A1, A2, ...)] AS SELECT ... ;`

Beispiel: Eine virtuelle Relation Buchhalter, nur mit den Mitarbeitern der Buchhaltungsabteilung:
```sql
CREATE VIEW Buchhalter AS 
SELECT PNr, Name, Gehalt FROM Mitarbeiter WHERE ANr = 01;
```

Die View *Buchchalter* wird erzeugt:

![3_DBS_5_View](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_View.png)

### Konsequenzen
Automatisch sind in dieser View alle Tupel der **Basisrelation**,
die die **Selektionsbedinung** erfüllen

An diese können beliebige Anfragen gestellt werden, auch in 
Kombination mit anderen Tabellen (`JOIN`) etc:
- `SELECT * FROM Buchhalter WHERE Name LIKE 'B%'`

In Wirklicheit wird lediglich die View-Definition in die Anfrage
eingesetzt und dann Ausgewertet:

![3_DBS_5_View_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_5_View_2.png)

Bei Updates in der **Basisrelation** (Mitarbeiter) <span style="color:#cc241d;">ändert sich auch die virtuelle Relation</span>

Umgekehrt können (mit Einschränkungen) auch Änderungen an der View durchgeführt werden,
die sich auf die Basisrelation auswirken

Eine View kann selbst wieder als Basis für eine View dienen (View-Hierarchie)

#### Löschen einer View
- `DROP VIEW VName;`

### In Views erlaubte Konstrukte
Folgende Konstrukte sind in Views erlaubt:
- Selektion und Projektion (inkl. Umbenennung von Attributen, Arithmetik)
- Kreuzprodukt und JOIN
- Vereinigung, Differenz, Schnitt
- Gruppierung und Aggregation
- Die verschiedenen Arten von Subqueries

> :warning: **Warning:** Nicht erlaubt sind: **Sortierung**

### Insert, Delete, Update auf Views
**Logische Datenunabhängigkeit**:
- Die einzelnen Benutzer-/Anwendungsgruppen sollen ausschließlich über
  das externe Schema (d.h Views) auf die Datenbank zugreifen (Übersicht, Datenschutz)
- Insert, Delete, Update auf Views erforderlich
**Effekt-Komformität**
- View soll dich verhalten wie eine gewöhnliche Relation
- z.B. nach Einfügen eines Tupels muss das Tupel in der View erscheinen usw.
**Mächtigkeit des View-Mechanismus**
- Join, Aggregation, Gruppierung usw.
- Bei komplexen Views Effekt-Konformität schwer zu erreichen bis unmöglich
**Wir untersuchen die wichtgsten Operationen in der View Definition auf diese Effekte:**
- Projektion
- Selektion
- Join
- Aggregation und Gruppierung
**Wir sprechen von Projektions-Sichten usw**
- Änderung auf Projektions-Sicht muss in Änderung der Basisrelationen transformiert werden

### Projektionssichten
**Laufendes Beispiel:**
- MGA (Mitarbeiter, Gehalt, Abteilung)
- AL (Abteilung, Leiter)
```sql
CREATE VIEW MA as
SELECT Mitarbeiter, Abteilung
FROM MGA
```
Hier gibt es keine Probleme beim Löschen:
```sql
DELETE FROM MA WHERE Mitarbeiter = ...
→  DELETE FROM MGA WHERE Mitarbeiter = ...
```

Bei `INSERT` müssen wegprojizierte Attribute durch `NULL` ersetzt oder
bei der Tabellendefinition festgelegte `DEFAULT`-Werte verwendet werden:
```sql
INSERT INTO MA VALUES ('Weber', 001)
→  INSERT INTO MGA VALUES ('Weber', NULL, 001)
```
Problem bei der Duplikatelimination (`SELECT DISTNCT`):
Keine eindeutige Zuordnung zwischen Tupeln der View und der Basisrelation

Bei Arithmetik in der `SELECT`Klausel: Rückrechnung wäre erforderlich:
```sql
CREATE VIEW P AS SELECT 3*x*x*x+2*x*x+x+1 AS y FROM A
```
Hier wäre das folgende Update problematisch:
→  `UPDATE P SET y = 0 WHERE ...`

→  Kein `INSERT`/`DELETE`/`UPDATE` bei `DISTINCT`/Arithmetik

### Selektions-Sichten
**Beispiel:**
```sql
CREATE VIEW MG AS
SELECT * FROM MGA
WHERE Gehalt > 20
```
- Beim Ändern und Einfügen kann es passieren, dass ein 
  Tupel aus der View verschwindet, weil es die Selektionsbedingung nicht mehr erfüllt:
  
  `UPDATE MG SET GEHALT = 19 WHERE MITARBEITER = 'HUBER'`
- Huber ist danach nicht mehr in MG
- Dies bezeichnet man als **Tupel-Migration**:
  
  Tupel verschwindet, taucht aber dafür vielleicht in einer anderen View auf
- Dies ist manchmal erwünscht
- Manchmal aber auch nicht (Datenschutz)
- Deshalb in SQL folgendes möglich: 
  ```sql
  CREATE VIEW MG AS
  SELECT * FROM MGA
  WHERE Gehalt > 20 
  WITH CHECK OPTION 
  ```
 Tupel-Migration wird dann unterbunden: Fehlermeldung 
 bei `UPDATE MG SET GEHALT = 19 WHERE MITARBEITER = 'HUBER'`

### Join-Views
**Beispiel:**
```sql
CREATE MGAL AS
SELECT Mitarbeiter, Gehalt, MGA.Abteilung, Leiter
FROM MGA, AL
WHERE MGA.Abteilung = AL.Abteilung
```
- `INSERT` in diese View nicht eindeutig übersetzbar:
	- `INSERT INTO MGAL VALUES ('Schuster', 30, 001, 'Boss')` 
	  
	  →  `INSERT INTO MGA VALUES ('Schuster', 30, 001)` 
	  
	  Wenn kein Tupel (001, 'Boss') in AL existiert:
	  
	  →  `INSERT INTO AL VALUES (001, 'Boss')`
	  
	  →  `UPDATE AL SET Leiter = 'Boss' WHERE Abteilung = 001`
	  
	  Oder Fehlermeldung?
- Daher: Join-Views in SQL nicht updatebar


### Aggregation, group by, Subquery
Auch bei Aggregation und Gruppierung ist es nicht möglich, eindeutig auf 
Änderungen in der Basisrelation zu schließen

Subqueries sind unproblematisch, sofern sie keinen
Selbstbezug aufweisen (Tabelle in from-Klausel der View wird
nochmals in der Subquery verwendet)

> :eight_spoked_asterisk: **Definition:** Eine View, die keiner der angesprochenen
> Problemkassen angehört, heißt <span style="color:#cc241d;">Updatable View</span>.
> Insert, Delete und update sind dann möglich

### Materialisierte View
**Begriffserklärung:**
- Materialisierte View = keine virtuelle Relation, sondern real gespeichert
  
  (der Inhalt der Relation wurde aber durch eine Anfrage an anderen Relationen und Views ermittelt)
  
  →  In SQL erreichbar durch Anlage einer Tabelle *MVName* und Einfügen der Tupel mit:
  
  `INSERT INTO MVName (SELECT ... FROM ... WHERE ...)`
- Bei Änderungen in den Basisrelationen muss die View aktualisiert werden, es gibt keine automatische Änderung in
  *MVName* und umgekehrt
- DBS bietet oft auch spezielle Konstrukte zur Aktualisierung (**Snapshot, Triger**), KEIN STANDARD SQL
- Der Begriff View bedeutet nicht Materialisierte View


## Rechtevergabe
Basiert in SQL auf Relationen bzw. Views

Syntax:

```sql
GRANT Rechtsliste
ON Relation
TO Benutzerliste
[WITH GRANT OPTION]
```

Rechteliste:
- `ALL [PRIVILEGES]`
- `SELECT, INSERT, DELETE` (mit Komma getrennt)
- `UPDATE` (optional in Klammern: Attributliste)

Benutzerliste:
- `PUBLIC` (alle Benutzer)
- Benutzernamen (mit Passwort identifiziert)

Grant Option:
- Recht das entsprechende Privileg an andere Benutzer zu vergeben

Rücknahme von Rechten:
```sql
REVOKE Rechtsliste
ON Relation
FROM Benutzerliste
[RESTRICT] -- Abbruch, falls Rechte bereits weitergegeben
[CASCADE] -- Propagierung der Revoke-Anweisung
```
