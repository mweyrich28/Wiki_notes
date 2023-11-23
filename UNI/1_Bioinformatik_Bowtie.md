# Bowtie
:bowtie:bwt:mapping:software:algorithm:alignment:

## What is Bowtie
- Ultra fast memory-efficient alignment tool
- Aligns short DNA sequences to the human genome
- Uses the *Burros-Wheeler transform (BWT)* to reduce the memory footprint of the genome index
- *BWT* is a *lossless text compression algorithm*
- Invers of BWT exists → we can reconstruct the input starting from the output 


## Burros-Wheeler Transformation
*Step by step:*

We start with a string we want to compress: t = banana:
1. Step: we add \$ to our string:
	- banana$

2. Step: Generate cyclic rotations:

|         |
|---------|
| banana$ |
| anana$b |
| nana$ba |
| ana$ban |
| na$bana |
| a$banan |
| $banana |

1. Order and sort lexicographically

|         |   |         |
|---------|---|---------|
| banana$ | → | $banana |
| anana$b | → | a$banan |
| nana$ba | → | ana$ban |
| ana$ban | → | anana$b |
| na$bana | → | banana$ |
| a$banan | → | na$bana |
| $banana | → | nana$ba |

1. Now we read the last column: this string represents our *BWT:* _annb$aa_:
	- We sort this String again lexicographically to: _$aaabnn_ we need this extra String for reconstruction. 
2. To reconstruct our original String again we start of by creating a table like this:

|            |   |   |   |   |   |   |                        |   |
|------------|---|---|---|---|---|---|------------------------|---|
| sorted BWT |   |   |   |   |   |   | This is our BWT string |   |
| \$         |   |   |   |   |   |   | a                      |   |
| a          |   |   |   |   |   |   | n                      |   |
| a          |   |   |   |   |   |   | n                      |   |
| a          |   |   |   |   |   |   | b                      |   |
| b          |   |   |   |   |   |   | \$                     |   |
| n          |   |   |   |   |   |   | a                      |   |
| n          |   |   |   |   |   |   | a                      |   |

### Reconstruction
:reconstruction:bwt:bowtie:

We start at the first row in the last column:
We construct our original string from *right to left*
Each time we hit a letter on the left column, we add the opposite letter to our string

- We start at "$"
- We are finished when hitting "$" again

String t: $\color{green}a$

| sorted BWT |   |   |   |   |   |   | This is our BWT string              |
|------------|---|---|---|---|---|---|-------------------------------------|
| $          |   |   |   |   |   |   | $\color{green}a$           <- start |
| a          |   |   |   |   |   |   | n                                   |
| a          |   |   |   |   |   |   | n                                   |
| a          |   |   |   |   |   |   | b                                   |
| b          |   |   |   |   |   |   | $                                   |
| n          |   |   |   |   |   |   | a                                   |
| n          |   |   |   |   |   |   | a                                   |

Our first letter is an a, to be specific, it's the first a relatively to our BWT String. Now we find the first a in the first column:

String t: $\color{green}na$

| sorted BWT |    |   |   |   |   |   | This is our BWT string                       |
|------------|----|---|---|---|---|---|----------------------------------------------|
| $          |    |   |   |   |   | / | a           <- start                         |
| a          | <- | - | - | - | - |   |  $\color{green}n$           <- letter across |
| a          |    |   |   |   |   |   | n                                            |
| a          |    |   |   |   |   |   | b                                            |
| b          |    |   |   |   |   |   | $                                            |
| n          |    |   |   |   |   |   | a                                            |
| n          |    |   |   |   |   |   | a                                            |

We arrived at the first a in the first column, the letter across said a is our next letter we add to our final String. 
Said letter is "n", to be specific, it's the first n in our BWT String, we jump to the first n in the first column and
*repeat this over and over again until we end at $*

Last step:

| sorted BWT |    |   |   |   |   |   | This is our BWT string     |
|------------|----|---|---|---|---|---|----------------------------|
| $          |    |   |   |   |   |   | a                          |
| a          |    |   |   |   |   |   | n                          |
| a          |    |   |   |   |   |   | n                          |
| a          |    |   |   |   | - | - | b  <- last char            |
| b          | <- | - | - | / |   |   | $  <- char across: we STOP |
| n          |    |   |   |   |   |   | a                          |
| n          |    |   |   |   |   |   | a                          |

Final String: $t = \color{green} banana$

## Searching for pattern using BWT
:pattern:bwt:string_search:exact_matching:bowtie:

We search for $\color{red} agc$ in the sequence *acaagc* using Bowtie:
![Overview](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/12_Ex_EiB1_chip_seq_and_short_read_mapping-5.jpg)

### Step by step
1. $\color{red} top$ arrow starts at the top and $\color{green} bottom$ arrow starts beneath the last string_search
2. Now we grab the last letter of the pattern *g* and we place this letter at the end of our table (matching the height of our arrows)
3. Then we look at exactly these letters, at which position are they? The *g* (at the red arrow) is the *first* one, we mark it with a one.
4. We do the same for the $\color{green} bottom $ arrow, the *g* is the second *g* in our column (since we just labeled the upper g as the first g)
5. Now we move the arrows, the $\color{red} top$ arrow is moved to the first *g* (in the first column), this would place our $\color{red} top$ arrow at the last row of the first column
6. We do the same for our $\color{green} bottom$ arrow, the first possible position for a second *g* is right beneath the $\color{red} top$ arrow.
7. We grab the next letter from our pattern and imagine putting it correspondingly to our arrows next to the last column
8. We count the relative position again (of the letters) 

> :warning: **Warning:**  If we put an imaginary letter to the top arrow and in reality, the real letter at this position (of the last column) is not said imaginary letter of the pattern, then our imaginary letter only exists for the top arrow. *We don't count it when we look at the position of the second arrow*

Here's an imagine showing said situation:
![Example](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Pattern_search_problem-34.jpg)

## Bowtie in action (Bowtie 2)
→  https://www.youtube.com/watch?v=fSnAeYHnPCw
