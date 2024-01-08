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
> Die Attribute `LName`, `LStadt` und `LLand` sind ***funktional abhängig*** vom Attribut `LNr` 
> (eben so `LLand` von `LStadt`)

→ Redundanzen führen zu Speicherplatzverschwendung

:def:dbs:anomalien:
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
:def:dbs:funktionale_abhängigkeit:
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
> Formalisierung von Redundanz und Anomalien

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

:def:dbs:superschlüssel:
> :eight_spoked_asterisk: **Definition:** ***Superschlüssel***
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

:def:dbs:primattribut:prim:
> :eight_spoked_asterisk: **Definition:** ***Prime Attribute***
> 
> Ein Attribut heißt **prim**, wenn es Teil eines Schlüsselkandidaten ist


## Partielle und volle Funktionale Abhängigkeit

Ist ein Attribut $B$ funktional von $A$ abhängig,
dann auch von jeder Obermenge von $A$.

**→ Man ist interresiert, minimale Mengen zu finden, von denen**
$B$ **abhängt** (Schlüsseldefinition)

:def:dbs:partielle_funktionale_abhängigkeit:voll_funktionale_abhängigkeit:
> :eight_spoked_asterisk: **Definition:** 
>
> - Gegeben: Eine funktionale Abhängigkeit $X \to Y$
> - Wenn es keine echte Teilmenge $X'$ von $X$ gibt, so dass $X' \to Y$ gilt 
>   dann heißt $X \to Y$ **voll funktional Abhängig** ($X$ $\cdot \atop \to$ $Y$)
> - **Anderenfalls eine partielle funktionale Abbhängigkeit**

Beispiel:

![3_DBS_7_Funktionale_Abhängigkeit_Bsp_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Funktionale_Abhängigkeit_Bsp_2.png)

### Volle FD vs Minimalität des Schlüssels
> :warning: **Warning:** Definitionen sind sehr ähnlich:

**Schlüssel:** Minimale Menge, die Eindeutigkeit erfüllt

**Volle FD:** Minimale Menge, von der ein Attribut abhängt 
(und die Eindeutigkeit ist äquivalent zur FD)

> :warning: **Warning:** Aus der Minimalität des Schlüssels folgt **nicht**, dass alle Attribute
> (immer) voll funktional Abhängig sind!!!

> :memo: **Note:** Unterschied der beiden liegt im Allquantor (der in den Definitionen verschieden ist):
	> - **Schlüssel:** Minimale Menge, von der alle Attribute funktional Abhängig sind
	> - **Volle FD** $X$ $\cdot \atop \to$ $Y$ **:** Für jedes Attribut $A \in Y$ gilt:
	>   $X$ ist die minimale Menge von der $A$ funktional Abhängig ist

# Herleitung von funktionaler Abhängigkeiten

## Armstrong-Axiome
:def:dbs:armstrong_axiome:
> :eight_spoked_asterisk: **Definition:** ***Reflexivität (R):***
> 
> Falls $Y$ eine Teilmenge von $X$ ist ($Y \subseteq X$), denn gilt immer $X \to Y$
> 
> **Insbesondere:** $X \to X$

> :eight_spoked_asterisk: **Definition:** ***Verstärkung (VS):***
> 
> Falls $X \to Y$ gilt, dann gilt auch $XZ \to YZ$, wobei $XZ \equiv X \cup Z$

> :eight_spoked_asterisk: **Definition:** ***Transitivität (T):***
> 
> Falls $X \to Y$ und $Y \to Z$ gilt, dann gilt auch $X \to Z$

→ Diese Axiome sind **vollständig und korrekt**:

Sei $F$ eine Menge von FDs:
- Es lassen sich nur FDs von $F$ ableiten, die von jeder 
  relationalen Ausprägung erfüllt werden, für die auch $F$ erfüllt ist
- Es sind alle FDs ableitbar, die durch $F$ impliziert sind

> :eight_spoked_asterisk: **Definition:** ***Triviale funktionale Abhängigkeit:***
> 
> Wegen **Reflexivität** ist jedes Attribut funktional Abhängig:
> - von sich selbst
> - von jeder Obermenge von sich selbst
> 
> → Solche Abhängigkeiten heißen **trivial**

