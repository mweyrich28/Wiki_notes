# Sortieren
:sort:

- Vl_1 →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_122.pdf)
- Ausbesserung Slide 67: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Ausbesserungen/3-Sortieren-67.pdf)
- Vl_2 →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_123-210.pdf)
- Übung →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Übungsblätter/AlgoDat_SoSe23_Übungsblatt3.pdf)

## Totale Ordnung Wdh
- Reflexiv
- Transitiv
- Antisymmetrisch
- Totalität: $x \le y \lor y \le x$

## Vergleichskriterien für Sort Algorithmen
- *Berechnungsaufwand:*
	- $\mathcal{O}(n^{2}), \mathcal{O}(n \log(n)), \mathcal{O}(n)$
- *WorsCase vs. Avg.:*
	- Ausnutzen von Vorsortierungen
- *Speicherbedarf:*
	- In-place
	- Kopieren
- *Stabilität:*
	- Erhalt der Reihenfolge von gleichwertigen Schlüsseln

## Übersicht von Sort Algorithmen
**Einfache**
- [BubbleSort](2_ADS_BubbleSort)
- [SelectionSort](2_ADS_SelectionSort)
- [InsertionSort](2_ADS_InsertionSort)
**Höhere**
- [MergeSort](2_ADS_MergeSort)
- [QuickSort](2_ADS_QuickSort)
- [HeapSort](2_ADS_HeapSort)
**Spezielle**
- [CountingSort](2_ADS_CountingSort)

*Sortieren geht nicht schneller als* $n \log n$ *!*:
- Diskussion ab Slide 77 / 199 [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/3-Sortieren_123-210.pdf)
- Entscheidungsbaum: Innere Knoten: Vergleiche, Blätter: alle möglichen Permutationen des Arrays
![Untere Schranke Worst-Case](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/untereschrankeWorstCase.png)

## Modernes effizientes Sortieren
![Modernes Sortieren](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/modSortieren.png)

## Fazit
![Fazit](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/fazit.png)
