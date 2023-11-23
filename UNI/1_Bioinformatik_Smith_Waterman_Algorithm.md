# Smith-Waterman algorithm
:smith_waterman:algorithm:dynamic_programming:

* is a variation of the Needleman-Wunsch algorithm
* it compares alignments of *any possible length* starting and ending at any position in the two sequences
* *Guarenteed to find the optimal local alignment*
* Scoring system: Substitution matrix & gap-scoring scheme
* When looking at protein sequences, we use the BLOSUM matrix

## Main difference to Needleman-Wunsch
- *There are no negative scores, the lowest score is 0*
- *The traceback begins at the highest score and ends with 0* (exclusive)

The scores are calculated slightly differently: S(i, j) = $max \begin{cases} \text{S(i-1, j-1) } + r(x_{i},y_{i})  \\ \text{S(i-1, j) } + g \\ \text{S(i, j-1)} + g \\ 0 \end{cases}$

*→  We look for long matching areas independent of how long mismatching areas are between them*

![Example](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Smith_1.png)
