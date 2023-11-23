# Material
1. [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect11-RNA-structure.pdf)
2. Tutorium Slides: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/10_Ex_EiB2_slides_RNA_structure_prediction_short_version.pptx.pdf)

## Types of RNA
:types_of_rna:
- mRNA
- tRNA
- rRNA
- snRNA (small nuclear RNA) →  Splicing
- snoRNA (small nucleolar RNA) →  rRNA processing
- miRNA (micro RNA) →  Gene regulation
- siRNA (short interfering RNA) →  Gene regulation

## Structure DNA vs RNA
:structure_dna_vs_rna:

![Structural differences](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/structure.png)

### What are wobble base pairs
- G-U appears as well:
	- G-U is a wobble base pair
	- C-G (3 H-bonds) > A-U (2-Hbonds) > G-U (wobble base pair)

*PURINE:* A, G →  2 rings 

*PYRIMIDINE:* C, T, U →  1 ring 

*TRANSITION:* 
Purine →  Purine: 
Pyrimidine →  Pyrimidine 

*TRANSVERSION:* 
Purine →  Pyrimidine 
Pyrimidine →  Purine 

### RNA secondary structure
:rna_structure:

→  Can become quite complex
→  Is essential for function
- single stranded RNA
- double stranded RNA (requires 2 RNA molecules)
- stem and loop
- bulge loop
- interior loop
- junctions
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/sec_struc.png)

#### Representation
- Graph
- Or linear
- Or circular
- Or dot plots

### RNA tertiary structure
→  Determined with X-ray crystallography
- more complex than secondary structure
- relevant to explain function

## Formalisation
### Definition 1
An RNA sequence of length _n_ is a string:
	s = (s1,s2,s3,...,sn), si ∈ {A,C,G,U}, ∀ i ∈ {1,...,n}

### Definition 2
An RNA secondary structure for a sequence is a set _P_ of ordered 
base pairs (i,j) with 1 ≤ i < j ≤ n, such that:
	- j-i > 3, because we need at least 4 bases to form a loop
	- i and j can only pair with each other, base pairs do not conflict:
	  {i,j} ∩ {i',j'} = ∅, ∀ (i,j),(i',j') ∈ P

### Definition 3
Nestedness:
- A secondary structure is called nested if:
	1. i < j < i'< j': (i,j) *precedes* (i',j')
	2. i < i'< j'< j: (i,j) *includes* (i',j')
- Pseudo-knots arise from non-nested secondary structures:
	- Base pairs from different stems cross each other
	- not uncommon in RNA
![Pseudo Knots](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/pseu_knots.png)

### How do we compare 2 RNA structures
How many base pairs do we have?
How many G-C base pairs do we have? →  3 H bridges

# Secondar Structure Prediction - RNA
:secondar_structure_prediction:
- Given RNA sequnce s = (s1,s2,...,sn)
- Identify correct secondary structure

## Combinatorics of secondary structures
*WE SIMPLIFY*
- exclude pseudo knots
- allow all possible base pairings
- Sequence length [1,n]
*CALCULATE*
- Let S(n) := number of secondary structures for a sequence of length n
- S(0) = 1
- S(1) = 1
- For n > 1:
	- S(n+1) = S(n) + S(n-1) + $\sum_{k = 1}^{n-2} S(k)S(n-k-1)$
	- For n = 7 is sum: S(1)S(5) + S(2)S(4) + S(3)S(3) + S(4)S(2) + S(5)S(1)
![Recursive sum](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/sum.png)
- S(n) can be approximated by:
![Approximation](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/approx.png)

### Approach to structure prediction using state of minimal energy
- RNA tries to fold into a structure of minimal energy
- Thus RNA will try to fold into a structure with the most base pairs
- We coudl try to find the structure with the most base pairs among all possible structures:
	- This is NP-hard

### Nussinov Folding Algorithm
:nussinov_folding_algorithm:alogrithm:dynamical_programming:
- Dynamic programming algorithm: finds best solution based on the best solutions from smaller subsequences
- Explores all best secondary structures recursively:
	- Optimal: maximizes number of base pairs
- We don't allow pseudo knots
- Scoring scheme: 1 for match, 0 for mismatch (Das könnt man noch verbessern, indem wir z.B G-C mehr gewichten (da 3 H Brücken), dann könnten wir aber nicht mehr sehen wie viele matches wir haben)

Three steps:
1. Initialization
2. Filling the matrix
3. Backtracking

*Initialization:*
- Sweep over the diagonal and fill in 0
- Also fill in 0 below the diagonal

*Filling the matrix:*
- We also sweep diagonally starting at i = 1, j = 2 
Die wir schauen uns die 4 Fälle jeweils an:
![4 Cases](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/filling.png)
1. Case: i unpaired (down)
2. Case: j unpaired (left)
3. Case: i-j pair (diagonal)
4. Case: bifurcation (down, left):
	- "M-Shape": ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/m_shape.png):
		- We also always need to look at the previous row and column
		- ![Fehlerhaft eingezeichnet aber Prinzip stimmt](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/RNA/m_shape2.png):
			- For d(6, 11) we compute:
```
                          ↓  d(k+1,j)
 d(6,7)  + d(8,11)  = 1 + 5 →  6
 d(6,8)  + d(9,11)  = 1 + 3
 d(6,9)  + d(10,11) = 3 + 3 →  6
 d(6,10) + d(11,11) = 5 + 0
               d(i,k)↑  
```

*Traceback:*
Der score steh oben rechts, wenn 2 →  wir haben 2 Basenpaarungen in unsere "optimalen", immer den höchsten score nehmen
Dann Backtracking:
- we additionally need a traceback matrix
- we stop at 0
- Webtool Nussinov: https://rna.informatik.uni-freiburg.de/Teaching/index.jsp?toolName=Nussinov

#### Problems of Nussinov
- All base pairs are considered equal
- Stability is not only determined by base pairs →  stability through base stacking
	- What we can do:
	  ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/free_e_rna_f.png)

#### Free energy minimization
- Nussinov can be adapted: replace delta by an energy function →  we turn the problem into a minimization (of free energy) problem
- BUT: We still don't consider base stacking and destabilizing loops
- WE NEED: better energy functions

### Zuker-Stiegler Algorithm
:zuker_stiegler_algorithm:alogrithm:
- Accounts for:
	- loops
	- stacked bases
	- other secondary structure features
- Everything is basically seen as loop: we decompose the structure into loops
- Finds a minimum free energy secondary structure
- müssen wir nicht im Detail können, aber zusätzliche Betrachtungen:
	- Base stacking und loops, base stacking ist eine Art von Loop →  wir betrachten alle Energiebeiträge

#### Definition 1
If (i,j) is a base pair in secondary structure P and i < h < j then base h is accessible from (i,j) in P
if theres no base pair (i', j') in P such that i < i' < h < j' < j

#### Definition 2
The set of all bases accessible from (i,j) in P is called the loop. The size of the loop is 
the number of unpaired bases in the loop

#### Definition 3
The set L of all k-1 base pairs and k' unpaired bases that are accessible from (i,j) in P is called
the k-loop closed by (i,j)

## Comperative Analysis
- Ausgleichende Mutationen = compensatory change →  two bases have to change
- That way, although the sequence changes, the structure stays the same
- similar structures although the sequences are different
