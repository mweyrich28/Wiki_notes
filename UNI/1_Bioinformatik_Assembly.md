# Assembly
:assembly:graph:graph_assembly:

> Merge a set of reads in order to reconstruct an unknown sequence (f.e if there's no reference genome yet) 

1) *_DNA - reconstructions of genomes_*
	- Reconstruct the genome of an organism, *whrere no reference sequence is available*
2) *_DNA - local reconstruction_*
	- Sometimes we have a reference genome, but the *deviations from the reference genome are so substantial* 
	  that at least for selected parts of that genome/individual, a *local assembly* has to be carried out

## Initial assembly and NGS assembly
- *_De-novo assembly:_*
	- No reference is known at all
	- Perfect solutions are NP complete
- *_Comperative assembly:_*
	- Closely related organism has already been sequenced
	- applications in metagenomics

### Applications
- The shorter the reads & the more reads: the more complex the task becomes
- Thus, short read NGS has been almost just applied for targeted re-sequencing
- *For de-novo sequencing of complex organisms, approaches like PacBio are more suitable*
- *For NGS assembly of short reads, Eulerian approaches perfor usually better than Hamiltonian path approaches*

## How do we merge our reads?
> *Graphtheory:* Nodes are represented by sequence fragments (k-mers) and edges by overlaps = *_overlap graph_*

### Greedy approaches
- *_Hamiltonian Path_*
- *_de Bruijn Graph_*

| Hamiltonian Path                 | Eulerian Path                    |
|----------------------------------|----------------------------------|
| Path that visits every node once | Path that visits every edge once |


#### Why graphs?
Let's say we have a read like: *ATGCTGCACGGATTGG* and we spit it into several fragments, 
then each node can be used to represent a fragment:
![Initial Graph](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Assembly_Graph_1.png)
Now we beginn at the heavies edge (5) and start merging the nodes:
![Firts merge](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Assembly_Graph_2.png)
We do continue merging the nodes which are connected by edges with the highest weight until we are left with only one node.
This node represents our new reference sequence. (If we have several edges with the same weight, we pick a random one)
![Finished Assembly](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Assembly_Graph_3.png)

##### Drawbacks
- Long runtime
- for all node pairs in the graph we need to calculate the pairwise suffix/prefix alignments

#### Alternative: local version
- Start with random read as seed contig (= set of overlapping DNA fragments) 
- Align from 3'-end (right) and merge the contig with the read (merge the ones with largest overlap)
- Repeat until no further extension is possible
- Apply principal to 5'-end (left)
- *Drawback:* decreased quality 


#### Problem of repetition
![Repetition](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Repetition.png)

## Eulerian path
- First the reads from a shotgun sequencing are as k-mers (composed out of k bases)
- For each k-mer the number of occurrences is calculated (this way we can estimate repeats)
- *Advantages:*
	1. No explicit calculation of alignments/overlaps, thus fast
	2. Finding Eulerian path is much less complex that finding Hamiltonian path
- *BUT:*
	1. Usually there isn't just one Eulerian path but a substantial and exponentially growing number
*_K-mers:_*
![Kmers](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/k-mers_1.png)


### De Bruijn graph
- Are *_Eulerian_*
- An n-dimensional graph on an alphabet of m symbols is a directed (gerichteter) graph. This is an particular kind of overlap graph
- It consists of *m^n^* nodes
- If a node results from another node by shifting the sequence by one character at the end of the node,
  an edge between both nodes is drawn
- De Bruijn graphs based algorithms are very sensitive to the parameter k

![De Bruijn Graph](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/DeBruijn_1.png)
*The assembly problem is equivalent in finding an Eulerian path that traverses eache edge in the Bruijn graph.*
![De DeBruijn construction](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/DeBruijn_2.png)

Another example:
![Finished DeBruijn Graph](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/DeBrujinGraph_Homework.jpg)
The number of the edges stems from the overview table (how often does a specific k-mere exist?). 
An *Eulerian path* in this graph would have to cross each edge x-times if we define x as the weight of the edge. 
A complete Eulerian path doesn't always exist!

![Eulerian Path](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/EulerianPathSolution.png)

#### Artifacts - Eulerian path
![SPUR](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Artifacts_SPUR.png)
![Bubble](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Artifacts_BUBBLE.png)
![Frayed roap](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Artifacts_FRAYEDROPE.png)
