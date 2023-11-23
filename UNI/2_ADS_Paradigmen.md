# Paradigmen
**MATERIAL**
1. [Slides-32](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/6-Paradigmen_1-32.pdf)
2. [Slides-33-end](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/6-Paradigmen_33-68.pdf)

## Backtracing
**Allgemein:**
BackTracking (Stufe, Lösungsvektor):
- *falls* Teillösung ungültig: gib *falsch* zurück
- *falls* alle Komponenten gesetzt sind: gib *richtig* zurück
- *solange* es auf der aktuellen Stufe noch Wahlmöglichkeiten gibt:
	- wähle einen neuen Lösungsschritt
	- setze die entsprechende Komponente
	- *falls* BackTracking ( Stufe+1, Lösungsvektor ): gib *richtig* zurück
	- *sonst* mache Wahl rückgängig_

→  Wenn es keinen neuen Teil-Lösungsschritt mehr gibt: keine Lösung!

## Sweep-Line-Algorithmus
:sweep_line:
- Vermeide den Vergleich aller Objekte mit allen anderen Objekten
- Wir testen nur Segmentpaare, die gleichzeitig von einer horizotalen Sweep Line L geschnitten werden
- Am schnittpunkt der Segmente wird ein Event ausgelöst: Von links nach rechts ändert sich die Reihefolge wenn L sich nach unten bewegt
- Speicherbedarf (Ergebnisgröße): $\mathcal{O}(n+r)$
- Laufzeit: $\mathcal{O}((n + r) \cdot \log (n))$

Bessere Erklärund für Q und T:
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Paradigmen/sweep_line_def.png)

### Algorithmus
- YouTube: https://www.youtube.com/watch?v=I9EsN2DTnN8

findIntersections(S):
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Paradigmen/findIntersections.png)

handleEvent(event p):
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Paradigmen/handleEvent.png)

Slide 65: rechter nachbar bei p,,r,,
