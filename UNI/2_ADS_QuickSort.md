# QuickSort
:quick_sort:algorithm:sort:

*Idee:*
I) Wähle ein "Pivotelement" $p$ aus der Folge aus
II) Zerlege die Folge in zwei Teilfolgen:
	- Teilfolge 1: Enthält alle Elemente $x \le p$
	- Teilfolge 2: Enthält alle Elemente $x > p$
III) Sortiere rekursiv auf den Teillisten mit QuickSort
IV) Einelementige Listen sind schon sortiert
V) Im gegensatz zu [2_ADS_MergeSort](2_ADS_MergeSort):
	- Aufwand liegt im "Divide-Schritt"
	- Merg-Schritt ist lediglich Konkatenation (da alles bereits richtig sortiert ist)

## Implementiert in Python
Wir benutzen das letzte Element als Pivot!
```python
def quick_sort(arr, low, high):
    print(arr)
    if low < high:
        pi = partition(arr, low, high) - ←  Positon des Pivots
        quick_sort(arr, low, pi-1) - Rekursion
        quick_sort(arr, pi+1, high) - Rekursion

def partition(arr, low, high):
    i = low - wir fangen ganz links an
    pivot = arr[high] - Pivot
    
    for j in range(low, high): - wir durchlaufen von low bis high
        if arr[j] <= pivot: - arr[j] <= pivot? 
            arr[i], arr[j] = arr[j], arr[i] - swap  [i] with [j]: [1,5,3] →  [1,3,5]
            i += 1 - Pivot eins weiter, da kleiner
    arr[i], arr[high] = arr[high], arr[i] - Pivot an die richtigen Stelle Tauschen, nachdem wir alle vergleiche gemacht haben 
    print(arr)
    return i
```
[Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_123-210.pdf): Bilder ab Slide 3

![Visualisierung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/bild1.png)
![PivotSort mit letztem Element](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/visGN1.png)
![Median of Three](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/visGN2.png)
## Komplexitätsanalyse Vergleiche
**Anzahl der Vergleiche**
- Best-Case: Die Folge zerfällt immer in zwei gleich große Teile: Mastertheorem $\mathcal{O}(n\log_{2}n)$: 
![Best Case](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/bestcase.png)
![Best-Case](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/mastertheorem.png) 
**Worst-Case: Die Folge zerfällt schlimmstenfalls immer in:**
- eine leere Folge
- und eine Folge der Länge $n-1$
![Situation](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/worstcase.png)
- Mit Master-Theorem gilt: $T(n) \in \mathcal{O}(n^{2})$: genau so langsam wie BubbleSort, InsertionSort, SelectionSort

**Average-Case**
- Annahme: alle $n$ Schlüssel sind verschieden
- Die Wahrscheinlichkeit der Eingabeanordnung sei $\frac{1}{n!}$
- Jede der $n!$ Permutationen ist gleich wahrscheinlich: Slides Seite 25 / 147
- Wir können die Länge zu $L_{1} = \frac{3}{4}n$ abschätzen
- $L_{1} = \frac{3}{4}n, L_{2} = \frac{1}{4}n$
- Der längste Rekursionspfad besteht aus $\log_{\frac{4}{3}}n$ Knoten
- Jedes Level des Aufrufbaums nutzt $\mathcal{O}(n)$ Vergleiche
- Damit ergibt sich insgesamt: $\mathcal{O}(n \log n)$

## Wie wähle ich das Pivot Element?
![Pivot](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/pivotelem.png)
![Median als Pivot](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/pivot1.png)
- Durch die Berechnung des Medians machen wir unsere Laufzeit kaputt →  Fällt in der Praxis raus
![Median of Three](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/pivot2.png)
![Random Pivot](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/QuickSort/pivot3.png)
