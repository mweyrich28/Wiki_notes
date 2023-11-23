# MergeSort
:merge_sort:algorithm:sort:divide_and_conquer:

*Idee:*
- Zerlege die Eingabenfolge in zwei gleichlange Folgen. Diese lassen sich dann unabh. von einander sortieren
- Anschließend werden beide Teilfolgen zusammengeführt
- Rekursiv können diese Schritte auch auf die Teillisten angewendet werden
- *Divide and Conquer*

## Implementiert in Python (rekursiv)
```python
	def merge(array, lefthalf, righthalf):
		i, j, k = 0, 0, 0
		while i < len(lefthalf) and j < len(righthalf):
			if lefthalf[i] <= righthalf[j]:
				array[k] = lefthalf[i]
				i=i+1
			else:
				array[k] = righthalf[j]
				j=j+1
			k=k+1
			while i < len(lefthalf):
				array[k] = lefthalf[i]
				i=i+1
				k=k+1
			while j < len(righthalf):
				array[k] = righthalf[j]
				j=j+1
				k=k+1


	def mergeSort(array):
		if len(array) > 1:
			mid = len(array) // 2
			lefthalf = array[:mid] - 0 bis mid-1
			righthalf = array[mid:] - mid bis len(array)

			mergeSort(lefthalf)
			mergeSort(righthalf)
			merge(array, lefthalf, righthalf)
```
[Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_122.pdf): Bilder ab Slide 93.

## Komplexitätsanalyse direkt
- Wie viele Vergleiche werden benötigt?
	- In der *Divide-Phase* wird nichts verglichen
	- In der *Merge-Phase* werden $\log_{2}(n)$ Baumebenen bearbeitet (Wdh: Binärbaum mit $n$ Knoten hat maximal Höhe $h = \log_{2}n$)
	- Auf jeder Baumebene finden höchstens $n$ Vergleiche statt und genau $n$ Verschiebungen (Kopiervorgänge) statt

![Baumdarstellung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/MergeSort/m1.png)

## Komplexitätsanalyse mit Master-Theorem
- Für ein Array der Länge $n > 1$ beträgt die Laufzeit $T_{ms}(n)$ von MergeSort:
	- $T_{ms}(n) = 2 \cdot T_{ms}( \frac{n}{2}) + T_{merge}(n)$
	- und $T_{ms}(n) = const$ für $n \le 1$
- Auf diese rekursive Gleichung lässt sich das Master-Theorem anwenden:
	- Parameter $a = 2$ und $b = 2$
	- Die Funktion $merge$ läuft *genau einmal* über die Arrays jeder Ebene: $T_{merge}(n)\in \mathcal{O}(n)$
	- Also insgesamt: $T_{ms} \in \mathcal{O}(n \cdot \log n)$
