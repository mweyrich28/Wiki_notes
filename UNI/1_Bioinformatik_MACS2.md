# MACS2
:macs2:algorithm:peak:peak_detection:

## Model-based analysis of ChIP-seq (MACS2)
- Identifies genome-wide *locations of transcription/chromatin factor binding histone modification* from *ChIP-seq*

## Overview of how MACS2 works
1. Removing redundant reads
2. Adjusting read position ( _tag shift_ by d/2 where d is the band size » increased resolution)
	- d is estimated by MACS2
4. Calculating peak enrichment
5. Estimating False Discovery Rate
![Tag Shift performed on Graph](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/MACS2/Tag_Shift.png)
![Image 2 Tag Shift](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/MACS2/Tag_Shift_2.png)
