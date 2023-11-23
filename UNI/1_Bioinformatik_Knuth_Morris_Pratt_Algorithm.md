# Knuth-Morris-Pratt
:kmp:knuth_morris_pratt_exact_pattern_search:pattern_search:algorithm:

## Key idea
- KMP is a *prefix based* algorithm
- It tries to avoid as many unnecessary comparisons as possible 
- The worst case runtime is: $O(m + n)$
- Key idea: *_"If a pattern fails to match, slide pattern to the right by as many positions as possible"_*
- KMP compares pattern: *left → right* but shifts the pattern more intelligently than naive algorithms
→  ![Smart shifts in String searching](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/KMP/KMP1.png)

### How does KMP react to mismatches
- When a mismatch occurs, the pattern can be shifted by the length of the largest prefix of P(0...j) that is also a suffix of P(1...j) [P being the pattern] to avoid redundant comparisons
- KMP knows how far to shift the pattern by computing a so called *Failure Function* (basically an int[])*
- Example [a, b, a, a, b, a] $\underbrace{\to }_{\text{Failure Function}}$ [0, 0, 1, 1, 2, 3]
- The failure function tells us, at which index of P we should continue to compare our P to T, e.g if we have a mismatch and our failure function gives us the value 3, then this means that we start comparing at index 3 (of P) since we already know that index 0-2 are matches

 
## Worst case Runtime
For situations like:
- Pattern = xxxxxx
- Example String = xxxxixxxxixxxxixxxxixxxxixxxxi
*»* $O(m + n)$
- [1_Bioinformatik_KMP_py](1_Bioinformatik_KMP_py)

## KMP in Action
![Step 1](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/KMP/k6.png)
![Step 2](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/KMP/k7.png)
![Step 3](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/KMP/k8.png)
![Step 4](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/KMP/k9.png)

- After the mismatch occurred, KMP shifted the pattern to the last matched character 
