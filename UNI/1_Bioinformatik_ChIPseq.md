# Chromatin immunoprecipitation
:chip-seq:mapping:peak_calling:
![Introbox ChIPSeq](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/ChIP-seq_1.png)
## Protein-DNA interaction
*DNA binding proteins:*
- Transcription factors
- DNA replication factors (DNA polymerase)
- DNA repair factors
- DNA structure proteins (e.g histones)

*With ChIP we can analyse:*
1. Protein interaction with DNA
2. Other DNA-interacting proteins
3. Protein specific antibodies

*Several research protocols for ChIP are:*
- ChIP-chip: microarrays
- ChIP-PCR: quantitative real-time PCR
- *ChIP-seq: NGS*

## Data Analysis ChIP-seq
## Analysis pipeline
> ChIP → Sequence → Mapping → Signal map → Peak detection → Analysis

### Step 1: ChIP
- Glue proteins bound to DNA and cut DNA into smaller fragments by sonication *(library preparation)*
- Isolate proteins which we're interested in by *using _antibodies_* binding to these specific proteins *(Immuno precipitation)*
- Warm everything up and be left with only the DNA fragments without proteins and histones

### Step by step:
1. First, we purify DNA from cross-linked cells and cut it into fragments of size between 200-600bp
2. Now we perform *immunoprecipitation*: We add protein specific antibodies which only bind to the proteins of interest
3. Now we separate the fragments with the protein of interest from the rest by linking them to a surface matrix using magnetic 
   beads. That way we fix them physically, allowing us to separate these fragments of interest
4. Reverse cross-linking and purify DNA

### Step 2: Sequencing
- Sequence fragments with NGS *(paired-end sequencing)*
- Mapping of sequenced fragments to reference genome, discard garbage reads

### Step 3&4: Signal map and peak detection
- Create histogram which counts how often each genomic position is covered by *short sequence reads*
- → *binomeal modle (paired-end sequencing)*
When calling peaks on data which consists of million of reads, approaches like dynamic programming will fail, thus we need an 
efficient mapping algorithm. It has to deal with *missmatches (by mutation, sequencing errors*) and somehow needs to compress 
big data while still being able to access and work with the data, without constantly having to compress and extract it.
- We use [1_Bioinformatik_Bowtie](1_Bioinformatik_Bowtie) for data compression
- Peak detection is done with [1_Bioinformatik_MACS2](1_Bioinformatik_MACS2)


### Step 5: Analysis
- Apply motif discovery tool to look for e.g TFs
*Important:*
In rea-life applications, we always should perform two experiments:
1. Experiment as shown in the above
2. A control experiment whrere we sequence everything (i.e. we don't filter out anything)
→ That way we get two different maps. This is useful, that way we can filter out some FPs because some peaks appear on both maps 
(meaning they are random and they have nothing to do with our analysis)

## Signal Map
![Histogram Signalmap](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Signal_Map_CHiP.png)
- This is a *histogram* for forward and reverse reads for all uniquely mapped reads, in other words: Count how often each 
  genomic position is covered by a short sequence read.
- *Assumption*: Binding sites should be somewhere between corresponding peaks on the forward- and reverse strand in the histogram
- Our data shows "bi-modal enrichment pattern": *A peak on forward strand is followed by a similar peak on the reverse strand.*
The reason for this is the relatively long fragment (~ 600bp) vs. read length size (~ 150bp)
