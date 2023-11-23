# Next generation sequencing (NGS)
:next_generation_sequencing:illumina:ngs:

## Illumina
![Overview](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Illumina_1.png)
1. Library preparation
2. Cluster growth (bridge amplification)
3. Sequencing
4. Image acquisition
5. Base calling


## Wichtige Schritte
### Library preparation
- Vorbereitung der DNA Fragmente
- Die DNA Fragmente entstehen durch Ultraschallbehandlung der Sequenz $\implies$ So erhalten wir Fragmente, 
  die alle die gleiche/eine sehr sehr ähnliche Länge besitzen
- Hinzufügen von Adaptern, Selektion nach Fragmentlänge
- Optional kann hier noch ein PCR gemacht werden, falls es insgesamt wenig Fragmente sind
- ![Picture](/home/malte/01_Documents/vimwiki/Assets/Bio/LibraryPrep.png)

#### Template amplification
- Klonale Amplifikation der DNA Fragmente durch *bride amplification*
- [[Bridge Amplification]]

#### Bridge Amplification
Das DNA Fragment wird auf die *Flow-Zelle* gelegt, diese besteht aus *Microwells:* ![Picture](/home/malte/01_Documents/vimwiki/Assets/Bio/BridgeAmp.png). 
Auf der Flow-Zelle ist sozusagen ein Rasen von Komplementären Sequenzen (zu den in der Library preparation hinzugefügten)
*Adaptorsequenzen*. Der von dem Rasen festgehaltene DNA Strang wird nun von der DNA-Poly. II vervollständigt.
Anschließend werden die zwei Stränge voneinander getrennt, einer ist nun fest an dem Rasen angebaut. 
Dieser kann sich jetzt an dem oberen Ende frei bewegen und sich so an den korrespondierenden Rasenadapter knüpfen. 
Hier findet wieder eine Duplication des Strangs statt, dieses mal wieder in die andere Richtung. 
Das ganze geht so lange bis wir ein groß Cluster eines Fragments erstellt haben. 
Durch das Cluster wird das Signal der Fluorophore stark genug sein, um von einem Senor erkannt zu werden.
Durch die _Linearisation_ entfernen wir alle komplementären Stränge der Sequenz, ansonsten würden wir die Sequenz 
vorwärts und rückwärts (Komplement) gleichzeitig lesen
Abschließend wird durch das _Blocking_ noch die nach oben zeigenden Enden der Sequenz blockiert, 
damit sie nicht weiter Brücken bilden 
Ein Primer wird in die Flowcell gegeben: nun kann die DNA Polymerase II anfangen den Strang zu übersetzen
![Synthese auf der Flowzelle](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Illumina_2.png)
![Bridge amplification](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Illumina_3.png)
![Linearization](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Illumina_4.png)
	
#### Sequencing/imaging=
*Lesen der Sequenz:*
- Integration von fluoreszenzmarkierten Didesoxynukleotiden (= wie eine Suppe aus Nukleotiden).
- Die jeweilig komplementären Nukleotide binden sich an den DNA Strang.
- Die überflüssigen Didesoxynukleotide werden weg gewaschen.
- Jetzt findet das Imaging statt.
- Dann werden die Fluoreszenz-Marker und Terminierungsgruppen entfernt.
- Der nächste Zyklus beginnt.

Also wird pro Zyklus eine Base sequenziert. Ein Bild des Ablaufs: 
![Zyklus](/home/malte/01_Documents/vimwiki/Assets/Bio/Imaging.png)


## Paired-end Sequencing
Wir machen da weiter, wo wir oben aufgehört haben. Nach dem wir eine Sequenz vollständig sequenziert haben, entfernen wir nun die 
_blockers_, so können sich wieder über die bridge amplification die Stränge duplizieren. 
Nachdem wir wieder einen vollständigen Rasen haben, entfernen wir nun die ursprünglichen Stränge durch Linearization. 
Wir verbleiben dieses mal mit den reversed strands. Diese sequenzieren wir genau so wie wir davor die originalen strands 
sequenziert haben.

| Vorteile                                                                                                  |
|-----------------------------------------------------------------------------------------------------------|
| Die Distanz zwischen jedem paar ist uns bekannt                                                           |
| Algorithmen nutzen dieses Wissen nun, um reads besser mappen zu können (vor allem bei repetitive regions) |

![Paired-end read](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/paired-end-read-1.jpg)

## Paired-end vs. single-end sequencing
![Advantage of paired-end sequencing](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/paired-end_vs_singleend.png)

Short DNA fragments are covered with a greater efficiency compared to paired-end reads. 
Repeat-rich genomes face the *challenge of more multiple mapped reads, as shown for the orange read, compared to paired-end sequencing.*

YouTube video: https://www.youtube.com/watch?v=gNT6Mg-xAbc

## Multiplexing
- In order not to waste sequencing chemistry and to bring down the cost, each sample can be assigned a barcode 
  (additional few bases at adapter sequence)
- When the sequencing has been finished *the first bases then determine the sample* (de-multiplexing)
