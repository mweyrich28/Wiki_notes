# Conditional Probability
:conditional_probability:bedingte_wahrscheinlichkeit:

## Definition
$$
\boxed{P_{B}(A) = P(A|B) = \frac{P(A \cap B)}{P(B)}} 
$$

## Properties of conditional probability
- $A \cap B = \emptyset \implies P(A|B) = 0$
- $B \subseteq A \implies A \cap B = B \implies P(A|B) = \frac{P(B)}{P(B)} = 1$
- $A \subseteq B \implies A \cap B = A \implies P(A|B) = \frac{P(A)}{P(B)}$
- $P(A \cap B) = P(B) \cdot P(A|B)$ 

## Law of total Probability
> If B,,1,,, B,,2,,, B,,3,,,... is a partition of sample space $\Omega$ then for any event $A$ we have:

$$
\boxed{P(A) = \sum_{i = 1}^{n} P(A \cap B_{i}) = \sum_{i = 1}^{n} P(A|B_{i}) \cdot P(B_{i})} 
$$

## Independence ## 
In normal cases $P(A) \neq P(A|B)$, but if $P(A) = P(A|B)$ then $A \land B$ are *independent*
	
*Definition:* If *A* and *B* are independent of each other then:
$$
P(A \cap B) = P(A) \cdot P(B)
$$