> :eight_spoked_asterisk: **Definition:** ***Symmetrieeigenschaften von funktionaler Abhängigkeit:***
> 
> Bei der funktionalen Abhängigkeit gibt es kein Gesetz zur Symmetrie oder Antisymmetrie, d.h. 
> bei zwei beliebigen Attribut-(Mengen) $X,Y$ sind alle 4 Fälle möglich:
> - Es gilt nur $X \to Y$
> - Es gilt nur $Y \to X$
> - Es gilt $X \to Y$ und $Y \to X$
> - Es gibt keine funktionale Abhängigkeit zwischen $X$ und $Y$

## Hülle einer Attributmenge
- **Eingabe:** eine Menge $F$ von FDs und eine Attributmenge $X$
- **Ausgabe:** die vollständige Menge von Attributen $X^{+}$, für die gilt: $X \to X^{+}$

```
AttrHülle(F,X)
    Erg := X
	while (Änderung an Erg) do
	    foreach FD Y -> Z in F do
		    if Y subset(Erg) then
			   Erg := Erg union(Z)
	Ausgabe X+ = Erg
```
Beispiel: AttrHülle(F, {LNr}) mit:
- $F = \left\{LNr \to LName; LNr \to LStadt; LStadt \to LLand; LNr, Ware \to Preis\right\}$
- $Erg_{i}$ = $Erg$ nach $i$-ter Iteration der `while`-Schleife
- $Erg_{0}= \{LNr\}$
- $Erg_{1}= \{LNr, LName, LStadt\}$
- $Erg_{2}= \{LNr, LName, LStadt, LLand\}$
- $Erg_{3}= \{LNr, LName, LStadt, LLand\} = Erg_{2}$

## Weitere Regeln zu funktionaler Abhängigkeit
> :eight_spoked_asterisk: **Definition:** ***Vereinigungsregel (VE):***
> 
> Falls $X \to Y$ und $X \to Z$ gilt, dann gilt auch $X \to YZ$

> :eight_spoked_asterisk: **Definition:** ***Dekompositionsregel (D):***
> 
> Falls $X \to YZ$ gilt, dann gilt auch $X \to Y$ und $X \to Z$

> :eight_spoked_asterisk: **Definition:** ***Pseudotransitivitätsregel (P):***
> 
> Falls $X \to Y$ und $ZY \to V$ gilt, dann gilt auch $XZ \to V$

![3_DBS_7_Herleitung_funk_Abh_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Herleitung_funk_Abh_Bsp_1.png)

![3_DBS_7_Herleitung_funk_Abh_Bsp_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Herleitung_funk_Abh_Bsp_2.png)


# Normalisierung
:def:dbs:normalform:normalisierung:
→ In einem Relationenschema sollen also möglichts keine funktionalen Abhängigkeiten auftreten,
**außer vom gesamten Schlüssel**

→ Verschiedene Normalformen beseitigen unterschiedliche Arten von funktionalen Abhängigkeiten bzw. Redundanzen/Anomalien:
- 1. Normalform
- 2. Normalform → 1. Normalform
- 3. Normalform → 2. Normalform
- Boyce-Codd Normalform (BCNF) → 3. Normalform
- 4. Normalform → BCNF

→ Herstellung einer Normalform durch *Verlustlose* Zerlegung des Schemas in mehrere Schemata

## 1. Normalform
> :eight_spoked_asterisk: **Definition:** ***1. Normalform***
> - Keine Einschränkung bezüglich der FDs
> - Ein Relationenschema ist in 1. Normalform, wenn alle Attributwerte **atomar** sind
> - In relationalen Datenbanken sind nicht-atomare Attribute nicht erlaubt/nicht möglich
> - Nicht-atomare Attribute z.B. durch `GROUP BY`:
	> ![3_DBS_7_1_Normalform_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_1_Normalform_Bsp_1.png)

