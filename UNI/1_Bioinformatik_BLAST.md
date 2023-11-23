# BLAST
:blast:algorithm:

*Basic Local Alignment Search Tool (BLAST):*
* Finds regions of *local similarity* between sequences
* Compares nucleotide or protein sequences to database
* Alignments are assigned a *significance score* (called _E-value_)
* *E-value (expectation value):*
_number of different Alignments with scores equivalent to or better than a score *S* that one can expect to occur in a dataset search by chance_
* The lower the E-value, the more significant the score S and, thus the alignment 

*There are different types of BLAST programs:*

![BLAST Programs](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/BLAST_Programs.png)
## Steps of BLAST
1. Remove low complexity region or sequence repeats in the *query* section
2. Make a k-letter word list for the query sequence
	- (for proteins k=4, for DNA k=11)
3. List the possible matching words
4. Organize the remaining high-scoring words into an efficient search tree
5. Repeat step 3 to 4 for each k-letter word in the query sequence
6. Scan database sequences for exact matches with the remaining high-scoring words 
7. Extend the exact matches to *high-scoring segment pair* (HSP)
8. List all HSPs in the database whose score is high enough to be considered 
9. Evaluate the significance of the HSP score
10. Make two or more HSP regions into a longer Alignment
11. Show the gapped [1_Bioinformatik_Smith_Waterman_Algorithm](1_Bioinformatik_Smith_Waterman_Algorithm) local alignments of the query and each of the matched database sequences
12. Report every match whose expect score is lower than a threshold parameter

![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/BLAST_OverView_1.png)

![Picture Blast 2](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/BLAST_OverView_2.png)
