# Wright-Fisher Model
:wright_fisher:population_genetics:allele_distribution:

## Assumptions
1. Constant population size: $< \infty$
2. Diploid organisms
3. Allele frequency identical for male and female
4. Non overlapping generations
5. random mating
6. NO selection, mutation, migration

## Units
- $N:=$ Population size
- $n_{A} :=$ Number of *A* alleles
- $n_{a} :=$ Number of *a* alleles
- $t :=$ generation


## Calculating allele frequency
- $p = \frac{n_{A}}{\underbrace{2N}_{\text{Diploid Organisms}} }$
- $q = 1 - p = \frac{n_{a}}{2N}$

Then we can calculate the number of alleles A in generation t+1: $P(n_{A}' = k) = B_{2N, p}(\underbrace{k}_{\text{Generation}} ) = \binom{2N}{k} \cdot p^{k} \cdot q^{2N-k}$

### How quickly does allele frequency change
- $\mu = np$
- $\text{Var}(x) = npq$
- $\sigma = \sqrt{npq}$

*» Consequence for allele frequency of generation t+1:* $p' = p + \frac{\sqrt{pq}}{2N}$

- The larger the population, the smaller the effect
- The effect drift is largest for $p=q=0.5$

![Wright Fisher](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/PopulationGenetics/WrightFisher.png)
