# Effizienz und Komplexität
:effizienz:effektivit:komplexität:big_o:o_notation:rekursion:mastertheoreme:divide_and_conquer:substract_and_conquer:

- Vl →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/2-Komplexität.pdf)
- Übung →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Übungsblätter/AlgoDat_SS23_Tutorium2.pdf)

## Definitionen
- _Effektivität_: 
	- Algorithmus liefert gewünschtes Ergebnis
	- das *Ziel* wird erreicht.
- _Effizienz_: Wirtschaftlichkeit im Ressourcenverbrauch, nicht zu viel Aufwand betreiben.
	- Effizienzmaße: Rechenzeit, Speicherplatzbedarf, Zugriffe auf Sekundärspeicher (z.B. Festplatte, I/O), Kommunikationsaufwand (z.B. Netzwerk, I/O), Energieverbrauch.
	- Laufzeit hängt von: Takt der CPU, Länge der Eingabe, Implementierung der Basisoperationen ab.

## O-Notation
- Formale Formel: $\mathcal{O}$-Notation: $\mathcal{O}(f) = \{g:\mathbb{R} \to \mathbb{R}| \exists_{c > 0}; \exists_{x_{0} > 0}: \forall x \ge x_{0}: |g(x)|\le c \cdot |f(x)|\}$
- In der Informatik: $\mathcal{O}$-Notation: $\mathcal{O}(f) = \{g:\mathbb{N} \to \mathbb{R}| \exists_{c > 0}; \exists_{n_{0} > 0}: \forall n \ge n_{0}: |g(n)|\le c \cdot |f(n)|\}$
- Sprechweise:
	- $f$ ist obere Schranke von $g$
	- $g$ wächst höchstens so schnell wie $\mathcal{O}(f)$

Beispiel SummeBis:
```java
int summeBis(int n){
	int sum = 0; // 1 Operation
	for(int i = 0; i<n; i++){// 1 + 2n Operationen
		sum += 1;	// Je 1 Operation
	}
	return sum; // 1 Operation
}
```
Es werden $2 + 3 \cdot n +1 = 3n +3$ Basisoperationen verwendet

### Regeln
$$
\mathcal{O}(\log(n)) = \mathcal{O}(\log_{2}(n)) = \mathcal{O}(ln(x))
$$
- wegen $b = a^{\log_{a}b}$ gilt: $a^{\log_{a}n} = n = b^{\log_{b}n} = a^{(\log_{a}b) \cdot \log_{b}n}$
- $\log_{a}n (\log_{a}b) \cdot \log_{b}n = const \cdot \log_{b}n$
$$
g_{1} \in \mathcal{O}(f_{1}) \land g_{2} \in \mathcal{O}(f_{2}):	g_{1} + g_{2} \in \mathcal{O}(max(f_{1}, f_{2}))\\
g_{1} \in \mathcal{O}(f_{1}) \land g_{2} \in \mathcal{O}(f_{2}):	g_{1} \cdot  g_{2} \in \mathcal{O}(f_{1} \cdot f_{2})
$$	
### Tabelle
![Überblick](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/komplexitätsklassen.png)

#### Beziehungen zwischen Komplexitätsklassen
![Beziehungen](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/komplexitätsklassen_beziehungen.png)

## Fib Zahlen Python
### Endständige Rekursion
```python
def fib(n, res=1, prev=0): - Endständige Rekursion
	if n ## 0:
		return prev
	return fib(n-1, res + prev, res)	
```
Gibt: $\mathcal{O}(n)$

![Ablaufsprotokoll](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Algorithmen/fib_python_o_n.png)
## Master-Theoreme
Bei rekursiven Algorithmen: Big_O ist schwer zu bestimmen, deshalb haben wir Master-Theoreme

### Master-Theorem: Divide and Conquer
![Divide and Conquer](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Master_Theoreme/divideandconquer.png)

Wenn wir solche Gleichungen haben:
- a = Wie oft führe ich $T$ durch?/ Wie viele Aufrufe haben wir?
- b = In wie viele Teile schneide ich das Array?
- Dann schauen wir in was bei $\log_{b}a$ rauskommt und *davon abhängig entscheiden* wir die Komplexitätsklasse

*Beispiel:*

Sei $T(n) = T( \frac{n}{2}) + n$ und $T(1) = c_{0}$:

$c = c_{0}$

$a = 1, b = 2, \\ f(n) \in \mathcal{O}(n^{1}) \implies \underbrace{d = 1 > 0}_{\text{d ist der Exponent in } n^{1}}  = \log_{2}1 \implies T(n^{1}) \in \mathcal{O}(n)$

*In Klausur: Mastertheoreme anwenden, Faktoren richtig bestimmen*

### Master-Theorem: Verallgemeinerung für $f(n) \in \mathcal{O}(n^{d})$
![Verallgemeinerung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Master_Theoreme/verallgemeinerung.png)

### Master-Theorem Substract And Conquer
![Substract and Conquer](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Master_Theoreme/subandcon.png)

### Substitution
Idee: Schwierige Ausdrücke auf bekannte zurückführen

*Beispiel:*

$T(n) = 2 \cdot T(⌊\sqrt{n}⌋) + \log n$

- Substituiere: $m = \log n$, ergibt: $T(2^{m}) = 2 \cdot T(2^{ \frac{m}{2}})+m$
- Setze $S(m) = T(2^{m})$
- Ergibt: $S(m) = 2 \cdot S( \frac{m}{2}) + m$
- Mit Master-Theorem: $S(m) \in \mathcal{O}(m \log m)$
- Rücksubstitution: $T(n) = T(2^{m}) = S(m) \in \mathcal{O}(m \log m) = \mathcal{O}(\log n - \log \log n)$ 
