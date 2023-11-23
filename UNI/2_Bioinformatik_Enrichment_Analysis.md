# Gene Ontology & Enrichment Analysis
1. Vl →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect04-Enrichment-Analysis.pdf)
2. Übung →  [Slides](file:///home/malte/OneDriver/03_GoodNotes_Backup/01_Studium/2. Semester/Bioinformatik/3_Ex_EiB2_enrichment_analysis.pdf)
3. Tutorium Slides: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/3_Ex_EiB2_enrichment_analysisstudents.pptx.pdf)

→  Goal: Identifying functional patterns in (gene) expression data

*Identification of Functional Groups:*
- *Gene Sets:* For each function I look which genes correspond to said function and put them into a set
  Problem: How can we identify the function of a gene? →  Knockout or over-expressing genes (artificial)
- *Networks:* Each node = gene; edges = is there a correlation between gene a and b?
  Community Detection (Louvain Method) 
- *Pathways:* Interaction between genes and proteins; like a mind map

## Gene Annotation
:gene_annotation:
- We need structured and controlled vocabulary: 

### Ontology
:ontology:
- A collection of terms and their definitions and the logical relationships between them

### Gene Ontology
:gene_ontology:
- A collection of terms *describing gene products* and their definitions and the logical relationships between them
- A term my have more than one parent term
- And more than one child →  not a tree
- But can be described as: *Directed Acyclic Graph (DAG)*
- *Directed:* The relationship between terms is directed →  not symmetrical
- *Acyclic:* There are no cycles in the graph →  no term can be its own parent
!["Part of" and "is a" relationship](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/EnrichmentAnalysis/go.png)
*Gene Ontology is actually made out of 3 different ontologies:*
1. cellular component
2. molecular function
3. biological process

## Enrichment Analysis
:enrichment_analysis:

Two types of analysis:
1. Gene set overrepresentation analysis (GSOA/ORA):
	- Fisher's exact test
2. Gene set enrichment analysis (GSEA):
	- Enrichment score
	- Empirical p-value
*GSOA vs GSEA:* 
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/EnrichmentAnalysis/gseaVSora.png)

*_Goal of Enrichment Analysis:_*
- Identify functional patterns in gene expression data
- Identify functional groups of genes
- Enrichment analysis is most often used to characterize a gene list 
  by looking at classes of genes representing biological processes/functions (gene sets) 
  that are over represented in the gene list

**SIGNIFICANT ENRICHMENT:**
- Gene expression data can be related to gene sets (e.g. GO terms) in order to mine its functional meaning
- Which gene sets summarize at best gene expression patterns?

### Gene Set Overrepresentation Analysis / ORA
:gene_set_overrepresentation_analysis:fishers_exact_test:ora:gsoa:
1. Rank genes by their expression values (Fold change, t-test, etc.)
2. Select threshold for significance (What is up/down regulated?)
3. Look at random overlap between gene set and significant genes
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/EnrichmentAnalysis/overlap.png)
- Are there more genes in the gene set than expected by chance (=random sampling of significant genes)?

#### Fisher's exact test
![Picture](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/EnrichmentAnalysis/fisher.png)
- Is threshold dependent
- Does not require random sampling of significant genes
- It is based on the hypergeometric distribution
- a: *signifikante Gene*, die *nicht* im Gene-Set liegen
- b: *signifikante Gene*, die im Gene-Set liegen
- c: *nicht signifikante Gene*, die *nicht* im Gene-Set liegen
- d: *nicht signifikante Gene*, die im Gene-Set liegen

*BUT:*
- No natural value for the threshold
- Different results based on threshold
- Loss of information due to thresholding

*Man muss sich bei ORA entscheiden, ob wir nur hochregulierte/runterregulierte oder beides gleichzeitig anschauen wollen*

→  Use *Gene Set Enrichment Analysis* instead →  Whole distribution of genes is used

### Gene Set Enrichment Analysis
:gene_set_enrichment_analysis:gsea:

Identify pathways enriched in ranked gene lists, with a particular emphasis on ordering based on a measure of differential gene expression

1. Rank genes by their expression values (Fold change, t-test, etc.)
2. Compute an enrichment score (ES) for each gene set
3. Generate a null distribution for the ES using permutations
4. Compute an empirical p-value for each gene set
5. Correct for multiple testing (FDR) →  [1_Bioinformatik_Multiple_Hypothesis_Testing](1_Bioinformatik_Multiple_Hypothesis_Testing)

Problem of redundancy:
- Gene sets are often redundant (aka. overlapping only with a differences)
- GO has a very large number of gene-sets, often with slight differences
- Gene sets are often correlated
- We need a visualisation framework going beyond the enrichment tables →  enrichment map
- Different pathway databases have different yet overlapping definitions of pathways
- Globally, it is useful to grasp the overlap relations between enriched gene-sets

#### Enrichment score
:enrichment_score:

![Enrichment Score](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/EnrichmentAnalysis/es.png)
- Die Striche sind Gene, die wir in einen Gene Set haben
- Die Bar sind alle Gene in unserem Experiment (sortiert nach expression)
- Enrichment Score: höchster Punkt der grünen Kurve

#### Empirical p-value
:empirical_p_value:
> Mit dem empirischen pVal schauen wir wie sich unsere beobachtete Variable (ES) allgemein verhält, 
> wenn wir an den Parametern herumspielen. Diese Werte die wir mit Zufall generieren nennen wir hier Permutationen.
> Nachdem wir viele dieser Permutationen berechnet haben, schauen wir, wo unser tatsächlich beobachtete Wert steht.
> Wir nehmen als Zähler alle Werte die besser waren als unser Wert und teilen durch alle Werte. Im Bild
> konnten wir 4 Werte sehen, die einen besseren pVal hatten als unser beobachteter Wert, deshalb:
> $\frac{5}{2000} = 0.002 =$ *Empircal p value*

**Step 3 and 4 of GSEA:**
![Empirical p-value](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/EnrichmentAnalysis/empirical_p.png)

##### Phenotype / Gene Set Permutation
Wie erstellen wir unsere Permutationen?:
→  Phenotype Permutation:
- Wir Permutieren die labels unserer Patienten →  Bildung zufälliger Gruppen
- Die Phenotype Permutation funktioniert gut für viele samples

Bei wenigen samples: Gene set permutation (nicht so gut wie Phenotype Permutation, aber besser als nichts):
- Wir bauen uns zufällige Gene Sets mit der gleichen Größe
- Diese Gene Sets verhalten sich aber ganz anders im Ranking als echte Gene Sets

### G-profiler
:gprofiler:
> Beim gProfiler: Wir geben als Input alle signifikanten Gene, die wir beobachtet haben. Dann wird der Overlap dieser sigs mit
> bekannten GO Gene Sets berechnet. Das machen wir mit dem Fisher's exact test. Wir schauen uns im Endeffekt für jeden Overlap an, 
> wie wahrscheinlich es ist, den gleichen Overlap eines Gene Sets mit zufällig gezogenen Genen aus den sigs zu bekommen
> Zusätzlich müssen wir dann noch die pvals anpassen, z.B mit:
[1_Bioinformatik_Multiple_Hypothesis_Testing](1_Bioinformatik_Multiple_Hypothesis_Testing)
