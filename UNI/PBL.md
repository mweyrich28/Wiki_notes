# MEETINGS TOBIAS
- [PBL_Meeting_2023_11_01](PBL_Meeting_2023_11_01) 
- [PBL_Meeting_2023_10_17](PBL_Meeting_2023_10_17)
- [PBL_Meeting 2023_10_03](PBL_Meeting_2023_10_03)
- [PBL_Meeting_SWS2023](PBL_Meeting_SWS2023)

[PBL_scratchpad](PBL_scratchpad)

# Links
**ZOOM:** https://tum-conf.zoom-x.de/j/63202886852?pwd=Q3hIMkRaS2RJNVdMMUVZVG4wUUI4Zz09
**GOOGLEDOC:** https://docs.google.com/document/d/15DwOm7K61YApvAiY4LyH-0l3AoPX76apr5yUiKNAt_g/edit#heading=h.re35j1ggm5w3
**ROSTLAB:** https://rostlab.org/public/senoner/pbl_2023/
**AI:** https://www.perplexity.ai/
**Sharp:** https://shap.readthedocs.io/en/latest/
**ROLLING SLIDE DECK:** https://docs.google.com/presentation/d/1nXOvPpPtJtgAs2bgqxKO1nhkzBcqYnZnUvY9FQuEK6U/edit#slide=id.g24e36ff07fb_2_536
**ROSALIND:** https://rosalind.info/classes/1003
CLEAN: https://www.science.org/doi/10.1126/science.adf2465
TRUC REPORT: https://docs.google.com/document/d/1pPLVQxp9Ut4bZC9vd8bMaInSURhLbw1IqDKZqZsxNSY/edit

# Notes
[PBL_Multiclass_CNN_Notes](PBL_Multiclass_CNN_Notes)
[PBL_Bootstrapping](PBL_Bootstrapping)

# CNN Results
[PBL_CNN_Results](PBL_CNN_Results)

# Pros of open source AI - 18.12.2023 Groupe discussion
- **Transparency:** Openness about data sources → Verification of data quality, bias, etc.:
	- **More thoughtful development**, since it is more accessible to the public)
	- Greater understanding of how AI works
	- Greater inspection of underlying code
	- individuals can use it to build their own AI solutions
- **Not everybody has GPU** or the necessary resources to train their own models
- **Better recruitment of talent** → attracts more people to the field
- **Potential acceleration/Rapid Innovation:** Open-source AI development fosters rapid innovation by allowing developers
- **Customization and Flexibility:** Open-source AI frameworks provide developers with the freedom to customize and modify the technology according to their specific needs. This flexibility allows for rapid prototyping, experimentation, and adaptation to different use cases, making it easier to address diverse challenges and requirements.
- **Longevity and Independence:** Open-source AI projects are not tied to the fate of a single company


- Introduction should be a bit more detailed than usual
- An outsider that is familiar with biology should undestand what pur problem is
- Always stay as brief as possible
- 1 info per slide
- Not show test data set just say the twst and trainig datasets are similar in terms of statistical characteristocs
- Plot partial values of clean pubication for sota comparison 



# 2023-12-21
TODO für Slides:
- Which dataset will be merged with non enzymes? → For binary classification → New dataset?
- CLEAN performance on NEW dataset has only one score but we don't know on which level
- CLEAN was trained only on enzymes? Our models were trained on non enzymes & enzymes
- Was CLEAN trained on SPLIT100?
- Should we just use ECpred/DeepEC as SOTA comparison?
- How much information do we need to give on the chosen test dataset?
- How important are the error bars for CLEAN since it will most certainly outperform our models by a lot?


# Fragen
## Validation
- Sollen test daten auch \ge 1022 sein?
- weighted F1 score ausrechnen für FNN statt micro oder nochmal fragen
- Für multiclass: soll ich nochmal alles ohne non enzymes trainieren?
## Paper
- Fragen wegen website citing → einmal IUBMB und mass table
- Wie detailliert sollen wir embeddings einleiten/erklären esm2 vs ProtT5
- Quellen angabe zu den scores?
- Unwanted sections in large latex template
- Bootstrapping explanation? alpha + iterations etc.
- Wir haben gzip knn auf undersampeled data trainiert, aber die baseline nimmt die gesamten datenmenge?
- Homology based inference → muss ich das erklären? Und zitieren? Und ist das schon richtig so?
- Wenn wri weitere ansätze in Supplemental Material packen, müssen diese dann auch in methods erklärt werden oder werden in methods nur die ethods erwähnt, die auch in der Discussion sind?
