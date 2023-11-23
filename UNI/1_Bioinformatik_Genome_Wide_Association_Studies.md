# Genome Wide Association Studies
:gwas:cochran_armitage:

## Definition
> In genomics, a genome-wide association study (GWA study, or GWAS), is an observational study of a genome-wide set of genetic variants in different individuals to see if any variant is associated with a trait.

## Example
- Variant A increases risk for a certain disease:

→ Task:
	- *Given:* genetic information and disease status of a set of people
	- *Goal:* identify the disease-associated genetic variation/identify genetic affect associated with said disease

## GWAS
- Detect disease risk → better monitoring of risk patients
- Prescribe personalized medicine against disease


### Encode SNPs
- *Additive effects:*
	- 0: homozygous major allele (A/A)
	- 1: heterozygous (A/G $\lor$ G/A)
	- 2: homozygous minor allele (G/G)

- *Dominant effects:*
	- 0: homozygous major allele (A/A)
	- 2: heterozygous (A/G $\lor$ G/A)
	- 2: homozygous minor allele (G/G)

- *Recessive effects:*
	- 0: homozygous major allele (A/A)
	- 0: heterozygous (A/G $\lor$ G/A)
	- 2: homozygous minor allele (G/G)

## Linkage/Linkage disequilibrium
SNPs in close proximity on the locus are very often correlated:
![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/PopulationGenetics/linkage.png)


## Linear models
- Usually one allele is considered the *risk allele*
- *Risks* are assumed to be *additive*

### Cochran-Armitage Test
![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/PopulationGenetics/cochranArmitage.png)

*» With the Cochran-Armitage test we cant classify the disease risk for heterozygous «*

## Manhattan Plots
- Type of scatter plot
- Displays data with large number of data points
- Dots $\iff$ SNPs
- *X-axis: genomic coordinates*
- *negative logarithm of the association p-value for each SNP*
- Because strong associations have small p-values, they are placed higher on the y-axis because $-\log_{10}(p)$ returns high results for small p-values

![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/PopulationGenetics/manhattanPlot.png)
