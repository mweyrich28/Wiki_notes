# Sanger-Sequenzierung
:sanger_sequencing:sequencing:

## Funktionsweise
Wir nehmen uns ein doppelsträngiges DNA Fragment und denaturieren es.
So verbleiben wir mit einem einzelsträngigen DNA Fragment mit einer unbekannten Basensequenz. 
Die Fragmente werden in vier Reagenzgläser gegeben. Diese enthalten jeweils Desoxynukleotiden, 
DNA Polymerase, DNA Ligase und jeweils ein _Didesoxynukleotiden(ddNTPs) (Chain-terminarting ddNTPs)_
- Didesoxynukleotide:
- ddGTP, ddATP, ddCTP, ddTTP (für Guanin, Adenen, Cytosin, Thymin)
Diese agieren wie Stopper in dem Prozess der DNA Synthese. 
Also synthetisieren wir in den jeweiligen Reagenzgläsern DNA und diese wird dann von den einzelnen _ddNTPs_
an verschiedenen Stellen unterbrochen. So erhalten wir neue Fragmente mit unterschiedlicher Länge.
Diese Fragmente sind die Komplemente einzelnen Sequenz-abschnitte. 
Diese können nun der Länge nach sortiert werden und in die einzelnen Basen eingeteilt werden, 
je nach dem aus welchem Reagenzglas sie stammen:

| Länge | G | A | C | T |
|-------|---|---|---|---|
| 1     | x |   |   |   |
| 2     |   | x |   |   |
| 3     |   |   | x |   |
| 4     | x |   |   |   |
| 5     |   | x |   |   |
| 6     |   |   |   | x |

So ist unsere Sequenz: *TAGCAG*, nun bilden wir das Komplement: *ATCGTC*

- Um die Schnipsel der Länge nach zu ordnen benutzen wir den Prozess der *_Gelelektrophorese_*, 
  ein Gel, dass unter Spannung steht. Kurze Fragmente können einen weiteren Weg durch das Gel zurücklegen als größere Schnipsel. 
  Das Ergebnis wird dann aus dem Gel abgelesen.
- Dieses Verfahren eignet sich für DNA Fragmente < 500 Basen in Länge
![Sanger Sequencing](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Sequencing/Sangerseq.png)

## Nachteile
→ Arbeitsintensiv und fehleranfällig


## Modifikation
- Hier verwenden wir nur noch *ein* Reagenzglas mit den gleichen Bestandteilen. Diese mal sind *alle ddNTPs* in dem Reagenzglas 
  enthalten und sind zusätzlich *Fluoreszenzmarkiert* 
- Diese bilden wieder Schnipsel unterschiedlicher Länge (nachdem sie auch wieder Denaturiert wurden). 
  Diese Schnipsel werden anschließend in der *_Kapillarelektrophorese_* analysiert. Dazu werden sie wieder in ein Gel gegeben und 
  die jeweilige Färbung durch die fluoreszenzmarkierten Didesoxynukleotiden können durch einen Laser erkannt werden. 
  Ein Computer gibt dann einen Output file (trace file). Diese Methode ist auch bei machen Abschnitten ungenau.
- Bild (Improved Sanger sequencing):
![Improved Sanger Sequencing](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Sanger_1.png)

