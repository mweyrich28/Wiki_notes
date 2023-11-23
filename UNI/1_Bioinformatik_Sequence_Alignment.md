# Sequence Alignment
:sequence_alignment:alignment:

> *Usually when we search for sequences in the genome, we almost never find a perfect match 
> (the longer the sequence we want to find, the more unlikely a perfect match)*
## Looking back at String Matching
*Applications:*
- Searching for *sequence features* (like TF binding sites like TATA-Box)
- Searching sequence data bases for *matches of similar sequences*
- *Mapping* next gen sequencing reads to reference genome


### Different types of alignment
- _Global_ alignment of two strings 
- _Pattern matching_ (semi-global)
- Finding _overlaps_
- Finding _similarities: local alignment_


## Global vs. Local alignment
- *Global:* match as much of the sequence as possible. Is based on [1_Bioinformatik_Needleman_Wunsch_Algorithm](1_Bioinformatik_Needleman_Wunsch_Algorithm)
- *Local:* finding the regions with highest density of matches. Is based on [1_Bioinformatik_Smith_Waterman_Algorithm](1_Bioinformatik_Smith_Waterman_Algorithm)
- *Both algorithms are based on Dynamic-Programming and are similar*

### Mapping
- Mapping describes the process of finding the overall region where a read is placed in the context of a reference genome 

   
### Alignment
- Alignment describes the *exact* positioning of each base in a read in a target region
![Mapping vs Alignment](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Mapping.png)

## Pairwise Alignment
*Definition:* The process of lining up two sequences to achieve maximal levels of identity (and conservation) 
for the purpose of *assessing the degree of similarity* and the possibility of *homology*
- Are *two* (protein or gene) sequences related?
- Applications
- identify *domains or motifs* that are shared between proteins
- Identify *homologous* genes/proteins
- [1_Bioinformatik_BLAST](1_Bioinformatik_BLAST) = *"Basic Local Alignment Search Tool"*


### Why compare protein sequences?
- They carry more information (20 vs 4 characters)
- While SNP in DNA can change their sequence, amino acids are redundant and are not always affected by SNPs (codon triplets).
  Since proteins are composed of amino acids, thy structure of proteins often don't alter that way.


## Comparing Sequences
1. [1_Bioinformatik_Homology](1_Bioinformatik_Homology)
2. [1_Bioinformatik_Analogy](1_Bioinformatik_Analogy)
3. *Identity:* The extend to which two (nucleotide or amino acids) sequences are invariant (=unveränderlich/gleich bleibend).
4. *Conservation:* Changes at specific positions of an amino acid or (less commonly DNA) sequence 
   that preserve the physico-chemical properties of the original residue (=Rückstand).
5. *Similarity:* The extend to which nucleotide or protein sequences are related. It is based upon: *Identity + Conservation*.
![Homology](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Homology.jpg)

### Why homology is important for Bioinformatics
When 2 proteins or DNA sequences are homologous they *share a common ancestor.* Through pairwise alignment, we can look back in time at sequence evolution

# Issues in sequence alignment
- Sequences differ in length (most of the time)
- There may be only a relatively small region in the sequence that matches
- We want to allow *partial matches* (some amino acids are more substitutable than others) 
- *Variable length regions* may have been inserted/deleted from the common ancestral sequence. This results in *gaps* in alignment


# How can we fix this with an algorithm?

## Quantitative global alignments
We want to:
* Maximize the number of base-to-base matches
* in order to achieve this goal we can insert gaps
* We are not allowed to change the order of bases
* gap-to-gap matches are meaningless

## Now how do we quantify our alignment?

### Scoring scheme
The alignment score is the *sum of substitution* (= score of each possible character replacement) and gap penalties. 
This score reflects the quality of the match 
- [1_Bioinformatik_Substitution_matrix](1_Bioinformatik_Substitution_matrix)
- Protein substitution matrices: [1_Bioinformatik_Evolutionary_substitution_matrix](1_Bioinformatik_Evolutionary_substitution_matrix)
* Are significantly more complex than DNA scoring matrices
* since they are composed of 20 amino acids 
* physico-chemical properties vary considerably
 

### Gap penalties

#### Constant gap penalty
- each gap has an identical cost independent of it's length(e.g. -10 per gap)
- total number of gaps matter, not their sum of points
- Goal: Minimizes the sum of gaps

#### Linear gap penalty
- penalty depends linearly on the size of the gap
- penalty for one large gap is the same as for many small gaps
- Goal: Minimize sum of all gap lengths 

#### Affine gap penalty
- In biological sequences,  it is more likely that one big gap of length 10 occurs in a sequence, than 10 small gaps	
- Therefore *we favor few long gaps over many small gaps* (If sum of lengths is equal)
- They use:
	* gap opening penalty $o<0$
	* gap extension penalty $e < 0$, with $|e| < |o|$, to encourage gap extension rather than gap introduction
	* a gap of length $L$ is given a penalty of $g = o + (L-1)e$ 


### What algorithms do we use?
* Exhaustive alignment (alignment with brute force) of two sequences would take way too long: 
* The number of possible global alignments of two sequences of length N is: $\frac{2^{2N}}{\sqrt{|\sum | \cdot N}}$
* → we need to use *dynamic programming*

### Global alignment
[1_Bioinformatik_Needleman_Wunsch_Algorithm](1_Bioinformatik_Needleman_Wunsch_Algorithm)
### Local alignment
[1_Bioinformatik_Smith_Waterman_Algorithm](1_Bioinformatik_Needleman_Wunsch_Algorithm)

## Fast local alignment
### Basic Local Alignment Search Tool (BLAST)
[1_Bioinformatik_BLAST](1_Bioinformatik_BLAST)
