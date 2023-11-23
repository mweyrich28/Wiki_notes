# Grundlagen 1 Algorithmen & Datenstrukturen
:algorithmen:datenstrukture:garbage_collection:pointer:traversierung:binärbaume:binärbaum:

VL →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/1-Grundlagen.pdf)
Übungsblatt →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Übungsblätter/AlgoDat_SS23_Übungsblatt1.pdf)

Fehler Folie 9:
```python
for i in range(n+1): - nicht range(n) →  da range(n) = [0, ..., n-1]
	...
```
 
## Algorithmen
- [[EiP Der Algorithmus|Eigenschaften]] nochmal wiederholt
 
## Datenstrukturen
- Pointer, z.B. sort Algorithmen viel effizienter, da nur mit den Adressen gearbeitet wird, kein unnötiges kopieren nötig
- Garbage collection in Java:
- Sobald keine Referenzen oder Verweise auf eine Speicherzelle zeigen, wird sie wieder freigegeben

 
## Binärbaum

| $\textbf{Wurzelgrad}$ | Anzahl an Kinderknoten |
| ---                   | ---                    |
| 0                     | 0                      |
| 1                     | 1                      |
| 2                     | 2                      |

### Eigenschaften
$$
\boxed{t = \text{Binärbaum}, \underbrace{h = Höhe}_{\text{Knotenlänge, mit Wurze}}}
$$
1) $t$ hat maximal $2^{h+1}-1$ Knoten
2) $t$ hat mindestens $h+1$ Knoten
3) $t$ hat maximal $2^{h-1}$ Blätter
4) $t$ hat maximal $2^{h}$ Blätter

### Baumtraversierung
![Überblick](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/traversierungen.png)

#### Preorder
```java
public static void printNodes(BinarySearchTree root){

    System.out.println(root.value);
	
    if(root.leftchild != null) {
        printNodes(root.leftchild);
    }
	
    if(root.rightchild != null){
        printNodes(root.rightchild);
    }
}
```	
#### Inorder
```java
public static void printNodes(BinarySearchTree root){

    if(root.leftchild != null) {
        printNodes(root.leftchild);
    }
	
    System.out.println(root.value);
	
    if(root.rightchild != null){
        printNodes(root.rightchild);
    }
}
```
#### Postorder
```java
public static void printNodes(BinarySearchTree root){

    if(root.leftchild != null) {
        printNodes(root.leftchild);
    }
	
    if(root.rightchild != null){
        printNodes(root.rightchild);
    }
	
    System.out.println(root.value);
}
```

#### Breadth-First (Breitendurchlauf)
	- Knoten ebenenweise durchlaufen, von links nach rechts
	- Eigenschaften auf Slide 61
![Array Einbettung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/breadth_first.png)
