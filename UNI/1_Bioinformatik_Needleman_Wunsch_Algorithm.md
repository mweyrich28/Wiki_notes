# Needleman-Wunsch Algorithm
:needleman_wunsch:algorithm:global_alignment:alignment:dynamic_programming:

Idea: build up the best *global* alignment by *using optimal alignments of smaller subsequences*
    
- uses dynamic programming (two 2D-matrices)
- S(i, j) = $max \begin{cases} \text{S(i-1, j-1) } &+ r(x_{i},y_{i})  \\ \text{S(i-1, j) } &+ g \\ \text{S(i, j-1)} &+ g \end{cases}$
- g = [[Gap Penalty]], 
- $r(x_{i}, y_{j})$ = match/substitution $x_{i} \text{ with} y_{j}$
- Our two matrices: 
    * *Score matrix*
    * *Traceback matrix*
- Three steps:
    1. Init of score matrix
    2. Calculation of scores and filling the traceback matrix
    3. Deducting the alignment from the traceback matrix
        * we begin at last cell (bottom right)
        * sequences are aligned from right to left:
        * We insert gaps as:
            * left pattern (first column) if we came from *←*
            * top pattern (first row) if we came from *↑*
- *Evlaluation:* The alignment with the best score will be the output of NW
- When looking at proteins, we *use PAM matrix*

## Example
- In this example we are using 
![Traceback matrix](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Needleman_1.png)
![Tracing traceback](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Needleman_2.png)
