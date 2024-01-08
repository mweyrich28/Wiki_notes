----

:dbs:funktionale_abhaengigkeiten:funktionale_abhängigkeiten:

----
FD muss allgemein gültig sein, d.h. für alle Tupel der Relation gelten. 
Z.B. in der Tabelle:


| `PersonenNr` | `Name`    | `Vorname` | `GebDatum` | `ProjektNr` :key: | `ProjektName`     | `Prioritaet` |
|--------------|-----------|-----------|------------|-------------------|-------------------|--------------|
| 1            | Schweizer | Albert    | 01.03.1973 | 5                 | Unis              | 7            |
| 2            | Carlos    | Rob       | 12.07.1975 | 1                 | Data Center       | 10           |
| 2            | Carlos    | Rob       | 12.07.1975 | 3                 | Lobby             | 8            |
| 2            | Carlos    | Rob       | 12.07.1975 | 6                 | Kanninchenzüchter | 2            |
| 3            | Müller    | Peter     | 09.10.1999 | 2                 | Hasenzüchter      | 3            |
| 3            | Müller    | Peter     | 09.10.1999 | 4                 | Politiker         | 5            |


Hier sind z.B.:
- `PersonenNr` -> `Name`, `Vorname`, `GebDatum` $\equiv \left\{PersonenNr\right\} \to \left\{Name, Vorname, GebDatum\right\}$
- `ProjektNr` -> `ProjektName`, `Prioritaet` $\equiv \left\{ProjektNr\right\} \to \left\{ProjektName, Prioritaet\right\}$
- `ProjektNr` -> `PersonenNr`, `Name`, `Vorname`, `GebDatum` $\equiv \left\{ProjektNr\right\} \to \left\{PersonenNr, Name, Vorname, GebDatum\right\}$

In dieser Relation ist der Primärschlüssle = `ProjektNr` (hier wird davon ausgegangen, dass es zu jedem Projekt
nur einen Anspechpartner gibt). Deshalb sind alle restlichen Attribute von `ProjektNr` funktional abhängig.


Eine triviale FD ist z.B. `ProjektNr` -> `ProjektNr` $\equiv \left\{ProjektNr\right\} \to \left\{ProjektNr\right\}$ da die linke seite vollständig 
in der rechten seite enthalten ist. Diese FD ist immer erfüllt.

