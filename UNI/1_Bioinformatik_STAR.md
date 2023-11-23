# STAR

## Read mapping (RNA)
- Typically reads are aligned to the genome but when dealing with RNA reads, we need to consider alternative splicing
- *STAR* is a _splice aware_ alignment tool

## STAR
- Has high accuracy
- Drastically outperforms other aligners in mapping speed, at the cost of being memory intensive
- It consists out of a *two-step*  process:
	1. *Seed searching*
	2. *Clustering, stitching & scoring*

### Seed searching
- Aligns every read to the longest sequence possible that exactly matches one or more locations on the reference genome
- These regions are called: *Maximal mappable prefixes*: ![Maximal mappable prefixes](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/STAR/MMPs.png)
- Each read can be split into so called *seeds*, after mapping seed1, STAR will try to find the 
  ![longest matching sequence](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/STAR/Seeds.png) for the remaining seed2 (unmapped portion of seed1) of the read  
- If STAR does not find an exact matching sequence for each part of the read due to mismatches or indels, 
  the previous *MMPs will be extended:* ![Extending MMPs](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/STAR/Extend.png)
- If extension does not give a good alignment, we will cut off (soft clip) this sequence

### Cluster, stitching & scoring
- Now we stitch the separate reads together by first clustering the seeds together *based on proximity* to a set of 'anchor seeds', or seeds that are not multi-mapping
- Seeds are stitched together based on the *best alignment for the read*: 
![Stitching](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/STAR/Stitching.png)
