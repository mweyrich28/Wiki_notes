# Boyer-Moore Algorithm
:boyer_moore:algorithm:string_matching:

## Boyer-Moore vs KMP
- *Prefixed-based* KMP has worst case runtime $O(m + n)$
- KMP is the faster option for small alphabets
- *Suffix-based* Boyer-Moore has worst case runtime $O(m \cdot n)$ (worse than KMP)
- BUT: in most cases, BM is faster than KMP in practice with *sublinear runtime*
- BM is particularly suited for *long search patterns and big alphabets*

## Boyer-Moore: How does it work
- For each step we start comparing our pattern from right to left while shifting it from left to right

### Skipping Rules
1. *Bad character rule:*
- If a mismatch occurs move to the next position
- let's say we mismatched character A in our searching process, BM will now
  search for the character A in P (going from right to left, starting at 
  mismatch) and shift P in order to match character A again
- If the mismatched character A does not occur to the left in P, BM shifts
  the entire pattern past said mismatch
- We also have to compute the bad character rule: BC[j]: 
$$
max \begin{cases} 1 \\ \text{length - last index of character }-1    \end{cases} \lor \text{P.length (for every character that doesnt exits in P)}
$$
- Let's apply this formula to the following pattern:

| Pattern | A | T | A | C | T |
|---------|---|---|---|---|---|
| Index   | 0 | 1 | 2 | 3 | 4 |

This results in:

| $\sum$ | A | C | T | Other |
|--------|---|---|---|-------|
| Index  | 2 | 1 | 1 | 5     |
 
![Bad character rule](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Boyer-Moore/BM_Bad_Char)

2. *Good suffix rule I:*

![Good Suffix I](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Boyer-Moore/Suffex1.png)


3. *Good suffix rule II:*

![Good Suffix II](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Boyer-Moore/Suffix2.png)
