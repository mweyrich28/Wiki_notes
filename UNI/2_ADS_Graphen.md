# Graphen
I) Vl →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/5-Graphen.pdf)

## Minimaler Spannbaum
- Definition: Ein Spannbaum eines Graphen ist ein Teilgraph, der alle Knoten enthält und zyklenfrei ist.
- Ein minimaler Spannbaum ist ein Spannbaum mit minimalen Gesamtkosten.
→  n-1 Kanten bei n Knoten

### Tiefendurchlauf vs Breitendurchlauf

Tiefendurchlauf: ![Wasmeier Definition](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/tiefensucheDef.png)

Ablauf: 
![Ablauf 1](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/tiefensucheAblauf1.png)
![Ablauf 2](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/tiefensucheAblauf2.png)
![Abauf 3](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/tiefensucheAblauf3.png)

- Starte bei einem beliebigen Knoten
- Gehe so weit wie möglich in die Tiefe
- Falls kein weiterer Knoten mehr erreicht werden kann, gehe einen Schritt zurück
- Wiederhole, bis alle Knoten besucht wurden
- Kann in 3 Typen eingeteilt werden:
	- Preorder: Knoten werden besucht, bevor die Kinder besucht werden
	- Inorder: Knoten werden besucht, nachdem der linke Teilbaum besucht wurde
	- Postorder: Knoten werden besucht, nachdem die Kinder besucht wurden
- Breitendurchlauf:
	- Starte bei einem beliebigen Knoten
	- Alle nachbarn kommen in die Warteschlange
	- Besuche alle Nachbarn
	- Besuche alle Nachbarn der Nachbarn
	- Wiederhole, bis alle Knoten besucht wurden

### Prim-Algorithmus
Pseudocode:
```
𝑉′ ← 𝑣0 beliebig
𝐸′ ← ∅
Solange 𝑉′ ≠ 𝑉:
	(𝑢, 𝑣) = argmin 𝑐(𝑒)
		    𝑒∈𝑉′ ×(𝑉−𝑉′)
	𝑉′ = 𝑉′ ∪ 𝑣
	𝐸′ = 𝐸′ ∪ {(𝑢, 𝑣)}
```
Die Laufzeitkomplexität ist 𝑂(|𝑉|^2^)

### Algorithmus von Kruskal
*Idee (ähnlich zu Prim-Algorithmus):*
- Starte mit leerer Kantenmenge.
- Kanten sind aufsteigend sortiert
- Füge sukzessive minimale Kanten bezüglich ihrer Kosten hinzu, sodass kein Zyklus entsteht. Es entstehen dann zuerst nicht zusammenhängende Teilgraphen, 
  die dann durch Hinzufügen von Kanten verbunden werden.
- Stoppe, falls keine solche Kante mehr gefunden werden kann (die nächste Kante bildet einen Zyklus, alle Knoten erreichbar).

*Pseudocode:*
```
𝐸′ ←  ∅
Sortiere 𝐸 aufsteigend nach 𝑐(𝐸)
Solange 𝐸 ≠ ∅
	𝑒 ←  min(𝐸)
	𝐸=𝐸−{𝑒}
	Falls 𝐺(𝑉, 𝐸′ ∪ {𝑒}) zyklenfrei:
		𝐸′ = 𝐸′ ∪ {𝑒}
```
Hier dominiert das Sortieren die Laufzeit: 𝑂 (|𝐸| log |𝐸|)

### Union Find Algotithmus
**Berechnet die Zusammenhangskomponenten eines Graphen:**
- Repräsentiert Komponenten durch ausgewählte Knoten (Repräsentanten)
- Erstellt für jede Zusammenhangskomponente einen Baum
- Kantengewichte werden nicht berücksichtigt →  Bäume sind nicht unbedingt minimal
**Ablauf:**
- Initialisierung: Jeder Knoten ist sein eigener Repräsentant (zeigt auf sich selbst)
- Duchlaufe alle Kanten (x,y) ∈ E:
	- Vereinige die Partitionen der Knoten x und y mit union(x,y)
	- Bestimme die Partitionen der Knoten x und y mit find(x) und find(y)
