# Genomics Definition
:genome:genomics:sequencing:

- Study of whole genomes of organisms
- Sequencing → Assembly → Analyse structure and functions of genome
- *Genomics vs genetics:* 
- Genetics: We look at just one gene and it's functions
- Genomics: We look at the whole genome → all the genes and their relationships in order to identify 
  their combined influence on growth and development of the organism

Genomics focuses on interactions between *loci and alleles* within the genome and other _intragenomic interactions_ such as:

1. *Epistasis:* 
- A gene that influences the phenotypic expression of another gene at another locus
2. *Pleiotropy:* 
- A single gene contributes to multiple traits (Melanin)
3. *Heterosis:* 
- Heterozygous individuals have increased fitness compared to homozygous

## Sequencing

### Definition
- Getting access to the sequence/primary structure of any Biopolymer (DNA, RNA, mRNA, proteins etc.)
- Genomics harnesses the availability of *complete DNA sequences* for entire organisms

### First generation sequencing
- [1_Bioinformatik_Sanger_Sequencing](1_Bioinformatik_Sanger_Sequencing)

### Next generation sequencing (NGS)
- [1_Bioinformatik_Illumina](1_Bioinformatik_Illumina)
- Follow the classical approaches (f.e. of Sanger_Sequencing)
- High-throughput (hoher Durchsatz an Daten) + highly parallel sequencing (sequencing more than one sample/individual) 
  → *Next generation sequencing*

### Sanger vs. Illumina
- Sanger can be used to research/sequence *monogenetic diseases* but when it comes to more complex genetic disorders,
  it lacks high throughput
- For more complex genetic disorders we use NGS (f.e. [1_Bioinformatik_Illumina](1_Bioinformatik_Illumina)), with Illumina we can sequence many genes and at once
- Both are *sequencing by sythesis*

### Different generations of sequencing
- First generation
* (Sanger, Maxam, Gilbert) (Short read sequencing)
- Second generation (NGS)
* (Illumina, Solexa) (Short read sequencing)
- Third generation
* PacBio (Long read sequencing)
* Oxford Nanopore (Long read sequencing)


## Problems with NGS
- sequencing reads are comparably Short
- high error rates
- some genomic regions can be hard to impossible to access
- reference genome is not perfect and far from complete
- repeats are a huge problem

### Short read vs. long read
*Limitations of short read technologies:*
1. *GC bias*
2. it has difficulties mapping to *repetitive elements*
3. trouble discriminating paralogoues sequences, and difficulties in phasing 
   (welche Sequenz kommt von väterlicher/mütterlicher DNA?)
- Long read single molecule sequences resolve these obstacles *but suffer from high errror rate*

### Third generation sequencing

#### PacBio SMRT
- DNA is synthesized in zero-mode wave-guides (very small nanowells)
- Single polymerase binding to the bottom of nanowells
- No need for amplification (PCR)
 
##### Pros
- long reads
- short sequencing time
- no amplification bias 
- can detect epigenetic modifications (DNA-methylation)
![PacBio](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/pacBio_1.png|Image)

#### Nanopore sequencing
![Nanopore](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/nanopore_1.png)

#### NGS pipeline
*DNA extraction* →  *genetic enrichment* →  *Libary prep* → *sequencing* →  *primery analysis* →  *secondary analysis*

For Nanopore:

*DNA extraction*  →  *sequencing* → *primery analysis* → *secondary analysis*


## Applications -omics view
| DNA                                    | RNA                                |
|----------------------------------------|------------------------------------|
| Whole human genome sequencing          | Transcriptome sequencing (all RNA) |
| Exome sequencing                       | miRNOme sequencing                 |
| Gene panel sequencing (Bestimmte Gene) |                                    |
| Pathogene sequencing                   |                                    |
|                                        |                                    |
| SNP calling                            | Expression level                   |
| INDEL calling                          | Alternative splicing events        |
| Copy Number variations                 | Fusion genes                       |
| Genomic rearrangement                  |                                    |
