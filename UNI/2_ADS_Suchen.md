# Suchen
:ads_suchen:suchen:

I) Vl →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/4-Suchen_66.pdf)
ACHTUNG: Slide 8: [Slides](file:///home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/verbeserung.png)
II) →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/4-Suchen_67-99.pdf)
III) →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/4-Suchen_100-127.pdf)

## Einfache Suchverfahren

### Lineare Suche
```python
def linSearch(S, searchkey):
	for key, value in S:
		if key == searchkey:
			return value
```
Falls Schlüssel enthalten ist: im Mittel: $\frac{n}{2}$

$\implies \mathcal{O}(n)$

### Binäre Suche
```python
def binSearch(S, searchkey):
	if len(S) > 0:
		mid = len(S)//2
		key, value = S[mid]
		if searchkey < key:
			return binSearch(S[:mid], searchkey)
		elif searchkey > key:
			return binSearch(S[mid+1:], searchkey)
		else: # searchkey == key
			return value
```
Falls Liste nicht sortiert ist, entsteht Zusatzaufwand $\mathcal{O}(n\log n)$
- Daher v.a geeignet für sortierte Daten
- Daten, die sich selten ändern
Wenn die Daten sortiert sind: 
- $\mathcal{O}(\log n)$
- Bei jedem Durchlauf halbiert sich der durchsuchte Bereich: $T(n) = T(\frac{n}{2}) + 1$

→  *Damit ist die Komplexität* $\mathcal{O}(\log n)$ *- auch im Worst-Case*

#### Suffixarray
![Suffix Array](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/suffixarray_1.png)
**Komplexität:**
- $\mathcal{O}(\log |S|)$ Schritte für die Suche (binäre Suche)
- $\mathcal{O}(|P|)$ Zeichenvergleiche in jedem dieser Schritte
- Insgesamt: $\mathcal{O}(|P|\log |S|)$ Zeichenvergleiche insgesamt mit $\mathcal{O}(|S|)$ Speicher

### Interpolationssuche
- Idee: Schätze die Position, wo Suchschlüssel ungefähr liegt
- Annahme: Schlüssel sind sortiert im Datensatz & Elemente sind gleich verteilt
```python
def interpolSearch(S, searchkey):
	low, high = S[0][0], S[-1][0]
	if low <= searchkey <= high:
		i = (searchkey-low)*(len(S)-1)//(high-low)
		key, value = S[i]
		if searchkey < key:
			return interpolSearch(S[:i], searchkey)
		elif searchkey > key:
			return interpolSearch(S[i+1:], searchkey)
```
![Abschätzung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/interpolSearch.png)

*"Wenn ich einen Schlüssel a suche, dann steht er an der Stelle i"*

→  Sehr ähnlich zur binären Suche, lediglich schätzen wir hier ab, wo die "richtige Mitte" ist

#### Worst Case Beispiel
![Worst Case](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/wcInterpolation.png)
Hier hätte die Gerade eine sehr flache Steigung →  (0,1), (1,2), (2,3), (3,4), (4,5), (5,6), (6,7), (7,8), (8,9), (9,100)

→  Schlüssel sind nicht gleich verteilt

### Zusammenfassung einfache Suche
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/ueberblick.png)

## Binärer Suchbaum vs Heap
![Binärbaum vs Heap](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/binbaumvsheap.png)

### Binäre Suchbäume Fazit
![Komplexität](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/binBaumKomp.png)
![Fazit](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/binBaumFazit.png)

## AVL-Bäume
[2_ADS_AVL_Bäume](2_ADS_AVL_Bäume)

# Sekundär Speicher
:sekundärspeicher:

I) →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Algorithmen und Datenstrukturen/Slides/4-Suchen_67-99.pdf)

**Zugriffszeit Festplatten:**
- Suchzeit[ms]: Armpositionierung
- Latenzzeit[ms]: Rotation bis Blockanfang
- Transferzeit[ms/MB]: Übertragung der Daten

![Zugriffszeit](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/sekundärSpeicher1.png)

## B-Baum
![B-Baum](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/bbaum.png)
> **Blätter sind alle auf der selben Ebene: wie erhalten wir diese Struktur beim Einfügen?**

![Struktur](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/bbaumStruktur.png)
![B-Baum Suche](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/bbaumSuche.png)

### B-Baum Höheneigenschaften
- Wurzel: $1 \le$ #Schlüssel $\le 2k, 2 \le $ #Verweise $ \le 2k+1$
- Knoten: $k \le $ #Schlüssel  \le 2k, k+1 \le $ #Verweise $ \le 2k+1$

### Wie viele Schlüssel sind mindestens in einem B-Baum der Ordnung k erhalten?
![Knoten und Schlüssel B-Baum](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/höhenAbsc.png)
- Minimale Schlüsselanzahl $s_{min} = 2(k+1)^{h}-1$
- Maximale Höhe: $h \le \log_{k+1} \frac{s+1}{2}$

