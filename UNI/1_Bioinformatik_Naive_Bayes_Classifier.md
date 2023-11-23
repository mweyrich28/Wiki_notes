# Naive Bayes Classifier
:classifier:spam_filter:naive_bayes_classifier:

## Conditional Independence
$$
\boxed{P(X,Y|Z) = P(X|Y) \cdot P(Y|Z)} 
$$

## Naive Bayes Assumptions
- $P(X_{1}, X_{2}|C) = P(X_{1}|C) \cdot P(X_{2}|C)$
- Generally: $P(X_{1},...,X_{n}|C) = \prod_{i = 1}^{n} P(X_{i}|C) $

## Naive Bayes Classifier
- Single most used classifier out there
- But:
	- Usually, features are not conditionally independent
	- Probabilities P(C|X) often biased towards 0 or 1
	- Insufficient training data leads to problems: If one probability is = 0, ultimately $\prod_{i = 1}^{n} P(X_{i}|C)$ will be equal to 0

## Homework
- $max  \begin{cases} P(Play) \cdot P(Sunny|Play) \cdot P(Cool|Play) \cdot P(High|Play) \cdot P(Strong|Play) = 0.005 \\ P(\overline{Play}) \cdot P(Sunny|\overline{Play})\cdot P(Cool|\overline{Play})\cdot P(High|\overline{Play})\cdot P(Strong|\overline{Play}) = 0.2\end{cases}$ 
- Result: $0.005 < 0.2$, therefor we won't play tennis (under given parameters)

![Dataset](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Statistic/naiveByasClassifier.png)
