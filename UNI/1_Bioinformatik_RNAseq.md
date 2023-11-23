# RNA-seq 
:rna_seq:transcriptomics:

## Applications of RNA-seq
1. *Transcript quantification*
2. *Transcript discovery*
3. *Expression profiling*

## RNA-seq Data Analysis
![Pipeline](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/rna_seq_analysis.png)

## RNA to Sequencing Data
1. Create a soup of RNA and DNA
2. Remove DNA
3. Select RNA of interest (Remove rRNA, Select mRNA?)
4. Fragment RNA
5. Do reverse transcription → we're left with cDNA
6. Ligate(bind) sequence adaptors
7. (Optional) PCR amplification
8. Select a range of sizes

## Reasons for Quality Control
- Quality decreases towards 3' end (base trimming)
- CG-content
- Adaptor contamination
- Over represented k-mers
- Duplicated reads (seq errors)
- PCR artifacts
- Contaminations (from other organisms)
- Tools:
	- *FastQC*
	- *MultiQC* as a wrapper
	- more...

## How do we map our reads?
→  [[1_Bioinformatik_STAR]]


## RNA-seq Count Matrix
- *Count Matrix (N)* $= n \times m$
- $N_{ij}$ = Number of reads in *gene i* sequenced in *sample j*
![Image of count Matrix](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/Count_Matrix.png)

## Expression Units
:expression_units:tpm:cpm:rpkm:fpkm:

![Overview](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/ExpressionUnits.png)
### CMP
→  Counts per million mapped reads

### RPKM
→  Reads per Kilobase million *(for single-end RNA-seq)*

*We:*
1. Normalize for read depth:
	1. Count up the total reads in a sample and divide it by 1.000.000 → scaling factor $s_{x}$
	2. Divide the read counts by $s_{x}$ factor to normalize for *sequencing depth* → "reads per million (RPM)"
2. Normalize for gene length:
	1. Divide RPM values by length of each gene in kilobases → RPKM

### FPKM
→  Fragments per kilobase million 
- $FPKM = \frac{RPKM}{2}$

### TPM
→  Transcripts per million

*We:*
1. Normalize for gene length:
	1. Divide read counts by length of each gene in kilobases → reads per kilobase (RPK)
2. Normalize for read depth:
	2. Count up all values in a sample and divide by 1.000.000 → $s_{x}$
	3. Divide the RPK values by $s_{x}$ → TPM

#### Summary Expression Units
![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/Expression_Units.png)

### TPM vs RPKM
- The sum of all TPMs in each sample are the same
	- → easier to compare to the portion of reads that mapped to a gene in each sample
	- With TPM, "everyone gets the same sized pie"

![TPM vs RPKM](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/TPM_vs_RPKM.pnga)