#### Wie viele Schlüssel sind maximal in einem B-Baum der Ordnung k enthalten?
![B-Baum Höhenabschätzung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/höhenAbscMax.png)

### B-Baum Einfügen
![Einfügen](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/bbaumEinfügen.png)

### B-Baum Löschen Konzepte
Bei Unterlauf nach entfernen von N:
1) N ist Wurzel →  Baum ist leer 
2) N hat Nachbarn M mit mehr als $k$ Schlüssel 
![Ausgleich](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/bbaumAusgleich.png)
3) N hat Nachbarn M mit genau $k$ Elementen → 
![Verschmelzen](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/bbaumVerschmelzen.png)
Verschmelzen ist das Inverse zum Split

## B^+ - Baum
- ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/bplusbaum.png)

## R-Baum
- R →  Rechteck
- ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/rbaum.png)


# Bitvektoren
:bitvektoren:hashing:

> Geeignet für kleinen Suchwert Bereich: z.B. String ungeeignet, da |Alphabet|=26

**Operationen:**
- Insert, Delete: $\mathcal{O}(1)$
- Search: $\mathcal{O}(1)$
- Initialize: $\mathcal{O}(N)$ → Setzt alle Werte auf 0
**Speicherbedarf:**
- Anzahl Bits: $\mathcal{O}(N)$ maximale Anzahl an Elementen

## Hashing
**ZIEL:**
- Zeitkomplexität Suche $\mathcal{O}(1)$ (wie bei Bitvektor-Darstellung), Initialisierung: $\mathcal{O}(1)$

**AUSGANGSPUNKT:**
- Bei Bitvektor-Darstellung wird der Schlüsselwert direkt als Index in einem Array benutzt

**GRUNDIDEE:**
- Oft hat man ein sehr großes Universum (z.B. Strings), aber nur eine kleine 
  Objektmenge (Straßennamen einer Stadt), für die ein kleines Array ausreichend wäre

**IDEE:**
- Bilde verschiedene Schlüssel auf dieselben Indexwerte ab, *dadurch Kollision möglich* (da nicht injektiv)

**GUNDBEGRIFFE:**
- $U$ ist das Universum aller Schlüssel
- $S \subseteq U$ die Menge der zu speichernden Schlüssel mit $n = |S|$
- $T$ die Hash-Tabelle der Größe $m$

**HASHFUNKTION:**
- Berechnung des Indexwertes zu einem Schlüsselwert $x$
- Schlüsseltransformation: $h: U \to \left\{0,\dots,m-1\right\}$
- $h(x)$ ist der Hash-Wert von $x$

**HASHING WIRD ANGEWENDET WENN:**
- $|U|$ sehr groß
- $|S| << |U|$, Anzahl der zu speichernden Elemente ist viel kleiner als $|U|$

→  ![Hashing](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/hashing.png)

### Anforderung an eine Hashfunktion
- ℎ: 𝑑𝑜𝑚𝑎𝑖𝑛 𝐾 → 0, 1, … , 𝑚 − 1 soll surjektiv sein.
- ℎ 𝐾 soll effizient berechenbar sein, idealerweise in 𝑂(1).
- ℎ 𝐾 soll die Schlüssel möglichst gleichmäßig über den Adressraum verteilen, um dadurch Kollisionen zu vermeiden (Hashing = Streuspeicherung).
- ℎ 𝐾 soll unabhängig von der Ordnung der K sein in dem Sinne, dass
  in der Domain „nahe beieinander liegende“ Schlüssel auf nicht nahe
  beieinander liegende Adressen abgebildet werden.

**HASHFUNKTIONEN:**
- $h(x) = K \bmod m$ (für numerische Schlüssel)
- $h(x) = ord(K) \bmod m$ (für nicht numerische Schlüssel)

**PERFEKTE HASHFUNKTION:**
- $h(x)$ ist perfekt, wenn für $h: U \to \left\{0,\dots,m-1\right\}$ mit $S=\left\{k_{1}, \dots,k_{n}\right\}\subseteq U$ gilt:
$$
h(k_{i}) = h(k_{j}) \iff i = j
$$
**MINIMALE HASHFUNKTION:**
- $m = n$, es werden genau so viele Plätze wie Elemente benötigt

→  Kollisionen lassen sich schwer vermeiden: Seite 17 / 116

→  Speicherplatz $m$ wächst quadratisch mit $n$ (Zahl der Elemente), also wenn wir $n^{2}$, so müssen wir $m^{4}$

### Umgang mit Kollisionen
![Offenes Hashing mit geachlossener Addressierung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/offenHash.png)
![Geschlossenes Hashing mit offener Adressierung](/home/malte/01_Documents/vimwiki/Assets/2.Semester/ADS/Suchen/geschlossHAshing.png)