## 2. Normalform
> :eight_spoked_asterisk: **Definition:** ***2. Normalform***
> 
> Ein Schema ist in zweiter Normalform, wenn jedes Attribut entweder:
> - voll funktional Abhängig von **allen** Schlüsselkandidaten ist
> - oder ein Primattribut ist (Teil eines Schlüssels)
> 
> *Motivation:* Vermeidung von Redundanzen: Man möchte verhindern, dass Attribute
> nicht vom gesamten Schlüssel voll funktional Abhängig sind, sondern nur von einem Teil davon:
	> ![3_DBS_7_2_Normalform_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_2_Normalform_Bsp_1.png)
> 
> → Dies fordert man vorerst nur für Nicht-Schlüssel-Attribute

z.B.: Kann 2. Normalform verletzt sein, wenn ...
- ... ein zusammengesetzter Schlüssel (-Kandidat) existiert
- ... und wenn nicht-prime Attribute existieren

### Zur Transformation in 2. Normalform spaltet man das Rel Schema auf:
- Attribute, die **voll funktional abhängig** von Schlüssel sind, bleiben in der 
  Ursprungsrelation $R$
- Für alle Abhängigkeiten $X_{i} \to Y_{i}$ von einem Teil eines Schlüssels 
  $(X_{i} \not \subseteq S)$ geht man folgendermaßen vor:
  1. Lösche die Attribute $Y_{i}$ aus $R$ 
  2. Gruppiere die Abhängigkeiten nach gleichen linken Seiten $X_{i}$
  3. Für jede Gruppe führe eine neue Relation ein mit allen erhaltenen Attributen aus $X_{i}$ und $Y_{i}$
  4. $X_{i}$ wird Schlüssel in der neuen Relation

![3_DBS_7_2_Normalform_Bsp_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_2_Normalform_Bsp_2.png)

![3_DBS_7_2_Normalform_Bsp_3](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_2_Normalform_Bsp_3.png)

## 3. Normalform
> :eight_spoked_asterisk: **Definition:** ***3. Normalform***
> 
> Ein Relationenschema ist in der 3. Normalform, **wenn für jede nicht-triviale**
> **funktionale Abhängigkeit** $X \to A$ **gilt:**
> - $X$ enthält einen Schlüsselkandidaten
> - oder $A$ ist prim
> 
> *Motivation:* Man möchte zusätzlich verhindern, dass Attribute von nicht-primen Attributen
> funktional abhängig sind
> 
> ![3_DBS_7_3_Normalform_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_3_Normalform_Bsp_1.png)
> 
> **Abhängigkeit von Nicht-Schlüssel-Attribut** bezeichnet man häufig auch als
> *transitive* (Armstrong-Axiome) *Abhängigkeit* vom Primärschlüssel:
> - $\underline{LNr} \to LStadt \to LLand$, also indirekt $\underline{LNr} \to LLand$

**Anmerkung zur 3. NF:**
- Wieder Beschränkung auf FDs, bei denen die rechte Seite nicht prim ist
- Intuitiv mochte die Definition sagen: Nicht Prime Attribute sind nur von (ganzen) 
  Schlüsselkandidaten funktional abhängig, also:
  
  Für jede FD gilt:
  - Keine Partiellen FDs von Schlüsselkandidaten → 2. NF ist mit 3. NF impliziert
  - Keine FDs, bei denen die linke Seite kein Schlüssel ist bzw. Teile enthält, die nicht prim sind
- Wegen Reflexivitäts- und Verstärkungsaxiom und Allquantoren bei den FDs muss man aber berücksichtigen:
	- Es gelten immer auch die trivialen FDs 
	  
	  (z.B. $A \to A$, für jedes beliebige Attribut $A$. Deshalb Ergänzung der Definition: *"Für jede nicht-triviale FD gilt..."* (in 3.NF))
	- Ist $S$ Schlüssel, dann gilt immer auch $S' \to R$ für jede Obermenge $S \subseteq S'$, deshalb 
	  heißt es in der Definition: $X$ **enthält** einen Schlüssel (statt $X$ **ist** ein Schlüssel)

### Transformation in 3. Normalform
- Attribute, die voll funktional Abhängig vom Schlüssel sind, und die nicht 
  abhängig von Nicht-Schlüssel-Attributen sind, bleiben in der Ursprungsrelation $R$
