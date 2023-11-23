# Supervised Machine Learning
:machine_learning:supervised_machine_learning:

1. Vorlesung: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Slides/Bioinf2-Lect02-Supervised_Machine_Learning.pptx.pdf)
2. Tutorium Slides: [Slides](file:///home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/Tutorien/1_Ex_EiB2_supervised_learningstudents.pptx.pdf)
- Hyperparameter: Einstellungen der Methode, die man fine tunen kann

**What to use roead map:** ![Road Map](/home/malte/OneDriver/01_Studium/2.Semester/Einführung in die Bioinformatik II/EntscheidungsHilfe_mchineLerarningSciKit.png)

## Model Evaluation
### Cross Validation
:cross_validation:
- Daten werden in k Teile aufgeteilt
- k-1 Teile werden zum Trainieren verwendet, der letzte Teil zum Testen
- Das wird k mal wiederholt, so dass jeder Teil einmal zum Testen verwendet wird

#### K fold Cross Validation
:cross_validation:k_fold_cross_validation:
- Used technique to evaluate the performance of a classifier
- We have one set of data and we split it into k parts
- All but one part are used for training, the last part is used for testing
- This is repeated k times, so that each part is used once for testing
- ![K fold Cross Validation](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/kFoldCrossValidation.png)

#### Nested Cross Validation
:cross_validation:nested_cross_validation:
- Used technique to find the best hyperparameters for a classifier
- Extends k fold cross validation
- We have one set of data and we split it into k parts
- Inner loop: k fold cross validation to find the best hyperparameters
- Outer loop: k fold cross validation to evaluate the performance of the classifier
- ![Nested Cross Validation](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/nestedCrossValidation.png)

#### Leave one out Cross Validation
:cross_validation:leave_one_out_cross_validation:
- ![Leave one out Cross Validation](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/leaveOneOutCrossValidation.png)

### Bootstrapping
:bootstrapping:
- Anders als Cross validation
- Datenpunkte liegen in Urne und werden *zufällig mit zurücklegen* gezogen
- has a larger bias than cross validation
- that's why there are several implementations of bootstrapping

### Wiederholung Sensitivity, Specificity, Accuracy, Precision, Recall, F1-Score, PPV, NPV
:recall:precision:accuracy:sensitivity:specificity:f1_score:ppv:npv:tp:tn:fp:fn:

#### SENSITIVITY/RECALL
$$
TPR = \frac{TP}{P} = \frac{TP}{TP+FN}
$$

#### SPECIFICITY 
$$
TNR = \frac{TN}{N} = \frac{TN}{TN+FP}
$$


#### ACCURACY 
$$
ACC = \frac{TP+TN}{n}
$$

#### F1-SCORE 
$$
2 \cdot \frac{precision \cdot recall}{precision + recall}
$$

#### PRECISION / PPV
> The probability that subjects with a positive screening test truly have the disease:
$$
PPV = \frac{TP}{TP+FP} = 1 - \underbrace{FDR}_{\frac{FP}{FP+TP}}
$$

#### NPV
> The probability that subjects with a negative screening test truly do not have the disease:
$$
NPV = \frac{TN}{TN+FN} = 1 - \underbrace{FOR}_{\frac{FN}{FN+TN}}
$$

### Performance of Classifiers
:roc:auc:
**ROC (= Receiver Operator Characteristics):** ![ROC & AUC](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/roc.png)
- x: FP rate = 1 - Specificity, y: TP rate = Sensitivity
- Fläche unter kurve sollte maximal sein
- Mittlere Diagonale: Random Classifier

# Typical Classifiers
- Naive Bayes
- K-nearest neighbors
- Decision Trees: purity and Gini index, pruning
- Random Forest
- Boosted Trees
- Support Vector Machines
- Neural Networks

## K Nearest Neighbors
:k_nearest_neighbors:knn:
- Schaut sich die k nächsten Nachbarn an, wir klassifizieren unseren neuen Datenpunkt dann zu der Kategorie, 
  welche der häufigst gezählte Nachbar des neuen Datenpunktes ist. 
  Haben wir z.B. 5 Rote und 3 grüne Nachbarn, so ist unser neuer Datenpunkt rot.
- k is often chosen to be odd to avoid ties
- If there's still a tie, we can choose randomly
- low values for k can lead to overfitting, are noisy and sensitive to outliers
- high values for k can lead to underfitting, are smooth but ignore local structure
- Wie weit sind die Nachbarn entfernt? We calculate the distance
- Was ist ein Nachbar: Radius als Einschränkung oder, wir betrachten nur die $k$ nächsten Nachbarn

## Decision Trees
:decision_tree:
- Each node tests an attribute, also ein feature (Rain: yes, no?)
- Each branch corresponds to an attribute value
- Each leaf node assigns a classification
- Impurity: How well does a split separate the classes? Let's say we want to 
  choose the root node for a decision tree: ![Nodes](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/dTreesExample.png)
  of these should be our root? We want to choose the one that separates the classes the best. 
  →  Non of these nodes is perfect and we *measure this with impurity*.

### Impurity
:impurity:impurity_funvtions:re_substitution_error:gini_index:entropy:information_gain:
- we want to choose the node that separates the classes the best
- we measure this with impurity
- impurity should be low
- ![Impurity Functions](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/purity_functions.png)

## Random Forest
:random_forest:
- A decision tree alone might perform very good on the training data, but it might not generalize well →  Random Forest
- Ist eine Ensemble Methode und basiert auf Decision Trees, macht aber nicht nur einen Baum
- Quite robust to overfitting
- Quite robust to unbalanced class sizes

*CREATING A RANDOM FOREST:*
1. Create a new dataset, by sampling with replacement from the original dataset (bootstrapping)
2. Create a decision tree from the new dataset. At each node:
	- Randomly select $m$ features without replacement, e.g. blood pressure and height for $m = 2$
	- Split the node using the feature that provides the best split according to the objective function, for instance, maximizing the information gain
	- The feature used for this split won't be available for selection in the next step
3. Repeat the steps 1 and 2 until a tree is formed
4. Repeat steps 1 to 3 to create a forest of trees

We are left with a wide variety of trees, which are all different from each other. This is the "forest" part of the random forest. The trees will be different because each tree is created from a different bootstrapped sample of the original dataset. Additionally, at each node, the split is done by randomly selecting $m$ features without replacement from the $p$ features available. The value of $m$ is held constant during the forest creation. The value of $m$ is a hyperparameter of the random forest algorithm.
This variety makes random forests robust to outliers and noise in datasets. Additionally, the random forest algorithm is also robust to overfitting. This is because the algorithm relies on the power of ensemble learning, which reduces the variance of the model, without increasing the bias. The only drawback of the random forest algorithm is that it is difficult to interpret a large number of trees.

When classifying a new sample, we put it into every decision tree we created and then compare how many
trees predict class 1 and how many trees predict class 2. The class with the most votes wins.

### Out of bag error
:out_of_bag_error:
Evaluation: Typically, 1/3 of the data doesn't end up in the bootstrapped data set. We can use this left over
data to validate the model. This is called the out-of-bag error estimate. Out-of-bag error = samples out of the left over dataset, 
which were wrongly classified

Try different values for $m$ and see which one gives the best random forest

### Random Forests vs Boosted Trees
- Gradient boosting is a set of decision trees (just like random forests)
- Main differences:


|                     | Building Trees                                                                                  | Treating results                                                                | Tries to                     |
|---------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|------------------------------|
| *Random Forest*     | build each tree independently                                                                   | combines results *at the end of the process* (by averaging or "majority rules") |                              |
| *Gradient Boosting* | one tree at a time, where each new tree helps to correct errors made by previously trained tree | Gradient boosting combines results *along the way →  additively*                | *minimize the loss function* |


- Gradient boosting can result in *better performance*, but it's more sensitive to overfitting
- Random forests are more *robust to noise and overfitting* and is *easier to tune*

## Support Vector Classifier
:support_vector_classifier:
Maximum margin Classifier: Maxes out the margin distance between the closest points of each class
- BUT: not robust to outliers
Support Vector Classifier: allows some points to be on the wrong side of the margin
- We use cross validation to find the optimal soft margin (= how many miss classifications do we allow to lie inside our margin?)
![Terminology](/home/malte/01_Documents/vimwiki/Assets/2.Semester/Bioinformatik/Machinelearning/SVM/terminology.png)

### Support Vector Machines
:support_vector_machine:
- Support Vector Machines are an extension of the support vector classifier
- They are used for classification, regression and outlier detection
- Project data into a higher-dimensional space
- *Kernel Functions:* searches for a separating hyperplane in the higher-dimensional space. 
  That's how we know which function to use to project the data into the higher-dimensional space 
- Kernel Trick: We don't actually have to project the data into the higher-dimensional space, 
  we can just use the kernel function to calculate the distance between the data points in the higher-dimensional space
- Find a hyperplane that separates the data into classes
- The hyperplane is chosen to maximize the margin between the classes

## Artificial Neural Network
:artificial_neural_network:neural_network:
- Artificial Neural Networks are inspired by the human brain
- They are used for classification, regression and clustering
- They are very powerful and can be used for complex problems

### Advantages
- Data doesn't have to be normally distributed
- We can detect complex non-linear relationships
- Fault tolerance: If one neuron fails, the network still works
- Noise and missing values are not a problem
- Well suited for generalization

### Disadvantages
- Expensive and time consuming to train
- Overfitting is a problem
- Black-box: We don't know how the network works

### Activation Functions
- They are needed to squeeze the weighted sum of the inputs into a certain range (e.g. between 0 and 1)
- Weight: How important is the input for the output?
- Bias: How easy is it to get the neuron to fire? Maybe the neuron is always active, even if the input is 0
- Sigmoid function is not that popular anymore, because it is computationally expensive
- Rectified Linear Unit (ReLU) is the most popular activation function: ReLU(a) = max(0,a)

### Adding more hidden layers
Gains:
- More complex relationships can be modeled
- Better generalization
- Additional flexibility
Risks:
- Time consuming to train
- Overfitting is a problem
- More black-box →  Less understandable

### Why is the training of an ANN so time consuming?
- We have to find the optimal weights and biases for each neuron
- Solution: *Stochastic gradient:* We don't calculate the gradient for the whole dataset, but only for a small subset of the data. 
  That way we can estimate the gradient for the whole dataset and it is much faster
