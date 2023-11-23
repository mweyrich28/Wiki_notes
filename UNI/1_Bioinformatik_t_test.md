# t-test
:t_test:p_value:

## P-value
- The _p-value_ is the probability of an observed event (or more extreme) result *assuming that the*  $H_{0}$ *is true* 
- It represents the probability that we reject the $H_{0}$ although it is *true*

![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Statistic/pvalue.png|P-value|style="width:1000px;height:590px;"))


## Statistic tests (one-/two-sided)

- One-sided:
	- deviations in one direction are considered
- Two-sided:
	- deviations in both directions are considered


## Statistic significance

We have to define a *significance level* $\alpha$ (usually the cutoff value) in order to use the term "statistical significance"

→ If $p \le \alpha$: Deviation from $H_{0}$ is *significant* at a significant level of $\alpha \implies$ *REJECTION of* $H_{0}$ (We accept $H_{I}$)

→ If $p > \alpha$: Deviation from $H_{0}$ is *not significant* at a significant level of $\alpha \implies H_{0}$ *cannot be rejected* (we can't accept $H_{I}$)

» Therefor:
- Small $\alpha \implies$ less *Type 1 errors (FP),* more *Type 2 errors (FN)*
- Large $\alpha \implies$ more  *Type 1 errors (FP),* less *Type 2 errors (FN)*


## t-test

- Wants to compare the _mean_ between two samples/datasets

**We assume:**

1. If two sample sets are taken from the same population, then they should have fairly similar means
2. If our two means are different, then the sample sets are less likely drawn from the same population → they really are different

### Parametric t-test (one-sample)

$$
t = \frac{\overline{X} - \mu_{0}}{S/ \sqrt{n}}
$$

- $\overline{X} := \frac{\sum_{i = 1}^{n} x_{i}}{n}$
- $\mu_{0} := H_{0}$: "hypothetical mean", f.e monthly failure rate of microarrays = 2,1%? $\implies \mu_{0} = 2,1$
- $S := \sqrt{ \frac{1}{n-1} \sum_{i = 1}^{n} (x_{i} - \overline{X}) }$ (sample standard deviation)
- $n := $ Sample size 

$H_{0}$ is rejected for $p < \alpha$ with:

1. $p = P(|T| \ge |t|)$ (two-sided) $:= P(T \le t \lor T \ge t)$ (wegen Betrag)
2. $p = P(T \ge t)$ (right-sided)
3. $p = P(T \le t)$ (left-sided)

Example: 
- Given: $t = 3.07$ (two sided test), degrees of freedom: $1$:
	- Find a fitting value this table:
![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Statistic/t_test_table.png)
	- Therefor, we get $0.01 = p$ which is less then the significance value of $\alpha = 0.05$: we can reject the $H_{0}$, 
	  since there's evidence to suggest that the failure rate of the microarrays from this supplier is *not* $2.1%$ (see exercise 3)


## Common statistical tests for difference in mean

|                | Independent Samples       | Related Samples       |
|----------------|---------------------------|-----------------------|
| parametric     | Independent sample t-test | Paired samples t-test |
| non-parametric | Mann-Whitney U-Test       | Wilcoxon test         |



