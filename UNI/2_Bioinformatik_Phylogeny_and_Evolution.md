# MATERIAL
1. [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect09-Phylogeny.pdf)
2. [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/9_Ex_EiB2_slides_phylogeny.pptx.pdf)

## Phylogeny
:phylogeny:

> is the inference of evolutionary relationships between organisms

### Processes of speciation
:speciation:
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/phylogeny.png)
- *_Anagenesis_* - Transformation of species:
	- Higher development
	- Phyletic evolution
- *_Cladogenisis_* - Species splitting:
	- Root branching
	- Biodiversity is increased
- *_Regressive evolution:_*
	- Regression/degeneration

## Taxon
:taxon:
- Group of organisms
- Unity within biological classification (species, genus, family)

*MONOPHYLETIC TAXON:*
> Taxon has a common ancestry and *includes all subgroups* as well as the ancestral from itself →  clade

*POLYPHYLETIC TAXON:*
> Taxon includes derivatives of various lineages
> Taxon has no common ancestry

*PARAPHYLETIC TAXON:*
> Taxon does not include all the descendants of a common ancestor →  one or more subgroups are missing

![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/taxon.png)


## Topology of Phylogenetic trees
:phylogenetig_tree:
- *Nodes:*
	- *Internal* = _Hypothetical Taxonomic Unit_ (HTU) →  Common ancestor; based on predictions (today: sequencing)
	- *External* = _Operational Taxonomic Unit_ (OTU) →  still alive; sequenced
- *Root:* _Last Universal Common Ancestor_ (LUCA)
	- Root adds direction to our tree
- *Branches* = Evolutionary kinship
- No cycles
- Usually binary trees →  1 ancestor, 2 descendants/offsprings

### Rooted Tree
- Clear time course of evolution or divergence
- LUCA is the root

### Unrooted Tree
- Evolutionary relationship
- LUCA unknown
- No clear evolutionary direction

## Presentation of phylogenetic trees

### Cladogram
:cladogram:
- rooted or unrooted
- Only ancestry is displayed
- Branches are called clades
- The length of the branches is not important / has no meaning

### Additive Tree
:additive_tree:
- rooted or unrooted
- Edges:
	- Length = Quantitative measure of evolution (~ # of mutations)
	- Sum of the edge lengths = evolutionary distance of two taxa
- No information about mutation rate
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/additive_tree.png)

### Ultrametric Tree
:ultrametric_tree:
- *Always rooted*
- Edges constant mutation rate *(molecular clock)*
- Identical evolutionary distance between ancestors and descendants

#### Comparing main differences between the three types of trees
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/phylogenetic_tree_comparison.png)

### Complexity - Phylogenetic Trees
- n := #leaves (OTUs)

|                 | Unrooted | Rooted   |
|-----------------|----------|----------|
| #internal nodes | n-1      | n-2      |
| #nodes          | k = 2n-2 | k = 2n-1 |

**Possible Trees:**
- Unrooted: $\frac{(2n-5)!}{(2^{n-3}(n-3)!)}$
- Rooted: $\frac{(2n-3)!}{(2^{n-2}(n-2)!)}$

### Species vs Feature (gene/protein) trees
The topology of a gene (or protein) tree may differ from the topology of a species tree.
- Gene trees are more variable than species trees
- Genes may duplicate or otherwise evolve before or after speciation events:
  Aka: A gene may duplicate before or after a two species diverge
- In Species trees, speciation usually occurs when a species becomes reproductively isolated from its parent species
![Species- vs. Featuretree](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/species_vs_feature_tree.png)

## Molecular Evolution
:molecular_evolution:
*Moleculare level:* Evolution is a process of mutation with selection
*Moleculare Evolution:* Study of the changes in genes and proteins over time
- A measure of evolutionary distance

### Molecular clock
:molecular_clock:
- For every given protein, the rate of molecular evolution is approximately constant over time in all evolutionary lineages
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/molecular_clock.png)
> Here we see, the rate of mutation is different for different proteins but constant for the same protein
- Why is that: The mutation rate is dependent on the function of the protein. 
  *Proteins with a more important function have a lower mutation rate.*
  *Proteins with a less important function have a higher mutation rate.*

### Mutations
:mutations:transition:transversion:
- Success of a mutation depending on its effect on organism
- Synonymous mutations: No change in the amino acid sequence
- Non-synonymous mutations: Change in the amino acid sequence

*PURINE:* A, G →  2 rings →  2 H-bonds

*PYRIMIDINE:* C, T, U →  1 ring →  3 H-bonds

*TRANSITION:* 
Purine →  Purine: 
Pyrimidine →  Pyrimidine 

*TRANSVERSION:* 
Purine →  Pyrimidine 
Pyrimidine →  Purine 

- *Transitions are way more likely than transversions* →  we need to account for that 
- [1_Bioinformatik_Homology](1_Bioinformatik_Homology)

*GENE LOSS:*
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/gene_loss.png)
→  Can complicate or distort reconstruction of phylogenetic trees/evolutionary events

### What events play a role in evolution of genes
- Speciation
- Gene duplication
- Gene loss
- Horizontal gene transfer
- Gene fusion, division and other rearrangements of genes

