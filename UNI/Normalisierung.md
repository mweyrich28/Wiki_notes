----

:dbs:normalisierung:normalisierung_datenbanken:

----

https://www.youtube.com/watch?v=aCXKT4ycAbQ

→ Will Anomalien vermeiden
→ Regeln müssen einfach stupide angewendet werden 
→ Normalformen bauen aufeinander auf

# Die nullte Normalform
**In der nullten Normalform befinden sich alle Daten unnormiert in einer einzigen Tabelle.**

| BestellNummer | Datum      | Name           | GebDatum   | Adresse                      | ArtNr | ArtName  | Preis |
|---------------|------------|----------------|------------|------------------------------|-------|----------|-------|
| 122           | 23.04.2021 | Max Mustermann | 28.03.2003 | Fliederweg 22 82031 Grünwald | 1     | Monitor  | 200€  |
| 122           | 23.04.2021 | Max Mustermann | 28.03.2003 | Fliederweg 22 82031 Grünwald | 2     | Haus     | 2000€ |
| 122           | 23.04.2021 | Max Mustermann | 28.03.2003 | Fliederweg 22 82031 Grünwald | 3     | Hamster  | 123€  |
| 123           | 24.04.2021 | Jörg Mann      | 01.01.1999 | Königsstraße 1 80335 München | 4     | Maus     | 20€   |
| 123           | 24.04.2021 | Jörg Mann      | 01.01.1999 | Königsstraße 1 80335 München | 5     | Keyboard | 1000€ |



# Die erste Normalform
**Bei einer Tabelle der ersten Normalform müssen alle Attribute atomar sein.**

> :eight_spoked_asterisk: **Definition:** ***Atomar***
> 
> Atomare Attribute können nicht weiter in kleinere Attribute zerlegt werden und sind somit nicht weiter zerlegbar:
>
> Zum Beispiel kann hier `Name` in `Vorname` und `Nachname` zerlegt werden.
> Die Adresse kann in `Straße`, `Hausnummer`, `PLZ` und `Ort` zerlegt werden.

Neue Tabelle mit nur atomaren Attributen:

| `BestellNummer` :key: | `Datum`    | `Vorname` | `Nachname` | `GebDatum` | `Straße`       | `Plz` | `Ort`    | `ArtNr` | `ArtName` | `Preis` |
|-----------------------|------------|-----------|------------|------------|----------------|-------|----------|---------|-----------|---------|
| 122                   | 23.04.2021 | Max       | Mustermann | 28.03.2003 | Fliederweg 22  | 82031 | Grünwald | 1       | Monitor   | 200€    |
| 122                   | 23.04.2021 | Max       | Mustermann | 28.03.2003 | Fliederweg 22  | 82031 | Grünwald | 2       | Haus      | 2000€   |
| 122                   | 23.04.2021 | Max       | Mustermann | 28.03.2003 | Fliederweg 22  | 82031 | Grünwald | 3       | Hamster   | 123€    |
| 123                   | 24.04.2021 | Jörg      | Mann       | 01.01.1999 | Königsstraße 1 | 80335 | München  | 4       | Maus      | 20€     |
| 123                   | 24.04.2021 | Jörg      | Mann       | 01.01.1999 | Königsstraße 1 | 80335 | München  | 5       | Keyboard  | 1000€   |

→ Die ist jetzt in der **ersten Normalform**
> :memo: **Note:** Man könnte auch noch `Straße` und `Hausnummer` trennen, aber das ist nicht nötig, da es keine Anomalien verursacht, 
> bzw. wir weder nach `Straße` noch nach `Hausnummer` sortieren möchten.


# Die zweite Normalform
**Eine Tabelle befindet sich in der 2. NF, wenn diese sich in der 1. NF befindet und jedes**
**Nichtschlüsselattribut von jedem Schlüsselkandidaten voll funktional abhängig** ([Funktionale Abhängigkeit](Funktionale Abhängigkeit)) **ist.**