- Für alle Abhängigkeiten $X_{i} \to Y_{i}$ von einem Teil eines Schlüssels $(X \not \subseteq S)$ oder von Nicht-Schlüssel-Attribut:
  1. Lösche die Attribute $Y_{i}$ aus $R$ 
  2. Gruppiere die Abhängigkeiten nach gleichen linken Seiten $X_{i}$
  3. Für jede Gruppe führe eine neue Relation ein mit allen erhaltenen Attributen aus $X_{i}$ und $Y_{i}$
  4. $X_{i}$ wird Schlüssel in der neuen Relation

![3_DBS_7_3_Normalform_Bsp_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_3_Normalform_Bsp_2.png)


# Verlustlosigkeit der Zerlegung
:def:dbs:verlustlose_zerlegung:
> :eight_spoked_asterisk: **Definition:** ***Verlustlose Zerlegung***
> 
> Die Zerlegung einer Relation $R$ in die beide Teilrelationen $R_{1}$ und $R_{2}$ ist **verlustlos/verbundtreu**, wenn gilt:
> - $R = R_{1} \bowtie R_{2}$ 
> Das zeigt man, wenn mindestens eine der beiden folgenden FDs gilt:
> - $/R_{1} \cap R_{2} \to R_{1}$
> - $/R_{1} \cap R_{2} \to R_{2}$

Intuitiv ist klar, dass Verlustlosigkeit von größter
Wichtigkeit ist, weil andernfalls gar nicht dieselbe
Information in den Relationenschemata R1 und R2

# Abhänigkeitserhaltung
:def:dbs:abhängigkeitserhaltung:
> :eight_spoked_asterisk: **Definition:** ***Abhänigkeitserhaltung***
> 
> Die Zerlegung einer Relation $R$ in die beiden Teilrelationen $R_{1}$ und $R_{2}$ ist 
> **abhängigkeitserhaltend** (oder auch Hüllentreu), wenn gilt:
> - $F_{R} = (F_{R1} \cup F_{R1})$ bzw $F_{R}^{+} = (F_{R1} \cup F_{R2})^{+}$

D.h jede funktionale Abhhängigkeit soll mindestens eine der Teilrelationen vollständig
zugeordnet sein (also alle Attribute der linken Seite und das Attribut der rechte Seite müssen in einer der Teilrelationen enthalten sein)

Zwar führt die Verletzung der Abhängigkeitserhaltung
nicht zu einer Veränderung der speicherbaren Information,
aber eine „verlorene“ FD ist nicht mehr überprüfbar, ohne
dass der Join durchgeführt wird

→ Verschlechterung der Situation (Redundanz, Anomalien)

# Synthesealgorithmus für 3NF
:dbs:def:synthesealgorithmus_3nf:synthesealgorithmus:
> :eight_spoked_asterisk: **Definition:** ***Synthesealgorithmus für 3NF:***
> 
> Der **Synthesealgorithmus** ermittelt zu einem gegebenen Relationenschema $R$ mit funktionalen
> Abhängigkeiten $F$ eine Zerlegung in Relationen $R_{1}, \dots, R_{n}$ die folgende Kriterien erfüllt:
> - $R_{1}, \dots, R_{n}$ ist eine verlustlose Zerlegung von $R$
> - Die Zerlegung ist abhängigkeitserhaltend
> - Alle $(1 \le i \le n)$ sind in dritter Normalform

**IN SHORT:**

Der Synthese Algorithmis arbeitet in 4 Schritten:
1. Bestimme die **kanonische Überdeckung** $F_{c}$ zu $F$, d.h. 
   eine minimale Menge van FDs, die dieselben (partiellen und transitiven) Abhängigkeiten wie $F$ beschreiben
2. Erzeuge neue Relationenschemata aus $F_{c}$
3. Rekonstruiere einen Schlüsselkandidaten
4. Eliminiere überflüssige Relationen

**IN DETAIL:**

**Schritt (1): Bestimme die kanonische Überdekung F_c zu einer gegebenen Menge F von Funktionalen Abhängigkeiten (FDs)**
1. Führe für jede FD $X \to Y \in F$ die **Linksreduktion** durch, also:
	1. Überprüfe für alle $A \in X$ ob $A$ überflüssig ist, d.h ob 
	   
	   $Y \subseteq AttrHülle(F, X - A)$ gilt 
	   
	   → Falls das der Fall ist, ersetzte $X \to Y$ durch $(X - A) \to Y$

