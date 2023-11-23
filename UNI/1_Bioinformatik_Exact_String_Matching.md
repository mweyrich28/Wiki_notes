# Design techniques
:algorithm:design_techniques:string_matching:

## Exhaustive search
- *Bruteforce, examine every possible alternative to find a solution*

## Greedy algorithms
- *Choose the locally most attractive alternative at each iteration*
- *Contra:* Our trait off is the fact that our solution won't be the most optimal

## Divide and conquer
- *Devide problem into smaller sub problems and solve these smaller instances (preferably on binary level)*
- Split, solve, merge
- E.g.: Merge sort

## Dynamic programming
- Similar to divide and conquer but in dynamic programming, some of our subproblems overlap, that's why for every unique result we calculated we 
  keep it in a so called *_dynamic programming table_*
- A good example for the effect of dynamic programming is when we calculate the n-th fib number using recursion. If we don't keep track of all the numbers
  we calculated before, we would compute various operations multiple times. Therefore we keep track of every single result we calculated 
  so far in a _*DYNAMIC PROGRAMMING TABLE*_

----

# Algorithms

## String Matching
- Naive algorithms have a time complexity of: $O(\underbrace{m}_{\text{pattern.length}} \cdot  \underbrace{n}_{\text{text.length}} )$
- [1_Bioinformatik_Approaches_String_Matching](1_Bioinformatik_Approaches_String_Matching)
 
## Algorithms we talked about
- [1_Bioinformatik_Knuth_Morris_Pratt_Algorithm](1_Bioinformatik_Knuth_Morris_Pratt_Algorithm)
- [1_Bioinformatik_Boyer_Moore_Algorithm](1_Bioinformatik_Boyer_Moore_Algorithm)
