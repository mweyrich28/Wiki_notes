# Multiple Hypothesis Testing
:multiple_hypothesis_testing:

## Hypothesis Testing
- Usually we define an $\alpha$ (p-value cutoff), which tells us the probability for Type I errors (FP), but this only works
  for *one test.* But when performing multiple tests, a fraction of (approximately) $\alpha$ will have a positive result *by chance alone*
- We need to account for that

## What do we want to control?
:fwer:fdr:false_discovery_rate:family_wise_error_rate:
- *FWER (Family wise error rate):* 
	- probability of at least one *FP*
- *FDR (false discovery rate):* 

|               | called not significant | called significant | total   |
|---------------|------------------------|--------------------|---------|
| $H_{0}$ true  | $U$                    | $V$                | $M_{0}$ |
| $H_{0}$ false | $T$                    | $S$                | $M_{1}$ |
| total         | $M - R$                | $R$                | $M$     |

- $FDR := E ( \frac{V}{R} )$
- Fraction of *FPs* among the rejected $H_{0}$
- The *false discovery rate* is defined as *the expected ratio of false hypotheses among the ones called significant:* $ \frac{FP}{FP + TP}$

  
### Bonferroni Correction
:bonferroni_correction:

*→  Controls FWER*

*Notation:*
- $N:$ number of hypothesis tests
- $\alpha :$ value we want to control the FWER at
- $p_{i}:$ p-value for the i-th test

*Approach:*
- p-value cutoff for each individual test: $\frac{\alpha}{N}$
- in other words: *reject* $H_{0}$ if $p_{i} \le\frac{\alpha}{N}$


### Benjamin-Hochburg Method
:benjamin_hochburg:

*→  Controls False Discovery Rate*

*Notation:*
- $N:$ number of hypothesis tests
- $\alpha :$ value we want to control the FDR at
- $p_{i}:$ p-value for the i-th test

*Approach:*
- *Sort all p-values:* $p_{1}, p_{2},...,p_{N}$
- *For a given* $\alpha$ *, find the largest* $\color{red} k$ *such that:* $p_{\color{red} k}  \le ( \frac{\color{red} k}{N}) \cdot \alpha$
- ![Example](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Statistic/Benjamin-Hochburg.png)
