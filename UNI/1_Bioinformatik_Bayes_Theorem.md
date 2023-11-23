# Bayes Theorem
:bayes:bayes_theorem:

## Prior, Likelihood, Evidence, Posterior
$$
\boxed{\underbrace{P(A|B)}_{\text{Posterior}}  = \frac{\overbrace{P(B|A)}^{\text{Likelihood}} \cdot \overbrace{P(A)}^{\text{Prior}}}{\underbrace{P(B)}_{\text{Evidence}} }
} 
$$

## Example
- Two vessels:
	1. 8 Yellow balls & 4 blue balls := 12 in total
	2. 8 Blue balls & 4 yellow balls := 12 in total
- We take *two random balls* from vessel 1 and put it into vessel 2. Afterwards we draw a random ball from vessel 2
- P(B) = We draw two blue balls from vessel 2
- Question: What is the probability that two blue balls were drawn from vessel 1, when at the end a blue ball was drawn form vessel 2? 
- How to solve this:
	- There are three possibilities for the event *A:*
		1. We draw two blue balls $:= P(A_{1}) = \frac{4}{12} \cdot  \frac{3}{11} = 0,0909$ 
		2. We draw one of each $:= P(A_{2}) =\frac{4}{12} \cdot  \frac{8}{11} + \frac{8}{12} \cdot  \frac{4}{11} = 0,4848$
		3. We draw two yellow balls $:= P(A_{3}) = \frac{8}{12} \cdot  \frac{7}{11} = 0,4242$
	- Now we need one more value: $P(B)$, we calculate this probability with the law of total probability: $P(B) = P(B|A_{1}) \cdot P(A_{1})+ P(B|A_{2}) \cdot P(A_{2})... + P(B|A_{n}) \cdot  A_{n}$
	- For $P(B)$ we get: $0,5777$
	- Now we can calculate each scenario $P(A_{1}|B), P(A_{2}|B), P(A_{3}|B)$ with the formula of Bayes Theorem
	- Results:
		1. $P(A_{1}|B) = 0,1049$
		2. $P(A_{2}|B) = 0.5035$ 
		3. $P(A_{3}|B) = 0.3916$
