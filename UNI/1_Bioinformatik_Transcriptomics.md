# Transcriptomics
:transcriptomics:short_read_mapping:rna:micro_arays:microarrays:

## Overview

> Genomics →  Epigenomics →  Transcriptomics →  Proteomics

### Types of RNA
*Topic: Proteins*
- mRNA → messenger RNA → encodes proteins
- tRNA → transfer RNA → adaptor between mRNA and amino acids
- rRNA → ribosomal RNA → forms the ribosome
*Topic: gene regulation:*
- miRAN → micro RNA → regulates gene expression
- siRNA → short interfering RNA → silences gene expression
- lncRNA → long non-coding RNA → regulates gene expression
-*Other:* 
- snRNA → small nuclear RNA → functions in various nuclear processes (e.g splicing)
- snoRNA → small *nucleolar* RNA → facilitates chemical modifications of RNAs
- circRNA → circular RNA → function unclear

## Aims of Transcriptomics
- Understand *processes and associations* both within and between genes
- Genetic diseases lead to changes in gene expression through...:
	- Changes in regulation (epigenetics)
	- Splice variants
	- SNPs
	- Structural variants and copy number variations
- We cant target genes → Drug discovery
- Transcriptomics is individual →  Personalized medicine


## Micro Arrays
- Measures mRNA expression (the brighter the signal the higher the expression of a specific mRNA)
- Made out of solid substrate: Each dot on the surface binds to a specific mRNA, they bind to their target probes
- *Hybridization:*
	- Hybridization describes the binding of complementary strands of DNA
	- The level of hybridization can be measured by image analysis (level of hybridization is indicated by means of fluorescence)
	- The obtained measures indicate the level of expression of the gene corresponding probe


## Process Overview
1. We look at a certain cell type (e.g healthy bone cell and cancerous bone cell)
2. We multiply these by creating cell cultures
3. We isolate all RNAs
4. We tag all RNAs with a fluorescent
5. We do reverse transcription: RNA → cDNA (complimentary DNA), we then splice them to single strands of cDNA
6. The cDNA strands now can bind to the complementary strands on the microarray, each spot on the microarray resembling a specific RNA transcript (sequence in DNA)
7. Judging by the intensity of the color signal, we can tell whether RNA transcript x is over/under/not expressed 
   in our control/experiment probe
8. Often we need additional Background correction
![Process image](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/microarray.png)
$$
\text{Probe n} \Bigg( \frac{\color{red} \text{Amount of expreiment sample hybridization} }{\color{green} \text{Amount of control sample hybridization}}\Bigg) = \text{Probe n Expression Ratio} 
$$
## Oligonucleotide Array vs cDNA Spotted Array

### Oligonucleotide Arrays
- Not based on *competitive hybridization* (i.e. only one color)
- →  each chip containing samples from a single type
- Utilizes short probes/sequences (25-70bp), each gene is represented by a group of short probes 
- Cheaper once developed 

### cDNA Spotted Array
- Utilizes long probes/sequences (1-2 kb), each gene is represented by a single long probe
![Oligonucleotide vs cDNA Array](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/cDNA_Array_vs_Oligo.png)

## Data Pre-Processing
*Pipeline:*
- RAW data files from image processing software → Pre-Processing → Data matrix ready for downstream analysis

### Background Substraction Microarrays
**Background consists of:**
- non-specific binding to the fluorophore
- incomplete washing
- auto-fluorescence of the chip surface
**Background estimation from:**
- Local area around the spots
- Global background
- *Affymetrix:* So dense that there's no place between the probes
- Background estimation from the probe signals themselves
**BUT:**
- Background subtraction is *controversial*
- *Reduces bias* but *increases variance* in the estimates of the ratios of interest (ratio inflation)

### Normalization Microarrays
**Adjust the intensities from *each array* to balance them appropriately**
- That way, we can mace meaningful biological comparisons
**Reasons why data must be normalized:**
- *Systematic biases* in the measured expression levels
- *Unequal quantities* of starting RNA
- Differences in *labeling and hybridization efficiency*
- Differences in *detection efficiencies* between the fluorescent dyes used
**Assumption:**
- No global changes in gene expression between samples

**Important:**
- Gene innerhalb eines samples: *Nach der Länge sortieren*
- Gene von verschiedenen samples: *Nach der Anzahl der reads sortieren*

#### Normalization Methods
Commonly used:
- Scaling
- LOESS 
- Quantile
- Percentile shift
- RMA (Robust Multiarray Averaging)

#### Example
Without *normalization*, many genes will appear to be unregulated when really they're not

![Normalization Example](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Transcriptomics/normalization.png)
## Summarizing Values (Collapsing)
- Probes are often replicated on the array
- Each gene is often covered by multiple probes
- For downstream analysis replicate probes need to be *summarized (collapsed)*

### Commonly used strategies
- Probe level collapsing: Median/mean of replicate probe values
- Gene level collapsing: Median/mean of summarized probe values
- [[Imputation Mircoarrays]]

## Imputation Microarrays - Dealing with Missing Values
- Many downstream analyses *require a complex matrixe* of gene array values (input)
- Missing values are a common problem for the analysis of microarray data
**Strategies:**
1. missing values are removed
2. missing values are replaced by constant
3. missing values are re-estimated on the basis to the whole expression data (most common)
