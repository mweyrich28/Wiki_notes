# BubbleSort
:bubble_sort:algorithm:sort:

*Idee:*
- Vergleiche Paare von benachbarten Schlüsseln
- Tausche, falls links > rechts
- Wie Luftblasen →  Die größten Elemente treiben nach "oben" (rechts):
	- [2, 5, 3, 8, 9, 14, 7, 4, 13, 15, 17, 19, 0, 10, 11, 20, 21, 1, 22, 18, 23, 16, 6, 12, 24, 25, 26, 27, 28, 29]

## Implementiert in Java
```java
	public void bubblesort(int[] a){
		int n = a.length;
		for(int i = 0; i < n; i++){
			for(int j = 0; j < n-i-1; j++)	{ // Nach dem ersten Durchlauf schauen wir uns nur noch n-1 Elemente an, da im ersten
				if(a[j] > a[j+1]){			  // Durchlauf, das größte Element nach ganz rechts verschoben worden ist! 
					swap(a,j,j+1)	
				}
			}
		}
	}
```
## Komplexitätsanalyse Vergleiche
- Anzahl der Vergleiche
	- Unabhängig von der Vorsortierung der Folge →  Worst Case, average Case und best Case sind identisch
	- Im i-ten Durchlauf werden n-i+1 Elemente betrachtet und n-i Paare verglichen, insgesamt: $\displaystyle\sum^{n}_{i=1} (n-1) = \displaystyle\sum_{i = 0}^{n-1}i = \mathcal{O}(n^{2})$

## Komplexitätsanalyse Vertauschungen
- Anzahl der Vertauschungen:
	- Best Case: 0 Swaps *(Vorsortierung)*
	- Worst Case: $\frac{1}{2}(n^{2}-n)$ Swaps *(Invertierte Reihenfolge)*
	- Average Case: $ \frac{1}{4} (n^{2}-n)$ Swaps