- Am Ende zeigt das Array für jeden Knoten auf seinen Repräsentanten:
- find(x) bestimmt die Partition:
	- Solnage x nicht sein eigener Repräsentant ist, gehe zum Repräsentanten von x und gib x zurück
- union(x,y) vereinigt die Partitionen von x und y:
	- Bestimme die Partitionen von x und y mit find(x) und find(y)
	- Verbinde Partitionen: setze P(x) = y oder P(y) = x
	- Dazu verschiedene Heuristiken:
		- Setze immer den kleineren Baum unter den größeren
		- Setze "flachere" Bäume unter "tiefere"

![Union](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/unionFindunion.png)
![Find](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/unionFind.png)

> :memo: **Note:** 0 ist hier der Repräsentant der linken Gruppe

![Find](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/unionFind2.png)
![Union 2 groups](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/unionFind3.png)
→  kleinere Bäume werden unter größere gehängt!

## Suche nach kürzesten Wegen
:graph_shortest_path:
**Problemstellungen:**
- *"Single Source shortest Path":* Finde den kürzesten Weg von einem Knoten zu allen anderen Knoten 
- *"Single Destination shortest Path":* Finde den kürzesten Weg von allen Knoten zu einem Knoten
- *"Single Pair shortest Path":* Finde den kürzesten Weg von einem Knoten zu einem anderen Knoten

### Dijkstra-Algorithmus
:dijkstra:
- Löst das *"Single Source shortest Path"*-Problem
- Ziel: berechnet den kürzesten Weg von einem Startknoten zu allen anderen Knoten im Graph
- Gibt immer den kürzesten Weg aus
- Voraussetzung: Keine negativen Kantengewichte und zyklenfrei

**Ablauf:**
```
Dijkstra (𝐺,𝑣0 )
	𝑆 ← {𝑣0}
	for all 𝑣 ∈ 𝑉: {𝐷(𝑣) ← 𝑐[𝑣0 , 𝑣]} // Initialisiere Kanten
	
	while (𝑉 − 𝑆) ≠ ∅: // solange wir noch nicht alle Knoten besucht und abgearbeitet haben
		𝑤𝑚𝑖𝑛 ← argmin(𝑤∈V−𝑆 𝐷(𝑤)) // wir nehmen den Knoten mit der kleinsten Distanz
		𝑆 ← 𝑆 ∪ {𝑤𝑚𝑖𝑛} // wir fügen den Knoten zu den abgearbeiteten Knoten hinzu
		for all 𝑣 ∈ 𝑉 − 𝑆: // wir aktualisieren die Distanzen aller Nachbarn des Knotens
			𝐷(𝑣) = min(𝐷[𝑣] , 𝐷[𝑤𝑚𝑖𝑛] + 𝑐[𝑤𝑚𝑖𝑛 , 𝑣]) // falls die Distanz über den Knoten kürzer ist, aktualisieren wir die Distanz
```
→  Slides Seite 42: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/5-Graphen.pdf)

Komplexität:
- Falls G zusamenhängend, mit Adjazenzmatrix: 𝑂(|𝑉|²)
- Einsatz als "All Pairs shortest Path" Algorithmus: = O(|V| * |V|²) = 𝑂(|𝑉|³)

### Floyd-Algorithums
:floyd_algorithm:
- *"All-pairs shortest paths"*, negative edges allowed
- Versucht sukzessive, zwei Knoten über einen dritten zu verbinden (falls dies günstiger ist)
- Wir speichern die kürzensen Wege in einer Matrix (sehr kosteneffizeint)

