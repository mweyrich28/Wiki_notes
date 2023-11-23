# HeapSort
:heap_sort:algorithm:sort:

*Idee:*
- [[2_ADS_SelectionSort]]: Wähle n-mal das jeweils nächste Maximum in $\mathcal{O}(n)$
- Falls das immer i \mathcal{O}(\log n) ginge, hätten wir ein $n \log n$ Verfahren
- Idee: Stelle das jeweils nächste Maximum in $\mathcal{O}(\log n)$ ganz nach vorne  
- "eigentlich ist das HeapSort ein SelectionSort"
- HeapSort baut die Daten während dem Duchlaufen schon ein wenig um: *Das größte Element steht immer ganz links, siehe Bild*

Eigenschaften aus Quiz:
- Funktioniert in-place
![Idee](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/idee.png)

- Wie können wir Daten so umbauen, dass das größte Element immer links steht:
![Heap-Struktur](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/heapstruktur.png)

- Min Heap: Oben steht das kleinste Element
- Max Heap: Oben steht das größte Element

## HeapSort Ablauf
![Ablauf](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/ablauf.png)
Heap Aufbau: Bilder auf Slides 39 / 152: 
[Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_123-210.pdf)
- letzter Schritt: Tausche Wurzel mit dem letzten Element (das das ganz links steht), (hier die 21, diese nehmen wir dann aus dem Heap raus)
- dann wieder Heap aufbauen
- wdh. bis alle Elemente sortiert sind

![Heapaufbau](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/beispiel.png)
![Heapify](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/heapify.png)

## Heapaufbau
![Heapaufbau](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/aufbau.png)
Im Array sollte dann von jedem Element $i$ das jeweils $i+2, i+3$ Element kleiner sein (siehe Bild oben)

## Komplexität Heapaufbau
![Heapaufbau Komplexität 1](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/komplexHeap.png)
![Heapaufbau Komplexität 2](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/komplexHeap2.png)
![Heapaufbau Komplexität 3](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/HeapSort/komplexHeap3.png)

## Komplexität HeapSort
- Annahme: Daten liegen in Arr vor
- "Heapify:" $\mathcal{O}(n)$
- Für jeden der $n$ Knoten (weil jeder mal Wurzel wird):
	- Tauschen mit dem letzen Knotem $\mathcal{O}(1)$
	- Heapeigenschaft reparieren, Vertauschungen entlang eines Pfades im Baum; $\mathcal{O}(\log n)$
	- Insgesamt; $\mathcal{O}(n \log n)$
