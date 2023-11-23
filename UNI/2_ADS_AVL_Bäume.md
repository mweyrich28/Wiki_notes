# AVL-Bäume
:avl_bäume:

## Definition
**Binärbaum mit gewissen Eigenschaften:**
> Für alle Knoten gilt, dass die Höhen der beiden Teilbäume sich höchstens um eins unterscheiden

![Beispiel](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/AVL_bsp.png)
![Rekursive Def AVL](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/AVL_def.png)

## Minimal gefüllte AVL-Bäume
*Es gilt:*
$$
N(h) = \begin{cases} 1, h = 0 \\ 2, h=1 \\ \underbrace{N(h-1) + N(h-2) + 1}_{\text{Fast wie fib}}, h>1 \end{cases}
$$

→  Die Anzahl an Knoten wächst exponentiell in Abhängigkeit der Höhe →  das ist gut, da wir möglichst 
viele Daten in einem Baum möglichst niedrigen Baum (also niedrige Höhe) speichern wollen

→  Ein AVL Baum ist maximal 44% höher als ein maximal ausgeglichener binärer Suchbaum, 
aber nicht schlimmer (also ist immer noch $\log_{2}$ im worst case)

## Balance
- Knoten speichert *Höhendifferenz*(balance) $b$
- $b := \text{Höhe (Rechter Teilbaum)-Höhe (Linker Teilbaum)}$: 

![Balance](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/avl_balance.png)

- $b = -1:$ Links ist der Teilbaum um eins größer als der rechte
- $b = 1:$ Rechts ist der Teilbaum um eins größer als der linke
- Sobald $b < -1 \lor b > 1$ ist das AVL-Kriterium verletz

### Einfachrotation
![Einfachrotation (Rechts)](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/einfachRotation.png)
→  3 Änderungen 

![Einfachrotation (Links)](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/einfachRotationLinks.png)

→  *Die rot markierten Kanten werden immer so verändert*

### Doppelrotation
→  Der problematische Baum (B2) liegt in der Mitte →  Doppelrotation

![LR-Rotation](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/doppelRotLR.png)
![LR-Rotation Anwendung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/doppelRotLRAn.png)
![Komplexität](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/kompEinfuegen.png)

## AVL-Bäume Löschen
> Löschen wie bei normalem Binärbaum, jedoch kann es sein, dass danach das AVL-Kriterium verletz wird →  falls ja müssen wir wieder Rotieren

**Beim Löschen eines Knotens wird:**
- das AVL-Kriterium wiederhergestellt, wobei die 
  Suchbaumeigenschaft erhalten bleibt
- kann es vorkommen, dass der re-balancierte Unterbaum nicht 
  die gleiche Höhe wie vor dem Löschen besitzt

→  auf dem weiteren Pfad zur Wurzel kann es zu weiteren Rebalancierungen (des obigen Typs, also immer im anderen Unterbaum) kommen

→  beim Löschen werden maximal $h$ Rotationen benötigt

**Aufwand:**
$\underbrace{\mathcal{O}(h)}_{\text{Entfernen}} + \underbrace{\mathcal{O}(h)}_{\text{Rotieren}} = \mathcal{O}(\log_{2}(n))$

# Splay Bäume
:splay_bäume:

**Grundidee:**
- Bei jeder Suche nach einem Schlüssel wird dieser durch
  Rotationen zur neuen Wurzel des Suchbaums (Operation „splay“).
- Nachfolgende Suchen verdrängen den Schlüssel wieder aus der
  Wurzel.
– Selten angefragte Schlüssel sinken dadurch schrittweise tiefer ab.	
– Häufig angefragte Schlüssel sinken nur wenig ab und werden
  deswegen schneller gefunden.

**Eigenschaften:**
- Suchen und Einfügen sind mit der Operation splay gekoppelt und führen zu einer Restrukturierung (in der Regel – wann nicht?).
- Splay-Bäume unterstützen die Operationen Suchen, Einfügen und Löschen.
- Splay-Bäume haben keine strukturelle Invariante wie die AVL-Bäume, welche für deren Effizienz verantwortlich ist.

## Splay Bäume Zusammenfassung
![Zusammenfassung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/zsm.png)
