# Network Biology
1. Vl →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect05-NetBiology.pdf)
3. Tutorium Slides: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/4_Ex_EiB2_slides_network_biologystudents.pptx.pdf)
## OMICS data
:omics_data:omics:
- Genomics →  DNA, Sequencing
- Transcriptomics →  RNA-seq, Microarrays
- Proteomics →  Mass spectrometry, liquid chromatography
- Epigenomics →  Chip-seq, DNA methylation, bisulfite sequencing
- Metabolomics →  Metabolite concentrations
- Interactomics →  Protein-protein interactions, protein-DNA interactions
- Citomics →  Chip-seq →  Genomic repertoire of the binding sequences of a transcriptome factor

Analysis of omics data:
- Analyse individual networks
- Compare multiple networks
- Projection of data onto networks

## Network Biology
:network_biology:network:
- Model biological systems/processes as networks
- Nodes: biological entities
- Edges: relation/interactions between nodes

Can be seen as different layers of biology →  different omics:
Molecular Graphs < Metabolic Graphs < Interaction Networks < Regulatory Networks < Signaling Networks < Ecological Networks < Cellular Networks < Tissue Networks < Organ Networks < Evolutionary Networks

PROBLEMS:
- Different levels have different objects
- Often no 1:1 mapping/relation between levels
- Edges between layers connect objects on different levels of the network hierarchy

### Data integration
**Challenge: integrate data from different omics levels / multiple types/layers of data**
- different data formats, ambiguties, nomenclature
- lack of data
- different scales
**Applications:**
- Metabolic engeineering: Optimize biomedical production of chemicals throug optimized, engeineered microorganisms
- Drug design: understand influences of drugs on a cell

## Gene Regularoty Networks
:gene_regulatory_networks:grn:
- *Gene regulatory network (GRN):* is the set of activating and repressing genes or gene products and their interactions. 
- *Network inference:* The process of learning these networks from (transcriptomics) datasets.
- Gene regulation can be described as a network of interactions between genes and their products →  GRN
- Remember: *Genes do not interact directly*
- Vereinfachte Ansicht in GRNs

**Modeling GRNs:**
- *Boolean networks:* Genes are either on or off
- *Bayesian networks:* Genes are either on or off, but can also be unknown
- *Differential equations:* Genes are on a continuous scale

**GRNs:**
- *Directed:* Genes can only be activated/deactivated by other genes

### Network Interference Problem
- Given: Expression profiles
- Find: The GRN describing the regulation of (all) genes

### Bayes Theorem
- P(D) can be ignored

### Bayesian Network
:bayesian_network:bayesian:
- Nodes represent random variables
- Edges represent conditional dependencies
- Let's say x →  y, z →  y, then y depends on x and z →  P(y|x,z) = P(y|x)P(y|z)
- Each node has a conditional probability table containing all conditional 
  probabilities of the node given its parents
- If there's a directed edge form X to Y →  
  Variable X has a direct causal influence on variable Y

![Modeling](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Networks/modelling.png)

Exercise: ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Networks/exercise.png)

## Protein Protein Interaction Networks
:protein_protein_interaction_networks:ppin:
- contain an edge for each protein interaction
- Bond between two proteins can be:
	- non-covalent interaction
	- Van-der-Waals interaction
	- Hydrogen bond
	- Electrostatic interaction
	- Hydrophobic interaction

### PPI Detection
:y2h:yeast_two_hybrid:

*Yeast two-hybrid:* ![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Networks/y2h.png)

#### Principle
- Two proteins are fused to a DNA-binding domain (DBD) and a activator domain (AD)
- If the two proteins interact, the DNA-binding domain and the transcriptional activation domain are brought together
- This leads to the expression of a reporter gene
- 
#### Advantages
- High-throughput
- Can be used for large-scale screens
- 
#### Disadvantages
- False positives
- False negatives
- Only binary interactions
- Interaction must take place in the nucleus of the yeast
- Proteins may not appear with each other in vivo (e.g. due to different expression times/different domains)
- No idication on how interaction takes place