2. Führe für jede (verbliebene) FD $X \to Y$ die **Rechtsreduktion** durch, also:
	1. Überprüfe für alle $B \in Y$, ob 
	    
	   $B \subseteq AttrHülle\Big(\big(F - (X \to Y)\big) \cup \big(X \to (Y - B)\big), X \Big)$
       
	   gilt. In diesem Fall ist $B$ auf der rechten Seite überflüssig und kann eliminiert werden. 
	   → Das heißt $X \to Y$ wird ersetzt durch $X \to (Y - B)$

3. Entferne alle FDs der Form $X \to \left\{\right\}$, die in (2.) möglicherweise entstanden sind.

4. Fasse die FDs der Form $X \to Y_{1}, X \to Y_{2}, \dots, X \to Y_{n}$ zusammen, so dass 
   
   $X \to \Big(Y_{1} \cup Y_{2} \cup  \dots \cup Y_{n}\Big)$ verbleibt
	   

**Schritt (2): Für jede FD x -> Y ist Element F_c**
1. Erzeuge ein Relationenschema $R_{X} := X \cup Y$
2. Ordne $R_{X}$ die FDs $F_{X} := \Big\{ X' \to Y' \in F_{c} | X' \cup Y' \in R_{x}\Big\}$ zu.

**Schritt (3) Rekonstruiere einen Schlüsselkandidaten**
1. Falls eines der in Schritt (2) erzeugten Relationenschemata $R_{X}$ einen Schlüsselkandidaten 
   von $R$ bezüglich $F_{c}$ enthält, sind wir fertig.
2. Anderenfalls wähle einen Schlüsselkandidaten $S \subseteq R$ aus und definiere folgendes zusätzliches Schema:
	1. $R_{S} := S$
	2. $F_{S}:= \left\{\right\}$

