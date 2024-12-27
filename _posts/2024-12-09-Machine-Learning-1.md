---
categories: [ Study, Machine Learning ]
tags: [ ai ] 
---

Machine Learning is a crossroad between data science and sofware engineering; its objective is to make a processed data to make a software capable of prediction. In order to fulfill this, a fairly complex mathematical and statitical models are involved.


## Machine Learning as a Function
Since machine learning is based on mathematics and statitics, it is natural to regard it in such a manner. A machine learning model encapsulates a function which returns an output from one or many inputs. An inference process is used to predict future value after defining the function.

The training and inference process advances in the following steps:
1. Training data is formulated from a past observation. Properties or functions of the observed categories are used as "labels" in the model. x is a function/property and y is a label; since observations consists of multiple functions, x is a vector [x1, x2, x3]; For example, when scientists are trying to classify parrots, physical features (such as color, beak size, etc) are x and parrot type is y.

2. Apply algorithm to the accumulateed data and find out the relationship between the functions and the labels; this enables calculations based on x and y.

3. The result of the algorithm is a model(f) encapsulating the function with the calculation. (y=f(x))

4. We are done with training so we can now use this trained model for inference. Models are software programs encapsulating a function retrieved from a training process. a function's output is expressed as ŷ.


## Types of Machine Learning
- Supervised Machine Learning : an algorithm with known functions and label values in the training data
    - Regression : a form of SML where the labels predicted from the label are numerical values 
        - Example: Number of ice creams sold on a day with a fixed temperature, rainfall, wind velocity.
    - Classification : a form of SML for displaying classes
        - Binary Classification: a classification method where labels decide whether the observed category is an instance of a certain class or not. Binary classification might other wise predict results that are mutually exclusive (cannot happen at the same time). 
            - Example : If a patient is likely to have diabete from his/her age, weight, blood sugar level
            - Basically a yes or no
        - Multiclass Classification : predicts a label which stands for one of the multiple available classes.
            - Example : Types of penguins based on physical features
            - more than two possibilities (classes)

- Unsupervised Machine Learning : an algorithm with no known  labels, but only known function values
    - Clustering: The most popular form of UML is clustering. Clustering algorithms groups several individual clusters based on the similarities they have.
        - Example : Groups flowers based on size, number of leaves, etc.
    - In a way, clustering is similar to multiclass classification (Grouping based on observation). However, the difference is that if the model is aware of classes the training data belongs in. 
    - Sometimes, clustering is used before training to decide existing class sets. For example, clustering can be used to divide customers into groups before analyzing them for their class features. Then, classification is used to put labels on the clustered result, and the labeled data can be used to train a model which predicts the group a new customer will belong in.

![image](https://github.com/user-attachments/assets/c1ef0e08-6cf7-42e4-a869-30ab2515e714)


## Regression
Regression models produce number labels based on training data including functions and known labels. A process of training model and evaluating prediction performance is repeated until a certain level of prediction accuracy is met. The diagram below shows the main elements of a training process of SML:

![image](https://github.com/user-attachments/assets/7b061862-b96e-4bf2-a1f3-eb3482a0b9bd)


1. Divide dataset for testing valditity of the model, while maintaining the data's subset.
2. Training data is fit into the model using an algorithm (regression uses algorithms like linear regression)
3. The excluded subset is used to test if the model can predict the label.
4. Compare the predicted result with actual subset values (test value). Then, we calculate a matrix conveying how accurate the predictions were.

We repeat this process until a satisfactory result is attained.

There are a few maxtrix used to evaluate the regression accuracy:
- MAE (Mean Absolute Error) : Variance doesn't care about signs (+-).
- MSE (Mean Squared Error) : We amplify the error.
- RMSE (Root Mean Squared Error) : Since MSE makes result matrix to no loonger reflect the labeled number, we use RMSE. (squared and rooted)
- R^2 (Coefficient of Determination) : Since there exists a random difference between the actual value and the prediction, R^2 accounts for those random variance ratio that can't be covered by a line. 
    - R^2 = 1- ∑(y-ŷ)^2 ÷ ∑(y-ȳ)^2
    - R^2 compares the sum of the squared differences between the predicted labels and the actual labels with the sum of the squared differences between the actual labels and the mean of the actual labels.


## Binary Classification

Binary classification, being a SML, also follows a repetitive process to improve the prediction accuuracy. Of course, unlike regression, binary classification calculates for the probability of classes. 

When training a binary classification model, algorithms like logistic regression is used. A sigmoid function portraying the result can be seen below.

![image](https://github.com/user-attachments/assets/9d0041dd-cff7-4b42-810a-7d056782f7de)

Which can be portrayed as f(x) = P(y=1 | x) in a function.
We drew a line in the middle, so y<0.5 means false and the other half would be true.

The matrix for evaluating a binary classification looks like the one below.

![image](https://github.com/user-attachments/assets/f29365ae-3ca7-43cf-9f91-4e00555b5396)

This is called a confusion matrix, and returns values as followed:

- ŷ=0 & y=0: True Negative(TN)
- ŷ=1 & y=0: False Positive(FP)
- ŷ=0 & y=1: False Negative(FN)
- ŷ=1 & y=1: True Positive(TP)

The Accuracy (matrix measuring ratio of correct cases) is measured like this:
- (TN + TP) / (TN + FN + FP + TP)
- For example, if (2+3) / (2+1+0+3) = 0.83 => 83% Accuracy

The Recall (matrix measuring the ratio of correctly recognized positive cases) is measured like this:
- TP / (TP + FN) 
- For example, 3 / (3+1) = 75% of those with diabetes have been classified as positive

The Precision (matrix measuring positive cases actually being detected) is measured like this:
- TP/ (TP + FP)
- For example, 3 / (3/0) = 100% of positive cases were actually diabetic

The F1 (matrix combining recall and precision) is measured like this:
- (2 * PREC * REC) / (PREC + REC)

The AUC (Area Under Curve) depicts the area under the ROC (graph comparing TPR and FPR, depicting how TPR and FR changes as it approaches the threshold) parabola. If the AUC is 1.0, it is a perfect model (100% correct), and 0.5 means an entirely random guess.

![image](https://github.com/user-attachments/assets/ae50a7a4-2811-4c7b-9516-a6dfda0048ae)

## Reference

[https://learn.microsoft.com/ko-kr/training/modules/fundamentals-machine-learning/](https://learn.microsoft.com/ko-kr/training/modules/fundamentals-machine-learning/)

