# File Formats Bioinformatics
:fasta:fastq:sam:bam:

## Fasta
- A variable number of sequence records
- Mostly sequences of nucleotides

### Attributes
- Id 
- Sequence

### Example
```
>Mus_musculus_tRNA-Ala-AGC-1-1 (chr13.trna34-AlaAGC)
GGGGGTGTAGCTCAGTGGTAGAGCGCGTGCTTAGCATGCACGAGGcCCTGGGTTCGATCC
CCAGCACCTCCA
>Mus_musculus_tRNA-Ala-AGC-10-1 (chr13.trna457-AlaAGC)
GGGGGATTAGCTCAAATGGTAGAGCGCTCGCTTAGCATGCAAGAGGtAGTGGGATCGATG
CCCACATCCTCCA
```

![Picture](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Formats/FASTA.png)

## Fastq
FASTQ was conceived to solve a specific problem arising during sequencing: Due to how different sequencing technologies work, the confidence in each base call (that is, the estimated probability of having correctly identified a given nucleotide) varies. This is expressed in the Phred quality score. FASTA had no standardised way of encoding this. By contrast, a *FASTQ record contains a sequence of quality scores for each nucleotide.*

- Mostly used to store short read data from high-throughput sequencing expreiments
- Sequence and quality scores are usually put into single line each

### Format
1. A line starting with @, containing the sequence ID.
2. One or more lines that contain the sequence.
3. A new line starting with the character +, and being either empty or repeating the sequence ID.
4. One or more lines that contain the quality scores.


### Example
```
@071112_SLXA-EAS1_s_7:5:1:817:345
GGGTGATGGCCGCTGCCGATGGCGTC
AAATCCCACC
+
IIIIIIIIIIIIIIIIIIIIIIIIII
IIII9IG9IC
@071112_SLXA-EAS1_s_7:5:1:801:338
GTTCAGGGATACGACGTTTGTATTTTAAGAATCTGA
+
IIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII6IBI
```

![Fastq](/home/malte/01_Documents/vimwiki/Assets/Bioinformatik/Formats/FASTQ_FORMAT.png)

## Sam & Bam
- SAM (Sequence Alignment Map)
- BAM -> Binary version of SAM which stores the same data (Binary compressed)
- SAM stores biological sequences aligned to reference Sequence
- Mostly used for storing data, such as nucleotide sequences, generated by [1_Bio_NGS](1_Bio_NGS).
- Format includes short and long reads


### Format
- Header (begins with @) & Alignment section
- Alignment sections have 11 fields, as well as a variable number of optional fields

| Col | Field | Type   | Brief description                     |
|-----|-------|--------|---------------------------------------|
| 1   | QNAME | String | Query template NAME                   |
| 2   | FLAG  | Int    | bitwise FLAG                          |
| 3   | RNAME | String | References sequence NAME              |
| 4   | POS   | Int    | 1- based leftmost mapping POSition    |
| 5   | MAPQ  | Int    | MAPping Quality                       |
| 6   | CIGAR | String | CIGAR string                          |
| 7   | RNEXT | String | Ref. name of the mate/next read       |
| 8   | PNEXT | Int    | Position of the mate/next read        |
| 9   | TLEN  | Int    | observed Template LENgth              |
| 10  | SEQ   | String | segment SEQuence                      |
| 11  | QUAL  | String | ASCII of Phred-scaled base QUALity+33 |