**Schritt (4) Eliminiere überflüssige Relationen**
1. Eliminiere diejenigen Schemata $R_{X}$, die in einem anderen Relationsschema $R_{X}$ enthalten sind, d.h:
	1. $R_{X} \subseteq R_{X'}$

## Beispiel
**Einkauf**(Anbieter, Ware :key:, WGruppe, Kunde :key:, KOrt, KLand, Kaufdatum :key:)

Es gelten folgende FDs:
- `Kunde`, `Ware` -> `KLand`
- `Kunde`, `WGruppe` -> `Anbieter`
- `Anbieter` -> `WGruppe`
- `Ware` -> `WGruppe`
- `Kunde` -> `KOrt`
- `KOt` -> `KLand` 

![3_DBS_7_Synthesealgorithmus_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Synthesealgorithmus_Bsp_1.png)

![3_DBS_7_Synthesealgorithmus_Bsp_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Synthesealgorithmus_Bsp_2.png)


# Boyce-Codd Normalform (BCNF)
In der **3. NF** können weiterhin folgende *Abhängigkeiten* auftreten:

**Abhängigkeiten unter Attributen, die Prim sind, aber noch nicht vollständig einen Schlüssel bilden**

Bsp:

**Autoverzeichnis**(`Hersteller` :key:, `HerstellerNr`, `ModelNr` :key:)
- es gilt 1:1-Beziehung zwischen `Hersteller` und `HerstellerNr`:
	- `Hersteller` -> `HerstellerNr`
	- `HerstellerNr` -> `Hersteller`
- Schlüsselkandidaten sind deshalb:
	- $\left\{Hersteller, ModelNr\right\}$
	- $\left\{HerstellerNr, ModelNr\right\}$

Schema befindet sich in 3. NF, da alle Attribute prim sind

Trotzdem können auch hier Anomalien auftreten

:dbs:def:boyce_codd_normalform:bcnf:
> :eight_spoked_asterisk: **Definition:** ***Boyce-Codd-Normalform***
> 
> Ein Schema $R$ ist in Boyce-Codd-Normalform, wenn für alle nicht trivialen
> Abhängigkeiten $X \to Y$ gilt:
> - $X$ enthält einen Schlüsselkandidaten von $R$

- Verlustlose Zerlegung ist generell immer möglich
- Äber die Abhängigkeitserhaltung ist nicht immer möglich


# Mehrwertige Abhängigkeit (multi-valued dependency, MVD)
→ Entstehen wenn mehrere **1:n-Beziehungen** in einer Relation stehen
(was nicht sein darf (siehe Kapitel 6))

![3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_1.png)

![3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_2](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_2.png)

:dbs:def:mehrwertige_abhängigkeit:mvd:
> :eight_spoked_asterisk: **Definition:** ***Mehrwertige Abhängigkeit***
> 
> Gegeben $X,Y \subseteq R$ und es sei $Z = R \setminus (X \cup Y)$,
> d.h der Rest $Y$ ist *mehrwertig abhängig* von $X (X \to \to Y)$, wenn
> für jede gültige Ausprägung von $R$ gilt:
> - Für jedes Paar aus Tupeln $t_{1}, t_{2}$ mit $t_{1}.X=t_{2}.X$ aber
> $t_{1} \not = t_{2}$, existieren die (nicht immer zu $t_{1}$ und $t_{2}$ verschiedenen)
> Tupel $t_{3}$ und $t_{4}$ mit den Eigenschaften:
> 	- $t_{1}.X = t_{2}.X = t_{3}.X = t_{4}.X$
> 	- $t_{3}.Y = t_{1}.Y$
> 	- $t_{3}.Z = t_{2}.Z$
> 	- $t_{4}.Y = t_{2}.Y$
> 	- $t_{4}.Z = t_{1}.Z$

D.h jedem $X$ ist eine **Menge von Y Werten** zugeordnet

Jede FD ist auch eine MVD

![3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_3](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_3.png)

![3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_4](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_Mehrwertige_Abhängigkeit_Bsp_4.png)


## Verlustlose Zerlegung MVD
Ein Relationenschema $R$ mit einer Menge $D$ von zugeordneten 
funktionalen mehrwertigen Abhängigkeiten (MVDs) kann genau dann
verlustlos in die beiden Schemata $R_{1}$ und $R_{2}$ zerlegt werden,
wenn gilt:
- $R = R_{1} \cup R_{2}$
- Mind. eine von zwei MVDs gilt:
	1. $R_{1} \cap R_{2} \to \to R_{1}$ oder
	2. $R_{1} \cap R_{2} \to \to R_{2}$ 


## Triviale MVD und 4. Normalform
:def:dbs:triviale_mvd:
> :eight_spoked_asterisk: **Definition:** ***Triviale MVD***
> 
> Eine MVD $X \to\to Y$ bezogen auf $X \cup Y \subseteq R$ ist
> **trivial**, wenn jede mögliche Ausprägung $r$ von $R$ diese MVD erfüllt.
> Man kann zeigen, dass $X \to \to Y$ trivial ost, gdw:
> - $Y \subseteq X$ oder
> - $Y = R - X$

Eine Relation $R$ mit zugeordneter Menge $F$ von FDs und MVDs ist in der **4. Normalform**, wenn
für jede MVD $X \to \to Y \in F^{+}$ eine der folgenden Bedingungen gilt:
- Die MVD ist trivial oder
- $X$ ist Superschlüssel von $R$

Bsp:

![3_DBS_7_4_Normalform_Bsp_1](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_DBS_7_4_Normalform_Bsp_1.png)


# Zusammenfassung
- 1. Normalform:
  Alle Attribute sind atomar
- 2. Normalform:
  Keine FD eines Nicht-Schlüssel-Attributs von **Teil** eines Schlüssels
- 3. Normalform:
  Zusätzlich keine nichttriviale funktionale Abhängigkeit 
  eines Nicht-Schlüssel-AttributsA von Nicht-Schlüssel-Attributen
- Boyce-Codd-Normalform: 
  Zusätzlich keine nichttriviale funktionale Abhängigkeit unter den Schlüssel-Attributen
- 4. Normalform: 
  Keine Redundanz durch MVDs
  
