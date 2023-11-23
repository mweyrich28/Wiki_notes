# Sanger-Sequenzierung
:sequencing:

## First generation sequencing
- [1_Bioinformatik_Sanger_Sequencing](1_Bioinformatik_Sanger_Sequencing)

## Next generation sequencing (NGS)
- 1_Bioinformatik_Illumina

## Messungen von...

### DNA Polymorphismen (DNA-seq)

![DNA Sequencing](/home/malte/01_Documents/vimwiki/Assets/Bio/DNA-seq.png)

### Cytosin Methylierung ### 

*WGBS* = Whole Genome Bisulfite Sequencing

![WGBS](/home/malte/01_Documents/vimwiki/Assets/Bio/WGBS.png)

### Histone Modifikationen (ChIP-seq)
![Überblick](/home/malte/01_Documents/vimwiki/Assets/Bio/ChIP-seq.png)
![Reads](/home/malte/01_Documents/vimwiki/Assets/Bio/ChIP-seq1.png)
![Interpreting Reads](/home/malte/01_Documents/vimwiki/Assets/Bio/ChIP-seq2.png)

Nur die DNA die um die modifizierten Histone gewickelt ist, wird sequenziert und dem Referenzgenom zugeordnet.
Mache Histonmodifikationen haben eine breite Verteilung (weil sie, wenn sie vorkommen, auf mehreren 
Histonen neben einander liegen). Andere Modifikationen haben eine enge Verteilung.


### RNA Expression (RNA-seq)
- Wir extrahieren die gesamte RNA (also alle möglichen wie z.B. siRNA, Long ncRNA rRNA, mRNA). Wir wollen aber nur die mRNA, deshalb selektieren wir diese (Poly-A-Selektion).
- Die mRNA wird dann zu cDNA umgewandelt (reverse Transkription) 
- Die resultierenden Stränge sind zu lang, also müssen sie wieder fragmentiert werden (library prep).
- Anschließend werden sie Sequenziert und wir erhalten unsere Reads.
- Auf dem Referenzgen bilden sich nun Peaks, diese sind dann ein Zeichen dafür, dass genau dieses Exon (verstärkt) expromiert wird. Exome ohne peak werden nicht exprimiert

![Ablauf](/home/malte/01_Documents/vimwiki/Assets/Bio/RNA-seq.png)

