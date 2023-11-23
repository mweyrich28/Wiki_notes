# Enzymkinetik
**Slides:** [ENZYMKINETIK](file:///home/malte/OneDriver/01_Studium/2.Semester/Biochemie I/kinetik.pdf) 

## Einführung
Enzymkinetik ist wichtig für...
- Quantitative Beschreibung enzymatischer Reaktionen u. Enzymeigenschaften
- Optimierung von Enzymreaktionen
- Identifizierung geschwindigkeitsbestimmender Schritte
- ...

## Begriffe
- $E$: Enzym
- $S$,$A$: Substrat
- $P$: Produkt
- $I$: Inhibitor
- $ES$: Enzym-Substrat-Komplex
- [$ES$]: Konzentration des Enzym-Substrat-Komplexes
- [$E_{0}$]: Gesamtkonzentration des Enzyms
- $k_{1}, k_{2}, k_{-1}, k_{a}, k_{d}, \dots$ Geschwindigkeitskonstanten
- $K_{1}, K_{j}, K_{i}, K_{d}$: Gleichgewichtskonstanten

## Enzymatische Reaktionen
Die Geschwindigkeit einer enzymatischen Reaktion hängt ab von...
- Diffusionsrate der Substrat(e), Produkt(e), Enzym
- Bindungs- und Dissotiationsrate von Substart und Produkt mit dem Enzym
- Reaktionsgesch. im aktiven Zentrum
- chemische Parameter

## Diffusionskontrollierte Reaktionen
Manche Reaktionen sind so schnell (also die Bildung des ES Komplexes), dass die 
Gesamtgeschwindigkeit durch die Diffusion von Substrat oder Produkt bestimmt wird.

## Ordnung einer Reaktion
> Ordnung einer Reaktion bezogen auf spezifische Komponente:
> Der Exponent, mit der diese Komponente in die Reaktionsgleichungen eingeht.
> Die Gesamtordnung einer Reaktion ist die Summe der Ordnungen der einzelnen Komponenten.

Bsp:
$$
\underbrace{2A + 1B \rightarrow P}_{\text{Eine Reaktion der 3. Ordnung}}
$$

### Pseudo (n-i)-te Ordnung
$$
	\begin{align}
	\text{Vor Reaktion}
	&\begin{cases}
		[A]&: 5000\\
		[B]&: 4
	\end{cases}\\
	\text{Nach Reaktion}
	&\begin{cases}
		[A]&: &\overbrace{4998}^{\text{Kaum Änderung}}\\
		[B]&: &\underbrace{2}_{\text{Änderung um Faktor 0.5 (Signifikant)}}
	\end{cases}
	\end{align}
$$
Die Reaktion ist also pseudo 1. Ordnung. $A$ liegt im Vergleich zu $B$ im Überschuss vor.
Also spricht man von einer Reaktion pseudo 1. Ordnung.

**Reaktionsschema Reaktion 1. Ordnung:**
$$
S \xrightarrow{k} P
$$
## Vereinfachte enzymatische Reaktion
![2_BioChem_VereinfachteEnzymatsicheReaktion](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/2_BioChem_VereinfachteEnzymatsicheReaktion.png)

- Diese Reaktion ist dominiert durch $k_{1}$. Der markierte Bereich schrumpft zusammen,
  jenachdem wo der Geschwindigkeitslimitierende Schritt liegt.
- "Wir beschränken uns auf Anfangsphasen": 
  - Das ist sinnvoll, da bei gerinen $c(P)$ kann ich die letzte Rückreaktion vernachlässigen (da $c(P) = 0$, anfangs).
  - Deshalb fehlt der Rückpfeil bei der letzten Rückreaktion.
- Wie schnell entsteht $P$?:
	- $v = \frac{[dP]}{dt} = k_{2}[ES]$

## Michaelis-Menten-Gleichung
![Ansatz](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/2_BioChem_MichaelsMentenGleichung.png)

$$
v = [E_{0}] \frac{k_{cat}[S_{0}]}{K_{m}+[S_{0}]} = \frac{V_{max}[S_{0}]}{K_{m}+ [S_{0}]}\\
\boxed{k_{2} = k_{cat}}\\
\boxed{K_{m} = \frac{k_{-1} + k_{2}}{k_{1}}} \text{ Michaelis-Konstante}\\
\boxed{V_{max} = [E_{0}]k_{cat}} \text{ Maximale Reaktionsgeschwindigkeit}

$$


