# InsertionSort
:insertion_sort:algorithm:sort:

*Idee:*
- Hält die linke Teilfolge Sortiert
- Füge nächstes Objekt hinzu, indem es an die korrekte Position eingefügt wird
- Wiederhole dies, bis Teilfolge aus der gesamten Liste besteht
- Bsp →  [4, 5, 7, 8, 9, 11, 20, 21, 22, 23, 25, 28, 2, 1, 13, 12, 14, 15, 6, 17, 10, 29, 16, 18, 24, 19, 0, 3, 27, 26]:
	- Linke Teilfolge zwar sortiert, jedoch gibt es immer noch Elemente in der rechten Teilfolge, die kleiner sind als das 1. Element links
	- Indiz für InsertionSort, bei [2_ADS_SelectionSort](2_ADS_SelectionSort)
 wäre in der Linken Teilfolge das aller kleinste Element links!

## Implementiert in Java
```java
	public void insertionSort(int[] a){
		for(in i = 1; i < a.length; i++){
			int key = a[i];
			int j = i;
			// Merke dir den Wert der nicht einsortiert ist (key). 
			// Dann schieben wir alles links stehend (was größer als key ist) um eins nach rechts.
			while(j > 0 && a[j-1] > key){ 
				a[j] = a[j-1];          
				j--;
			}
			a[j] = key; // füge den key dort ein, wo das letzte Element war, welches > als unser key ist
		}
	}
```
[Slides](/home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_122.pdf) ab Seite 44

### Variante mit Sentinel (= Wächterelement)
![Implementiert mit Wächerelement](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/InsertionSort/Sentinel.png)

## Komplexitätsanalyse Vergleiche
- Anzahl der Vergleiche
	- Abhängig von Vorsortierung
	- Im best Case: $\mathcal{O}(n)$ Vergleiche bei sortierter Folge
	- Avg. Case und worst Case: $\mathcal{O}(n^{2})$

## Komplexitätsanalyse Verschiebeoperationen
- Anzahl der Vertauschungen:
	- Best Case: Folge ist sortiert →  man benötigt keine Verschiebungen
	- Worst Case: Folge ist Absteigend sortiert und das $j$-te Element wird mit $j-1$ Operationen an den jeweiligen
	  Anfang geschoben: $\frac{n(n-1)}{2} \in \mathcal{O}(n^{2})$
	- Average Case: $\frac{n(n-1)}{4} \in \mathcal{O}(n^{2})$