Die Tabelle wird in mehrere Tabellen aufgeteilt, sodass jedes Nichtschlüsselattribut von jedem Schlüsselkandidaten voll funktional abhängig ist:

**Bestellung**

| `BestellNr` :key: | `Datum`    | `KundenNr` |
|-------------------|------------|------------|
| 122               | 23.04.2021 | 1          |
| 123               | 24.04.2021 | 2          |

**Kunde**

| `KundenNr` :key: | `Vorname` | `Nachname` | `GebDatum` | `Straße`       | `Plz` | `Ort`    |
|------------------|-----------|------------|------------|----------------|-------|----------|
| 1                | Max       | Mustermann | 28.03.2003 | Fliederweg 22  | 82031 | Grünwald |
| 2                | Jörg      | Mann       | 01.01.1999 | Königsstraße 1 | 80335 | München  |

**Artikel**

| `ArtNr` :key: | `ArtName` | `Preis` |
|---------------|-----------|---------|
| 1             | Monitor   | 200€    |
| 2             | Haus      | 2000€   |
| 3             | Hamster   | 123€    |
| 4             | Maus      | 20€     |
| 5             | Keyboard  | 1000€   |

**BestellungArtikel**

| `BestellNr` :key: | `ArtNr` :key: | `Anzahl` |
|-------------------|---------------|----------|
| 122               | 1             | 1        |
| 122               | 2             | 1        |
| 122               | 3             | 1        |
| 123               | 4             | 1        |
| 123               | 5             | 1        |

→ Hier werden sowohl `BestellNr` als auch `ArtNr` als Schlüsselkandidaten verwendet, da sie zusammen den Primärschlüssel bilden.
Nur mit diesen zwei Attributen hat `Anzahl` einen Sinn.

In allen Tabellen sind die nicht Schlüsselattribute voll funktional abhängig von den Schlüsselkandidaten.

**Beziehungen der Tabellen zu einander:**

----
:1:n_beziehung:

**Bestellung** <-> **Kunde**: 

Die `KundenNr` taucht in der Tabelle **Bestellung** auf, sie ist in der Tabelle **Bestellung** also ein Fremdschlüssel. 

Das beschreibt eine **1:N Beziehung**, da ein Kunde mehrere Bestellungen (oder gar keine) haben kann, aber eine Bestellung nur einem Kunden gehören kann. 

→ Also muss der *Primärschlüssel* :key: aus der Tabelle **Kunde** in die Tabelle **Bestellung** als *Fremdschlüssel* übernommen werden. 

→ So kann in **Bestellung** jede `BestellNr` nur einmal auftauchen, da sie :key: ist und die `KundenNr` mehrmals auftauchen, da sie *Fremdschlüssel* ist.

----
:n:m_beziehung:

**Bestellung** <-> **Artikel**:

Es handelt ish um eine **N:M Beziehung**, da eine Bestellung mehrere Artikel enthalten kann und ein Artikel in mehreren Bestellungen enthalten sein kann.

→ Wir müssen eine neue Tabelle **BestellungArtikel** erstellen, die die beiden Schlüsselkandidaten `BestellNr` und `ArtNr` enthält.

→ Dies ist dann ein **zusammengesetzter** Primärschlüssel :key:!


# Die dritte Normalform
**Eine Tabelle befindet sich in der 3. NF wenn diese sich in der 2. NF befindet und**
**kein nicht schlüssel Attribut transitiv von einem Schlüsselkandidaten abhängt**

In unserer Tabelle **Kunde** hängt `Ort` transitiv von `Plz` ab, da `Plz` von `KundenNr` abhängt:

	`KundNr` <- `Plz` <- `Ort`

Deshalb erstellen wir eine weitere Tabelle **Plz**, da `Ort` nicht direkt von `KundenNr` (also :key:) abhängt:

**Plz**

| `Plz` | `Ort`    |
|-------|----------|
| 82031 | Grünwald |
| 80335 | München  |
