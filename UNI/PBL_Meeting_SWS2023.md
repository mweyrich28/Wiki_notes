# PBL Meeting 28-06-2023 
- Barplots
- Split data by ,
- First remove these weird entries
- Splits →  redudancy reduction 100 →  completely redundant , 50 →  removed all seqs that had a sequence similarity of 50%
- Sugestion: 30% redundancy reduction, SPLIT30
- Binary classifier →  am Anfang machen
- Only enzymes →  he will upload the data
- Embeddings help us, they are complicated features
- Don't implement clean
- Implement clean in ESM2?
- Simple model from "scratch"
- Then Embeddings etc etc →  improve the model
- Step by step
- Random baseline comparison
- Working in Groups: Some people work on binary classification, others on a different model then compare
- Or everybody implements their own model and then we compare
- Presentation: standart dev , distribution of seqencelength
- aminoacid distribution / composition
- frequencie of aminoacid counts as input feature / one hot encoding
- EMBEDDINGS are performing best
- present dataset:
	- insights into data, maybe approaches we want to try (contrastive learning)
	- we decide to use split30, but it depends, some cases we might want to use a different split (100%)
	- show 30 and 100
	- some methods benefit having multiple samples of a enzyme family
	- he wants us to see the benefit of redundancy reduction

## What happened in the last 2 weeks 
Project Git:
- A GitHub repository was created where everything is documented
- We are using a .env for the environment variables

One hot encoding:
- We converted Split30 and all proteins (<= 1022) to one hot encoding
- We filtered out all multifunctional enzymes of different main classes
- We made every one hot encoded sequence the same length (which is 1022 AAs long) by adding zeros at the end →  This is not optimal, because we are adding information that is not there
- We also concatenated the one hot encoded sequences to one long vector
- This results in every sequence having a total of 1022 * 20 = 20440 entries
- The output was then stdout to a file

SVM:
- We used the one hot encoded sequences as input for the SVM


# Meeting during exam period 
- Dont do any optimization
- go for results
- Don't remove X
- BLOSUM reduce features
- Other encodings, ohe not ideal

# PBL Meeting 2023-09-06
Fragen:
- Was war der cutoff? ProtT5 →  1024? Wir dachten 1022: 1024 →  first and last entetiy are start and end tokens →  so sequence in total is 1022
Notizen:
- Email alle in cc machen 
- Optuna is an optimizer →  hyperparameter optimization →  best results, has early stopping
- extend cnn with non enzymes
