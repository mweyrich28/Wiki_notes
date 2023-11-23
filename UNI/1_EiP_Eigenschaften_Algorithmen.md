# Eigenschaften Algorithmus
:determinismus:determiniertheit:korrektheit:funktionaler_algorithmus:rekursion:

### Allgemeinheit
*Allgemeinheit*: Lösung für Problemklasse, nicht Einzelaufgabe

## Terminierung
Ein Algorithmus heißt terminierend, wenn er (bei jeder erlaubten Eingabe von Parametern) nach endlich vielen Schritten
beendet ist, anderenfalls spricht man von einem nicht terminierenden Algorithmus


## Determiniertheit
Ein Algorithmus heißt determiniert, wenn er bei denselben (zulässigen) Eingabewerten stets das selbe Ergebnis liefert,
anderenfalls heißt er nicht-determiniert 

```python
	def getRandNum():
		x = math.randint(0, 100)
		if x % 2:
			y = 16/4
		else:
			y = 2 * 2
		return y 
		- für jeden Wert von x ist y 4, also handelt es sich um einen determinierten Algorithmus, jedoch ist dieser
		- nicht deterministisch, da er für gerade Zahlen y anders berechnet als für ungerade
```

## Determinismus
Ein Algorithmus heißt deterministisch, wenn für alle Eingabedaten die Reihenfolge aller auszuführenden Schritte
eindeutig bestimmt ist, anderenfalls heißt er nicht-deterministisch

```python
	def calc(n):
		x = math.randint()
		n += x
		return n
		- dieser Algorithmus ist deterministisch, er führt für jedes x die gleichen Schritte aus, jedoch bekommen wir
		- für unterschiedliche x unterschiedliche Rückgabewerte, also ist dieser Algorithmus nicht determiniert
```

## Definition Spezifikation
- vollständige, detaillierte und unzweideutige Problembeschreibung

## Partielle Korrektheit
Algorithmus heißt partiell korrekt, wenn für alle gültigen Eingaben das Resultat der Nachbedingung des Algorithmus entspricht
Das Ergebnis muss aber (wenn eins raus kommt) richtig sein und Sinn machen
Endlosschleifen sind partiell korrekt!
Entweder terminiert er und gibt das *richtige Ergebnis* oder er terminiert *garnicht*

## Totale Korrektheit
Ein Algorithmus heißt total korrekt, wenn der Algorithmus partiell korrekt ist und für alle Eingaben terminiert 


### In short
- Terminierung: *"Werden wir fertig? (Egal wie)"*
- Deterministisch *"Ist der Weg immer gleich?/Weg & Ergebnis immer gleich"*
- Determiniert *"Ist das Ergebins eindeutig?/ Ergebnis immer gleich"*
- Partiell Korrekt *"Immer gültiges Ergebnis, z.B. Karte _gefunden_ oder _nicht gefunden_"*
- Total Korrekt *"Ist der Algotithmus partiell Korrekt und terminiert?"*

# Unterschied Methoden, Prozeduren, Funktionen
- Funktion: liefert als Ergebnis einen Wert eines Datentyps, nimmt lediglich Berechnungen vor
- Prozedur: imperativer Algorithmus: z.B. void main()
- Methode: OOP, Mischform aus Prozedur und Funktion

# Funktionaler Algorithmus
- Keine Schleifen, nur Rekursion
- Keine Anweisungen, nur Ausdrücke
- Determiniert
- *JAVA ist keine funktionale Sprache*, enthält aber einige funktionale Konzepte

*BEISPIEL* 
```java
	static int mul(int a, int b){
		return a * b;
	}
```
# Rekursion
- beruht auf der Zerlegung des Problems in mehrere kleinere gleichartige Probleme

## Rekursion Stack
- Eine rekursive Funktion ruft sich selbst so lange auf bis Abbruchbedingung (*Basisfall*) erfüllt ist
- Die Funktionsaufrufe "stacken" sich auf dem Stack: ![Aufrufshierarchie](/home/malte/01_Documents/vimwiki/Assets/EiP/Rekursion/Aufrufshierarchie.png)
- Die Ausgabe wird dann von oben nach unten durchgeführt: ![Ausführung](/home/malte/01_Documents/vimwiki/Assets/EiP/Rekursion/ausgeführte_Rek.png)
- Falls die Abbruchbedingung nie erreicht wird, kommt es zu einem `java.lang.StackOverflowError`:
	- Man spricht hier von der Rekursionstiefe, welche von Java limitiert ist
