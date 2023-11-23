**SLIDES:**
[Enzym Kinetik Slides](file:///home/malte/OneDriver/01_Studium/3.Semester/BioChemie2/Slides/BC2_231030_lokal.pdf)


# Michaelis-Menten-Gleichung
$S + E \rightleftharpoons^{k1}_{k-1} ES \rightleftharpoons^{k2}_{k-2} E + P$

## Vorraussetzungen
1. Anfangsgeschwindigkeit →  $[P] \approx  0 \to k_{2}$ vernachlässigbar
2. "Fließgleichgewicht": Die erste Reaktion ist sehr viel schneller als die zweite: 
   $v = k_{2} \cdot [ES]$ / $V = \frac{d[P]}{dt}$ 
   Fließgleichgewicht →  $\frac{d[ES]}{dt} = 0$ →  Bildung = Zerfall
   $$
   [S] \cdot [E] \cdot k_{1} = [ES] \cdot (k_{2} + k_{-1})
   $$
3. Bedingung: Substratüberschuss: 
   $$
   [S] \approx [S] - \underbrace{[ES]}_{\text{So Klein, dass man es vernachlässigen kann}}
   $$
   Für das Enzym gilt: 
   $$
   [E] = [E_{t}] - [ES] 
   $$
   $$
   \begin{align}
   [S] \cdot [E] \cdot k_{1} &= [ES] \cdot (k_{2} + k_{-1}) \hspace{20mm} \text{(Aus 2.)}\\
   [ES] &= \frac{[S][E] \cdot k_{1}}{k_{2}+ k_{-1}} \underbrace{\iff}_{K_{m}= \frac{k_{2}+k_{-1}}{k_{1}}} \\
   [ES] \cdot k_{m} &= [E] \cdot [S] \iff\\
   [ES] \cdot k_{m} &= ([E_{t}] - [ES]) + [S] \iff\\
   [ES] \cdot \frac{(k_{m} + [S])}{k_{m}} &= \frac{[E_{t}] \cdot [S]}{k_{m}} \iff \\
   [ES] &= \frac{[E_{t}] \cdot [S] \cdot k_{m}}{k_{m} \cdot (k_{m} + [S])} \\
   [ES] &= [E_{t}] \cdot \frac{[S]}{k_{m} + [S]}\\
   v_{0} &= k_{2} \cdot [ES] = k_{2} \cdot [E_{t}] \cdot \frac{[S]}{k_{m} +[S]} \implies \\
   &\underbrace{v_{0} = \frac{v_{max} \cdot [S]}{k_{m}+[S]}}_{\text{Michaelis-Menten-Gleichung}} 
   \end{align}
   $$ 
   
## Ausnahmen: Nicht alle Enzyme folgen der Michaelis-Menten-Gleichung
**Hämoglobin vs Myoglobin**
- Bindungscharakteristik von Hämoglobin ist abhängig von dem Druck von Sauerstoff. Kann bei niedrigem Druck Sauerstoff schlechter binden als Myoglobin.
- T vs R vorm: eine hat eine hohe Affinität für Sauerstoff, die andere eine niedrige. →  $k_{m}$ ist dann keine Konstante mehr, sondern eine Funktion von Sauerstoffdruck.
- Ein entsättigtes Hämoglobin, dass O2 aufnimmt, begünstigt die Bindung von weiterem O2. →  Positive Kooperativität
- **Hämoglobin muss möglichst viel O2 direkt in den Lungensäcken aufnehmen. Dort herrsch ein hoher Sauerstoffdruck. →  Hämoglobin muss dort eine hohe Affinität für O2 haben.**
- **In den Geweben herrscht ein niedriger Sauerstoffdruck. →  Hämoglobin muss dort eine niedrige Affinität für O2 haben, um es abzugeben.**

# Kontroll Theorie
## Proportional
![3_BioChem_3_KT_Proportional](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_BioChem_3_KT_Proportional.png)
## Differential
![3_BioChem_3_KT_Differential](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_BioChem_3_KT_Differential.png)
## Integral
![3_BioChem_3_KT_Integral](/home/malte/01_Documents/Vimwiki_md/UNI/SCREENSHOTS/3_BioChem_3_KT_Integral.png)



