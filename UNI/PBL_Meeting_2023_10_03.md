# Contents

- [03.10.2023](#03102023)
    - [Questions](#questions)
    - [Information about the datasets used for training](#information-about-the-datasets-used-for-training)
    - [Main Class Prediction](#main-class-prediction)
        - [CNN Split100 predicting only Main Class (= Model of last Meeting)](#cnn-split100-predicting-only-main-class-model-of-last-meeting)
    - [Enzyme/NonEnzyme Classification](#enzymenonenzyme-classification)
        - [CNN Split70 Binary Classifier (Optimized with Optuna)](#cnn-split70-binary-classifier-optimized-with-optuna)
            - [Combinding binary CNN with multi-class CNN](#combinding-binary-cnn-with-multi-class-cnn)
        - [CNN Split50 Main Class and Enzyme/NonEnzyme classification](#cnn-split50-main-class-and-enzymenonenzyme-classification)
    - [CNN 1st Subclass Prediction](#cnn-1st-subclass-prediction)
        - [1. Main Class 1st Subclass CNN](#1-main-class-1st-subclass-cnn)
        - [2. Main Class 1st Subclass CNN](#2-main-class-1st-subclass-cnn)
        - [3. Main Class 1st Subclass CNN](#3-main-class-1st-subclass-cnn)
        - [4. Main Class 1st Subclass CNN](#4-main-class-1st-subclass-cnn)
        - [5. Main Class 1st Subclass CNN](#5-main-class-1st-subclass-cnn)
        - [6. Main Class 1st Subclass CNN](#6-main-class-1st-subclass-cnn)
        - [7. Main Class 1st Subclass CNN](#7-main-class-1st-subclass-cnn)

# 03.10.2023

## Information about the datasets used for training

***All sampes used for training are:***
- $\le$ 1022 AAs long
- Don't contain AA "O|U"
- For Enzymes: No Multifunctional Enzymes (based on 1st EC number) are allowed

## Main Class Prediction 

### CNN Split100 predicting only Main Class (= Model of last Meeting)
![CNN Main Class](/home/malte/Desktop/Dataset/plots/cnn/enzymes_only/cnn_v5_1_100_loss.png)
![CNN Main Class](/home/malte/Desktop/Dataset/plots/cnn/enzymes_only/cnn_v5_1_100_scores.png)
![CNN Main Class](/home/malte/Desktop/Dataset/plots/cnn/enzymes_only/cnn_v5_1_100_conf.png)

## Enzyme/NonEnzyme Classification

### CNN Split70 Binary Classifier (Optimized with Optuna)
![CNN Binary](/home/malte/Desktop/Dataset/plots/cnn/enzyme_non_enzyme/cnn_binary_v2__opt_S70_loss.png)
![CNN Binary](/home/malte/Desktop/Dataset/plots/cnn/enzyme_non_enzyme/cnn_binary_v2__opt_S70_score.png)
![CNN Binary](/home/malte/Desktop/Dataset/plots/cnn/enzyme_non_enzyme/cnn_binary_v2__opt_S70_conf.png)

#### Combinding binary CNN with multi-class CNN
``` dot
digraph Model {
	
		Input [shape=Isquare];
		Stop [shape=diamond, style=filled, color=red];
		BinaryCNN [shape=square, style=filled, color=lightgrey];
		MulticlassCNN [shape=Msquare, style=filled, color=lightgrey];
		
		Input -> BinaryCNN [label="ESM2"];
		BinaryCNN -> NonEnzyme [label="0"];
		BinaryCNN -> Enzyme [label="1"];
		NonEnzyme -> Stop [label="Label 7"];

		node [style=filled, color=lightblue];
		0 [shape=diamond];
		1 [shape=diamond];
		2 [shape=diamond];
		3 [shape=diamond];
		4 [shape=diamond];
		5 [shape=diamond];
		6 [shape=diamond];
		Enzyme -> MulticlassCNN [label="ESM2"];
		MulticlassCNN -> 0 [label="Class 1"];
		MulticlassCNN -> 1 [label="Class 2"];
		MulticlassCNN -> 2 [label="Class 3"];
		MulticlassCNN -> 3 [label="Class 4"];
		MulticlassCNN -> 4 [label="Class 5"];
		MulticlassCNN -> 5 [label="Class 6"];
		MulticlassCNN -> 6 [label="Class 7"];
		
		{ rank=same; BinaryCNN MulticlassCNN }
		{ rank=same; 0 1 2 3 4 5 6 Stop }
		rankdir=LR;
}
```

### CNN Split50 Main Class and Enzyme/NonEnzyme classification (Optimized with Optuna)
![MulticlassCNN](/home/malte/Desktop/Dataset/plots/cnn/enzyme_non_enzyme/cnn_v1_opt_S50_loss.png)
![MulticlassCNN](/home/malte/Desktop/Dataset/plots/cnn/enzyme_non_enzyme/cnn_v1_opt_S50_score.png)
![MulticlassCNN](/home/malte/Desktop/Dataset/plots/cnn/enzyme_non_enzyme/cnn_v1_opt_S50_conf.png)

# Predicting 1st Subclass

## CNN 1st Subclass Prediction

**Split100 Class Distribution:**

![S100 Dist](/home/malte/Desktop/Dataset/plots/class_count_comparison/SPLIT100.png)

### 1. Main Class 1st Subclass CNN
![Distribution](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_1_s100_class_dist.png)
**Control:**
```zsh
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^1.23" | wc -l
17
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^1.20" | wc -l
64
```
**Label dictionary for outputlayer:**
```python
sec_to_label = {1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5, 7: 6, 8: 7, 9: 8, 10: 9, 11: 10, 12: 11, 13: 12, 14: 13, 15: 14, 16: 15, 17: 16, 18: 17, 20: 18, 21: 19, 23: 20, 97: 21}
label_to_sec = {0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6, 6: 7, 7: 8, 8: 9, 9: 10, 10: 11, 11: 12, 12: 13, 13: 14, 14: 15, 15: 16, 16: 17, 17: 18, 18: 20, 19: 21, 20: 23, 21: 97}
```
![Loss](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_1_s100_class_loss.png)
![Score](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_1_s100_class_score.png)
![Conf Matrix](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_1_s100_class_conf.png)

### 2. Main Class 1st Subclass CNN
![Distribution](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_2_s100_class_dist.png)
**Control:**
```zsh
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^2.9" | wc -l
241
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^2.10" | wc -l
20
```
**Label dictionary for outputlayer:**
```python
sec_to_label = {1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5, 7: 6, 8: 7, 9: 8, 10: 9}
label_to_sec = {0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6, 6: 7, 7: 8, 8: 9, 9: 10}
```
![Loss](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_2_s100_class_loss.png)
![Score](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_2_s100_class_score.png)
![Conf Matrix](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_2_s100_class_conf.png)

### 3. Main Class 1st Subclass CNN
![Distribution](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_3_s100_class_dist.png)
**Control:**
```zsh
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^3.7" | wc -l
186
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^3.8" | wc -l
54
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^3.9" | wc -l
8
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^3.10" | wc -l
1
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^3.11" | wc -l
71
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^3.13" | wc -l
24
```
**Label dictionary for outputlayer:**
```python
sec_to_label = {1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5, 7: 6, 8: 7, 9: 8, 10: 9, 11: 10, 13: 11}
label_to_sec = {0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6, 6: 7, 7: 8, 8: 9, 9: 10, 10: 11, 11: 13}
```
![Loss](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_3_s100_class_loss.png)
![Score](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_3_s100_class_score.png)
![Conf Matrix](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_3_s100_class_conf.png)

### 4. Main Class 1st Subclass CNN
![Distribution](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_4_s100_class_dist.png)
**Control:**
```zsh
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^4.5" | wc -l
2
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^4.7" | wc -l
2
```
**Label dictionary for outputlayer:**
```python
sec_to_label = {1: 0, 2: 1, 3: 2, 4: 3, 99: 4, 6: 5, 7: 6, 5: 7}
label_to_sec = {0: 1, 1: 2, 2: 3, 3: 4, 4: 99, 5: 6, 6: 7, 7: 5}
```
![Loss](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_4_s100_class_loss.png)
![Score](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_4_s100_class_score.png)
![Conf Matrix](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_4_s100_class_conf.png)

### 5. Main Class 1st Subclass CNN
![Distribution](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_5_s100_class_dist.png)
**Control:**
```zsh
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^5.99" | wc -l
3
```
**Label dictionary for outputlayer:**
```python
sec_to_label = {1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5, 99: 6}
label_to_sec = {0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6, 6: 99}
```
![Loss](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_5_s100_class_loss.png)
![Score](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_5_s100_class_score.png)
![Conf Matrix](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_5_s100_class_conf.png)

### 6. Main Class 1st Subclass CNN
![Distribution](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_6_s100_class_dist.png)
**Control:**
```zsh
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^6.4" | wc -l
52
~/Desktop/Dataset/data/enzymes/csv ❯ cut -f2 -d "," split100.csv | grep -P "^6.6" | wc -l
41
```
**Label dictionary for outputlayer:**
```python
sec_to_label = {1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5}
label_to_sec = {0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6}
```
![Loss](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_6_s100_class_loss.png)
![Score](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_6_s100_class_score.png)
![Conf Matrix](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_6_s100_class_conf.png)

### 7. Main Class 1st Subclass CNN
![Distribution](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_7_s100_class_dist.png)
**Label dictionary for outputlayer:**
```python
sec_to_label = {1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5}
label_to_sec = {0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6}
```
![Loss](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_7_s100_class_loss.png)
![Score](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_7_s100_class_score.png)
![Conf Matrix](/home/malte/01_Documents/projects/pbl_binary_classifier/tf_cnn_esm2/2nd_ec_class_pred/Plots/class_7_s100_class_conf.png)


# Notes
- Group them in other (range) 
- How secure are we with prediction 
- Cache maybe 
- One model better then many 
- Pre analysis Both embeddings 
- Correlation calculation maybe Trend in size 
- Maybe run pca 
- Homology based inference 
