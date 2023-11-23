# SelectionSort
:selection_sort:algorithm:sort:

*Idee:* Suche jeweils nächstes kleinstes Element
- Durchlaufe die Folge von links nach rechts mit einem Zeiger i.
– Links von i sind die kleinsten Elemente sortiert.
– Finde in der verbleibenden Menge die Position min des nächsten kleinsten Elements
– Tausche, falls bei min kleineres Element als bei i steht.
- →  Das kleinste Element wir immer nach ganz links verschoben:
	- Bsp. →  [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 26, 24, 22, 18, 28, 27, 17, 29, 23, 21, 19, 20, 16, 25]

## Implementiert in Java
```java
	public void selectionsort(int[] a){
		for(int i = 0; i < a.length -1; i++){
			int min = i;
			for(int j = i+1; j < a.length-1; j++){ 
				if(a[j] > a[min]){			  
					min = j;
				}
			}
			if(min>i){
				swap(a,i,min);
			}
		}
	}
```
Mit dem erten Duchlauf finden wir das kleinste Element und schiben es auf a[0], und schauen dann nurnoch ab a[1]...

[Slides](/home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_122.pdf) Seite 68: Beispiel mit Bildern

## Komplexitätsanalyse Vergleiche
- Anzahl der Vergleiche
	- In jedem der $n$ Durchläufe $n-i$	Vergleiche →  $\frac{n(n-1)}{2}\in \mathcal{O}(n^{2})$
	- Durch weitere if-Abfrage (min ## i) lässt sich Anzahl der Swaps im Austausch gegen $n$ zusätzliche Vergleiche verringern

## Komplexitätsanalyse Vertauschungen
- Anzahl der Vertauschungen:
	- Best Case: $n-1$ Swaps (0 mit zusätzlicher Abfrage)
	- Worst Case: $n-1$ Swaps
	- Average Case: n-1 Swaps
- Anzahl der Swaps wächst linear: *so ist SelectionSort besonders für Folgen großer Objekte geeignet, deren Vertausch teurer sind* 
