# CountingSort
:algorithm:sort:counting_sort:

*Idee:*
- Angenommen, die Schlüssel sind darstellbar als ganzzahlige Werte im Bereich $0,\dots,m-1$
- Bsp. Sortieren aller eingeschriebener Studenten anhand des Studiensemesters
- Wir können ein Histogramm erstellen und zählen für jeden Schlüsselwert eine Häufigkeit
- Diese Häufigkeit liefert die Position für jeden Record
- Bewege nun die Records an ihre erreichte Position

*BEISPIEL:*
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/CountingSort/bsp.png)

## Komplexität
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Sort/CountingSort/komp.png)
