# Poisson Distribution
:poiison:poisson_distribution:distribution:

## Application
- Model *events taking place over and over* in a completely unpredictable way (f.e counting yellow cars for one hour)

## Definition
- The _random variable_ *counts* the *numer of events* that take place in a given *interval*
- All events take place *independently* of all other events
- Events take place *at a constant rate* $:= \lambda $
- Probability mass function: 
$$
\boxed{P_{\lambda}(x) = e^{- \lambda \cdot t} \cdot \frac{(\lambda \cdot t)^{x}}{x!} } 
$$

## Important
- *For large* $n$ *and very small* $p$ *: Binomial → Poisson*

![Poisson and Binomial](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Statistic/poissonVSbin.png)
