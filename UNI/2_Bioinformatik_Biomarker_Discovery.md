# Biomarkers
:biomarkers:
1. Vl →  [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect06-Biomarker-Discovery.pdf)
2. Tutorium Slides: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/5_Ex_EiB2_biomarker_discoverystudents.pptx.pdf)
*DEFINITION:*
- A biomarker is ‘a characteristic that is objectively measured and evaluated as an indicator of normal biological processes, 
  pathogenic processes, or pharmacological responses to a therapeutic intervention’
- A biomarker is anything that can be used as an indicator of a particular disease state or some other physiological 
  state of an organism
- An *ideal* biomarker is one through which the disease comes about or through which an intervention alters the (course of the)
  disease

*EXAMPLES:*
Biomarkers can be...
- indicators of functional or structural changes in cells or tissues
- used to predict and monitor molecular changes relevant to the current development or future emergence of diseases, complaints or symptoms
- considered as a therapeutic target (when there's a clear causal relationship between the biomarker and the disease)
- can be based on *molecular, histological, radiographic or physiological* characteristics

## Typical Biomarkers
:typical_biomarkers:
- Complete blood count
- Blood pressure
- Body temperature
- Body mass index
- Waist to hip ratio
- Heart rate
- ... 

## Three biomarker types
:biomarker_types:
### Type 0: History
*Estimate the emergence or development of a disease:*
- Example: measurement of serum creatinine to measure kidney function or monitor injury to kidneys

### Type 1: Therapy
*Predict response to therapeutic treatment:*
- Further divided into:
	- Efficacy biomarkers: These are used to predict the clinical benefit of a drug.
	- Mechanism biomarkers: given information about the mechanism of action of a drug.
	- Toxicity biomarkers: These are used to predict the toxicological effects of a drug.
- Example: These are drug activity biomarkers and they indicate the effect of drug intervention. 

### Type 2: Surrogate
*Surrogate clinical endpoints in the course of clinical trials.*
A surrogate endpoint/biomarker is a measure of an effect of a specific treatment that may correlate 
with a real clinical endpoint
*BUT:* does not necessarily have a guaranteed relationship.

- Example: cholesterol levels in heart disease:
	- Cholesterol is a biomarker for heart disease
	- elevated levels = increased risk of heart disease
	- _But: not all people with high cholesterol will develop heart disease and not all people with heart disease have high cholesterol_

#### Clinical end points
:clinical_end_points:clinical_outcome_assessments:

- Biomarker 󰦎 clinical end point
- Biomarker 󰦎 clinical outcome assessment
- *Endpoint:* a precisely defined variable designed to indicate an outcome 
  of interest that is statistically analysed to address a particular research question
- *Clinical outcome assesment:* an evaluation of how an individual feels, functions or survives

*EXAMPLES:*
- Disease-free survival
- Overall survival
- Percent serious adverse events
- Death
- ...

→  Biomarkers can be *surrogate endpoints*

## Advantages of Biomarkers
In clinical trials, biomarkers can be used to:
- Identify patients who are likely to respond to a particular treatment
- Identify patients who are likely to experience side effects from a particular treatment
- Narrow down the patient population to those who are most likely to benefit from a particular treatment
- Smaller sample sizes

## Biomarker Discovery
:biomarker_discovery:
Biomarker discovery is the process of identifying biomarkers:
- Biomarkers are discovered through comparison of physiological states, 
  phenotypes or changes across control and case (disease) groups
- On the moleculare level, such differences can be reflected in differential activity of the transcriptome, 
  proteome, metabolome, epigenome, microbiome, etc. 
- Biomarker discovery typically relies on the idea that those molecular species
  (genes, proteins, ...) that display the greatest changes across phenotypes 
  may be reported as potential biomarkers

*STEPS TO IDENTIFY AND DEVELOP BIOMARKERS:*
Discovery →  Development →  Validation →  Clinical application

| Discovery                         | → | Development                       | → | Validation                        | → | Clinical application/use |
|-----------------------------------|---|-----------------------------------|---|-----------------------------------|---|--------------------------|
| Identify candidate biomarkers     |   | Prototype assay                   |   | Validation set                    |   |                          |
| Assay development                 |   | Test set                          |   | Specific detection of the analyte |   |                          |
| Specific detection of the analyte |   | Specific detection of the analyte |   | Real-world prospective validation |   |                          |
|                                   |   | Results reproducible              |   |                                   |   |                          |


### Methods of biomarker discovery
:methods_of_biomarker_discovery:biomarker_discovery_methods:mass_spectrometry:elisa:

Mass spectrometry-based proteomics:
- powerful method of biomarker discovery and analysis
- involves the identification and qualification of proteins and peptides in biological samples
- every protein has its own unique mass loading ratio
- that way we can count the occurrence of a protein in a sample and compare case and control
- if occurrence in case is higher than in control, it's a potential biomarker
ELISA:
- antibody based verification procedure
- uses protein specific antibodies to detect and quantify proteins in biological samples
- when they bind they can be detected by a colorimetric reaction
- the intensity of the color is proportional to the amount of protein present in the sample

## Gene Panels
:gene_panels:
- Gene panel = collections of genes grouped for testing
- Enables simultaneous sequencing of multiple genes known 
  to be associated with a particular disease or phenotype
- Advances in DNA sequencing technology have made gene 
  panels more economical and efficient than ever before

*Drawbacks:*
- Gene panels lack robustness
- Gene expression data is highly correlated

## Positive & Negative Predictive Value
:positive_predictive_value:ppv:npv:

- *PPV:* The probability that subjects with a positive screening test truly have the disease:
	- PPV = Precision = TP / (TP + FP) = 1 - FDR 
	  (False Discovery Rate = FP / (FP + TP))
- *NPV:* The probability that subjects with a negative screening test truly do not have the disease:
	- NPV = TN / (TN + FN) = 1 - FOR 
	  (False Omission Rate = FN / (FN + TN))

*Advantages of PPV and NPV:*
- In contrast to sensitivity and specificity, PPV and NPV *account for the prevalence (= Weiterverbreitung)* of the disease:
	- PPV increases with increasing disease prevalence
	- NPV decreases with increasing disease prevalence

# Multi-OMICS data integration
Advatage:
- Improves the accruracy and robustness of our model
- In transcriptomics, we have a lot of correlation →  it is difficult to differentiate cause and effect 
  →  we can use other omics data to help us, to get a better understanding of the data and a more clearer picture 
  of whats really improtant

# Summary
![Summary](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Biomarker/summary.png)
![Defining biomarker values](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Biomarker/graphs.png)

→  Hier fehlt der Blick auf das Individuum: Z.B. Smartwatch, die dein ganzes Leben lang Blutdruck misst wäre viel besser 
→  So haben wir eine Referenz für uns selbst
