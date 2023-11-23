# The Substitution matrix
:substitution_matrix:matrix:

- N $\times$ N *goodness score matrix* (N is 4 for DNA and 20 for proteins)
 
## Example for DNA goodness score matrix

|   | C  | T  | A  | G  |
|---|----|----|----|----|
| C | 1  | -1 | -1 | -1 |
| T | -1 |  1 | -1 | -1 |
| A | -1 | -1 | 1  | -1 |
| G | -1 | -1 | -1 | 1  |

* To further improve this matrix we can adjust the scoring for Purines (A, G) and Pyramidines (C,T) since Transitions ( purine $\to$ purine/ pyrimidine $\to $ pyrimidine) are more likely than transversions (pyrimidine $\to$ purine und anders herum)

|   | C  | T  | A  | G  |
|---|----|----|----|----|
| C | 2  | 1  | -1 | -1 |
| T | 1  | 2  | -1 | -1 |
| A | -1 | -1 | 2  | 1  |
| G | -1 | -1 | 1  | 2  |