Pseudocode:
```
let V = number of vertices in G
let dist be a |V| × |V| array of minimum distances initialized to ∞ (infinity)

for each vertex v
	dist[v][v] ←  0 // the distance from v to itself is 0
	
for each edge (u,v)
	dist[u][v] ← w(u,v)  // the weight of the edge (u,v)
	P[u][v] ← v // u is the predecessor of v

for k from 1 to |V|
	for i from 1 to |V|
		for j from 1 to |V|
			if dist[i][j] > dist[i][k] + dist[k][j] 
				dist[i][j] ← dist[i][k] + dist[k][j]
				P[i][j] ←  k // der neue kürzeste Weg von i nach j verläuft über k
			end if
```
![If Statement](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/FloydVideo.png)

→  `dict[2][3] ←  4-2 = 2` (siehe Bild)

Extrahieren des kürzesten Weges:

![Rekonstruktion kürzester Pfad](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/FloydPfad.png)

### A* Algorithmus
- Erweiterung von Dijkstra
- Bevorzugt Knoten, die in Richtung des Ziels gehen ("best first Suche")
- Berücksichtigt die Kosten des bisherigen Weges und die geschätzten Kosten zum Ziel
- Wähle als nächsten Knoten x jeweils denjenigen mit der kleinsten Summe f(x) für die geschätzen 
  Gesamtkosten von S bis Z: f(x) = g(x) + h(x), h(x) = Heuristik (die sagt uns, wenn wir uns annähern)
- Der A* veewaltet die besuchten Knoten in 2 Listen:
	- OpenedList: Ein Weg zum Knoten ist bekannt, aber noch nicht alle Nachbarn wurden besucht (es könnte günstigere Pfade geben) 
	  Nutzt Priority Queue zur Abarbeitung
	- ClosedList: Der kürzeste Weg zum Knoten (nicht zum Ziel)

**Qualitäteigenschaften:**
- Vollständig: Falls ein Pfad existiert, wird er gefunden
- Optimal: Es wird immer eine optimale Lösung gefunden
- Optimal effizeint: Bezogen auf die Laufzeit gibt es keinen Algorithmus, 
  der die gleiche Heuristik verwendet und schneller ist/weniger Knoten besucht

## Flussnetzwerke
- q = Quelle
- s = Senke
- c(u,v) = Kapazität der Kante (u,v)
- c(u,v) = 0, falls (u,v) ∉ E
- Symmetrie: f(u,v) = -f(v,u) →  f(u,v) = 7, f(v,u) = -7 →  alles was reinfließt, kann auch zurückfließen (negativer Fluss)
- Flusserhaltung: $\sum_{v \in V} f(u,v) = 0$ für alle $u \in V \setminus \{q,s\}$ 
  Wir betrachten einen Knoten (nicht q oder s) und schauen, wie viel reinfließt und wie viel rausfließt. Alles was reinfließt, muss auch wieder rausfließen. 
  Der Fluss ist also immer 0, außer bei q und s. Summer der eingehenden Flüsse = Summer der ausgehenden Flüsse
- Schreibweise über Kanten: -/4 => momentaner Durchfluss = 0, Kapazität = 4
- Residualnetz ist ein gerichteter Graph mit den gleichen Knoten wie das Flussnetz, aber mit zusätzlichen Kanten, die die Kapazität der Kanten im Flussnetz widerspiegeln. 
- "Flussnetzwerk minus Fluss" = Residualnetzwerk ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Graphen/residual_netz.png)

### Min-Cut-Max-Flow-Theorem
- s-t-Schnitt: Partitionierung von V in zwei disjunkte Mengen S und T mit s ∈ S und t ∈ T
- Kapatität des Schnitts: c(S,T) = $\sum_{u \in S, v \in T, (u,v) \in E} c(u,v)$ ist das Gesamtgeweicht der Kalnten von S nach T
- Der maximale Fluss ist gleich der minimalen Kapazität eines s-t-Schnitts.

### Ford-Fulkerson-Algorithmus
- Idee: Finde einen Pfad von s nach t, auf dem noch Kapazität frei ist. Erhöhe den Fluss auf diesem Pfad um die freie Kapazität.

### Eldmonds-Karp-Algorithmus
- Idee: Wähle den kürzesten Pfad von s nach t im Residualnetzwerk. Erhöhe f entlang p.
