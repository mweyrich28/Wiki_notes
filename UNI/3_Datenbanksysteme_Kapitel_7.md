# Kapitel 7 - Normalformen
**SLIDES:** [Kapitel 7](file:///home/malte/OneDriver/01_Studium/3.Semester/Datenbanken/Slides/dbs1_07.pdf)
${toc}

## Relationaler Datenbank-Entwurf
**Schrittweises Vorgehen**
- Informelle Beschreibung: ***Pflichtenheft***
- Konzeptueller Entwurf: ***ER-Modell***
- Relationaler DB-Entwurf: ***Relationenschema***

> :memo: **In diesem Kapitel:** Normalisierungstheorie als formale Grundlage für den
> relationalen DB-Entwurf

> :memo: **Zentrale Fragenstellung:**
> - Wie können Objekte und deren Beziehungen ins relationale Modell überführt werden
> - Bewertungsgrundlagen zur Unterscheidung von guten und schlechten relationalen DB-Schemata

## Motivation
**Relation Liefernat:**

![3_DBS_7_Motivation_Rel1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Motivation_Rel1.png)

**→ Hier gibt es offensichtlich einige Redundanzen:**
- Wenn bei mehreren Tupeln der Attributwert `LNr` gleich ist, 
  dann müssen auch die Attributwerte von `LName`, `LStadt` und `LLand` gleich sein
- Wenn (auch bei verschiedenen `LNr`) `LStadt` gleich ist, 
  dann muss auch `LLand` gleich sein

**→ Redundanzen durch funktionale Abhängigkeit**
> :eight_spoked_asterisk: **Definition:** Wir sagen:
> Die Attribute `LName`, `LStadt` und `LLand` sind ***funktional abhängig*** vom Attribut `LNr` 
> (eben so `LLand` von `LStadt`)

→ Redundanzen führen zu Speicherplatzverschwendung

> :eight_spoked_asterisk: **Definition:** **Anomalien** (Inkonsistenz durch Änderungsoperationen)

> :memo: **Note:** Das eigentliche Problem sind *Anomalien* und dass das Schema
> nicht intuitiv ist

- **Update Anomalie:** Änderung der Adresse (`LName`, `LStadt`, `LLand`) in nur einem Tupel statt allen 
  Tupeln zu einer `LNr`
- **Insert Anomalie:** Einfügen eines Tupels mit inkonsistenter Adresse; 
  Einfügen eines Lieferanten erfordert Ware
- **Delete Anomalie:** Löschen der letzten Ware löscht die Adresse

### Verbesserung
**Neues DB-Schema**

![3_DBS_7_Motivation_Rel2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Motivation_Rel2.png)

**Vorteile:**
- keine Redundanzen
- keine Anomalien

**Nachteil:**
- Um zu einer Ware die Länder der Lieferanten zu finden, ist ein *zweifach Join* nötig 
  (teuer auszuwerten und umständlich zu schreiben)

### Zurück zur ursprünglichen Relation
Die ursprüngliche Relation *Lieferant* kann mit Hilfe einer **View** simuliert werden:

![3_DBS_7_Motivation_Rel3](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Motivation_Rel3.png)

- Dies spart die Schreibarbeit beim Formulieren von Anfragen
- Macht die Anfragen übersichtlicher
- In diesem Fall ist die **View** <span style="color:#cc241d;">nicht updatebar</span> (die Änderungen verursachen ja die Probleme)
- Da die **View** nur eine <span style="color:#cc241d;">virtuelle Relation</span> ist, muss der Join trotzdem ausgewertet werden (weniger effizient)

## Schema-Zerlegung
Anomalien entstehen durch Redundanzen

**Entwurfsziel:**
- Vermeidung von Redundanzen
- Vermeidung von Anomalien
- evtl. Einbeziehung von Effizienzüberlegungen

**Vorgehen:**
- Schrittweises Zerlegen des gegebenen Schemas (Normalisierung) in ein 
  äquivalentes Schema ohne Redundanzen und Anomalien
  
> :eight_spoked_asterisk: **Definition:** **Funktionale Ahängigkeit**:
> Formalisierung von Redundanz und Anomalien

# Funktionale Abhängigkeit (functional dependency, FD)
- beschreibt Beziehungen zwischen den Attributen zweier Relationen
- Schränkt das Auftreten gleicher, bzw. ungleicher Attributwerte innerhalb einer Relation ein
  
  → spezielle Integritätsbedingung (nicht in SQL)

> :recycle: **Wiederholung:** ***Integritätsbedingungen in SQL:***
> - Primärschlüssel
> - Fremdschlüssel (referentielle Integrität)
> - NOT NULL
> - CHECK

> :recycle: **Wiederholung:** ***Schlüssel***
> 
> Eine Teilmenge S der Attribute eines Relationalen Schemas R heißt **Schlüssel** gdw.
> - **Eindeutigkeit:** Keine Ausprägung von R kann zwei verschiedene Tupel enthalten, die sich in 
>   **allen** Attributen von S gleichen
> - **Minimalität:** Keine echte Teilmenge von S erfüllt die Eindeutigkeit

## Konvention zur Notation
**Ab jetzt gilt**
$$
\begin{align*}
	A, B, C &\to \text{Bezeichnet einzelne Attribute}\\
	X, Y, Z &\to \text{Bezeichnet Attributmengen}\\
\end{align*}
$$
**Zur Vereinfachung gilt auch:**
$$
\begin{align*}
	A, B \to C &\equiv \left\{A, B\right\} \to C\\
	X \to Y, Z &\equiv X \to Y \cup Z\\
	t.A &\equiv \text{Attribut A des Tupels t}\\
	t.X &\equiv \text{Attributmengen X von Attributen des Tupels t}\\
	t.X = r.X &\equiv \operatornamewithlimits{\forall}_{A \in X} t.A = r.A
\end{align*}
$$

## Funktionale Abhängigkeit
> :eight_spoked_asterisk: **Definition:** ***Funktionale Abhängigkeit***
> 
> Gegeben:
> - Ein Relationsschema $R$
> - $X, Y$: Zwei Mengen von Attributen von $R(X,Y \subseteq R)$
> 
> Definition: $Y$ ist von $X$ **funktional Abhängig** 
$$
(X \to Y) \iff  \operatornamewithlimits{\forall}_{\text{Tupel }t \land r}: t.X = r.X \implies t.Y = r.Y
$$

→ Bsp:

![3_DBS_7_Motivation_Rel1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Motivation_Rel1.png)
![3_DBS_7_Funktionale_Abhängigkeit_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Funktionale_Abhängigkeit_Bsp_1.png)

"Wenn man sagt, dass $Y$ von $X$ funktional abhängt ($X \to Y$),
bedeutet das im Grunde, dass für jeden Eintrag oder Datensatz in einer Tabelle,
wenn zwei verschiedene Zeilen denselben Wert für $X$ haben, werden sie auch denselben Wert für $Y$ haben.
Anders ausgedrückt, eine Veränderung in $X$ führt immer zu einer bestimmten Veränderung in $Y$."

## Verglich mit Schlüssel
**Gemeinsamkeiten** zwischen dem Schlüssel im relationalen Modell
und *Funktionaler Abhängigkeit*:
- Für jeden Schlüsselkandidaten $S = \left\{A, B, \dots\right\}$ gilt:
  
  **→ Alle Attribute der Relation sind von S funktional Abhängig (wegen der Eindeutigkeit):** $S \to R$

- > :eight_spoked_asterisk: **Definition:** ***Superschlüssel***
  > 
  > Jede Menge, von der $R$ funktional Abhängig ist, ist ein **Superschlüssel**

**Unterschied:**
- Aber es gibt u.U. weitere funktionale Abhängigkeiten: 
  
  **Ein Attribut B kann z.B. auch funktional Abhängig sein:**
  - von Nichtschlüsselattributen
  - von nur einem Teil eines Schlüssels
  
  
> :warning: **Warning:** **FD ist Verallgemeinerung des Schlüsselkonzepts**

Wie der Schlüssel ist auch die funktionale Abhängigkeit eine **Semantische Eigenschaft** des Schemas:
- FD nicht aus aktueller DB-Ausprägung entscheidbar
- sondern muss für alle möglichen Ausprägungen gelten

> :eight_spoked_asterisk: **Definition:** ***Prime Attribute***
> 
> Ein Attribut heißt **prim**, wenn es Teil eines Schlüsselkandidaten ist


## Patielle und volle Funktionale Abhängigkeit