# Quantitative Modelling of Molecular Evolution

## P-distance
:p-distance:
Share of non-identical alignment positions: 
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/p_distance.png)
- D = Number of differences / Number of sites
- L = Aligned positions (without gaps)
	- D = 4, L = 24 →  4/24 = 1/6
- Problem: What if G →  C →  A →  C →  G: We can't observe/count these types of mutations

## Poisson Distance
:poisson_distance:
*ASSUMPTION:*
Number of mutations is poisson distributed
- $d_{p} = -\ln(1 - p)$ with p the p-distance
→  Distribution of the number of events (mutations) that occur
   at *a constant rate* and *independent of each other* in a *fixed* time
   interval or spatial area (sequence pos)

## Jukes-Cantor 1-Parameter Model
:jukes-cantor:
- Representation as *substitution rate matrix*
- All positions are independent and have identical mutation rate _alpha_ for all possible transitions
- Only works if the two sequences are very similar
- ![Matrix](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/jukes_cantor.png)

## Kimura 2-Parameter Model
:kimura:
- Representation as *substitution rate matrix*
- But this time: Transitions alpha and transversions beta have different mutation rates
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Phylogeny/kimura.png)

### Assumptions of the Jukes-Cantor and Kimura 2-Parameter Model
- Only substitutions, no insertions or deletions
- Substitutions in different positions are independent
- Substitutions only depend on the current state of the sequence (Markov process)
- Same mutation rate for all positions
- 1:1:1:1 ratio of nucleotides

# Reconstruction of phylogenetic tree
:phylogenetic_tree_reconstruction:

## Steps
1. Which data to use?: Ideally: sequence with highly conserved and very variable sections
2. Which model to use?: 
	- [Jukes-Cantor 1-Parameter Model](#Jukes-Cantor 1-Parameter Model)
	- [Kimura 2-Parameter Model](#Kimura 2-Parameter Model)
3. Which method to use?: 
	- [Distance based](#Distance based)
	- [Alignment based](#Alignment based)

### Distance based
- Multiple sequence alignment determines evolutionary distance between all pairs of OTUs
- Exactly one tree is produced
- Can be used for very large datasets
- Multiple trees do exist for one alignment
- Comparison of different trees is difficult

#### UPGMA
:upgma:distance_based_phylogeny:
- *Unweighted Pair Group Method using Arithmetic Mean*:
- Suitable for:
	- sequence data that has evolved under circumstances in which the rate 
	  of mutation is constant over time

*PRINCIPLE:*
- Sequential clustering
*ASSUMPTIONS:*
- Molecular clock
*RESULT:*
- Rooted tree with branch lengths

*ALGORITHM*
1. Take smallest distance in distance matrix
2. Height of new node = 0.5 * distance
3. Update distance matrix:
	- Distance of two clusters: $d(XY) = \frac{1}{N_{X} \cdot N_{Y}} \sum_{i \in X, j \in Y}d(i,j)$ 
	- $N_{X}:=$ Number of OTUs in cluster X
	- $N_{Y}:=$ Number of OTUs in cluster Y

#### Neighbor Joining
:neighbor_joining:
- Distance based method
- It considers different mutation rates

*PRINCIPLE:*
- Sequentially group OTUs while minimizing branch lengths
*ASSUMPTIONS:*
- Minimum evolution, i.e. the tree with the smallest sum of branch lengths is the best
*RESULT:*
- Unrooted additive tree with branch lengths

*ALGORITHM*
1. Calculate M matrix: $M_{ij} = (n-2)d(i,j) - r(i)-r(j)$:
	- r(i) = Sum of all distances of i to all other OTUs
2. Find minimum value in M matrix:
	1. Create a new node V that joins i and j
	2. Calculate distance of edges form i to V and j to V:
		- $b(V,i) = 0.5d(i,j)- \frac{1}{(n-2) \cdot 2} \cdot (r(i) -r(j))$
		- $b(V,j) = d(i,j) - b(V,i)$
3. Update distance matrix:
	1. $d(x,V) = 0,5 \cdot (d(i,x) + d(j,x)-d(i,j))$
4. Repeat until only one node is left

### Alignment based
- Multiple alignment is used directly
- Finding the optimal topology by evaluating all individual alignment positions
- All trees that explain the data are generated
- Computational complexity is high →  very expensive

#### Maximum Parsimony
:maximum_parsimony:
- Alignment based
- We are looking for the tree that requires the fewest number of mutations to explain the observed differences
- All possible topologies are considered
- Often results in many unrooted trees
- Based on minimal evolution
- Minimize the number of mutations to reconstruct the tree
- State changes instead of distance matrix
- *OUTPUT:* unrooted, additive tree/cladogram

*ALGORITHM:*
1. Search all informative positions
2. Determine which tree topologies need to be examined
3. For each position determine the number of mutations for each tree topology
4. Tree that requires the fewest mutations is the best 
   = Maximum Parsimony Tree

#### Maximum Likelihood
:maximum_likelihood:
- Alignment based
- We are looking for the tree that is most likely to have produced the observed data
- All possible topologies are considered
