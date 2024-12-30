---
categories: [ Study, Machine Learning ]
tags: [ ai ] 
---


## Multiclass Classification

Multiclass Classification predicts which of the multiple classes the input belongs to, and follows an identical repetitive training, testing, and evaluation process like the other SMLs.

Multiclass Classification uses multiple training algorithms, among which are:
- OvR(One-vs-Rest) Algorithm : proceeds machine learning based on the binary classification function of each class, and each class calculates the probability of the observed instance being a target class.
    - If there are 3 classes, there would be 3 binary classification functions:
        - f0(x) = P(y=0|x)
        - f1(x) = P(y=1|x)
        - f2(x) = P(y=2|x)
    - Each algorithm forms a sigmoid fuction calculating probability between 0.1 and 1.0.
    - We predict the class of the functionwhich creates the highest probability output.
- Polynomial Algorithm : An algorithm with the output being the vector(array) containing the probability variance of all the classes, with the probability adding up to 1.0.
    - f(x) =[P(y=0|x), P(y=1|x), P(y=2|x)]

The evaluation of multiclass classification is done through a confusion matrix.

![image](https://github.com/user-attachments/assets/a5b933ab-5a44-47cf-9daf-012f9587cf95)


The total accuracy, recall, and precision, when using the above matrix would be.
- Total Accuracy = (13+6)÷(13+6+1+1) = 90%
- Total Recall = 6÷(6+1) = 86%
- Total Precision = 6÷(6+1) = 86%

The F1 score would be
- Total F1 Score = (2x0.86x0.86)÷(0.86+0.86) = 86%

## Clustering

Labels in clustering are created only through observed features.

There are various algorithms usable during clustering, but the most prevalently used one is K-means clustering, which follows these steps:

1. Function(x) value is vectorized in order to define a N-dimension coordinate. (N is the number of features)
    - In case of flowers, there would be two cooridnates [x1,x2], number of leaves and number of petals
2. The number of clusters (k) for grouping the elements is set.
    - For example, in order to make 3 clusters, we use 3 as k. Then, k points are plotted on temporary coordinates, and become the centroids of the cluster.
3. Each data point (in this example a flower) is allocated to the closest centroid.
4. Each centroid moves to the center of the data points allocated to them based on the average distance among points.
5. Data points are reassigned to the cluster based on the new closest centroid after the centroids have been moved.
6. This process is repeated until the clusters stabilize or a repetition threshold set in advance.

Clustering models can be evaluated with the following components:
- Average distance from the centroid of a cluster
- Average distance to other centroids
- Max distance from the centeroid of a cluster
- Silhouette : value between -1 and 1 summarizing distance ratio among the points in the same cluster and points in different clusters. (value close to 1 has better segregated clusters)

## Deep Learning

Deep learning is basically an emulation of a human brain materialized by machine learning. We do this by formulating an artificial neural network. In an artificial NN, each neuron is a function reacting to input x and weight w. Function is wrapped in an "activation function" which decides rather to deliver output. 

ANN is composed of mutiple layers of neurons and models from this architecture is referred to as Deep Neural Network. Like the other machine learning techniques, deep learning intakes one or multiple features(x) and creates a function predicting labels(y). Functions (f(x)) are exterior layer for the nested functions, where each layer of the neural network encapsulates a function that operates on x, combined with weight (w) values associated with it.

The algorithm used to train the model iteratively feeds the feature values (x) of the training data through the layers to compute the output value ŷ. It then validates how far the computed ŷ is from the known y value by quantifying the model's error or loss level. The weights (w) are subsequently adjusted to reduce the loss. The trained model contains the final weight values that produce the most accurate predictions.


The weight of a NN is the key for calculating predicted values of labels. The model learns the weight belonging to the most accuratly predicting train processes. The process of learning is as follows:
1. The training/validity test data sets are defined and provided to the training features are provided to the input layer.
2. Neurons in each layer of a network applies a weight (initially randomly assigned) and produces data through the network
3. Output layer creates a vector containing calculations including ŷ.
4. Loss function is used to compare the predicted ŷ and the actual y values, and enumerate the difference (called a loss). The loss function calculates the enumerate variance of multpiple cases and sums them up to a singular loss value.
5. Since the entire network is basically a massive nested function, the optimization function uses differentiation calculator to decide the method to evaluate the effect of each weight to the loss of the network and calibrate (up or down) them to reduce the amount of loss. Generally, the Gradient descent method (method using function's slope to find optimal weight), to minimize loss.
6. The weight change history is backpropagated into the network layers to replace previously used weight.
7. This process goes through repeated epochs until the loss is minimized and the model can make predictions to some degree.

![image](https://github.com/user-attachments/assets/01c2d433-52be-4507-b040-be5062f6a6bf)


## Azure Machine Learning

Microsoft Azure Machine Learning is a cloud service for training, deploying, and managing machine learning models. It has the following capabilities:
- Exploring and preparing data for modeling
- Training and evaluating machine learning models
- Registering and managing trained models
- Deploying trained models for use in applications and services
- Reviewing and applying responsible AI principles and practices.

Azure Machine Learning provides these features to enhance machine learning workload:
- Centralized storage and management of datasets for model training and evaluation.
- On-demand computing resources to run machine learning tasks such as model training.
- AutoML (Automated Machine Learning) allows you to easily run multiple training jobs with different algorithms and parameters to find the best model for your data.
- A visual tool to define orchestrated pipelines for processes such as model training or inference.
- Integration with popular machine learning frameworks like MLflow, making it easy to manage model training, evaluation, and deployment at scale.
- Built-in support for visualizing and evaluating metrics for responsible AI, including model explainability and fairness assessments.

Users can run the following tasks with the Azure Machine Learning Studio:

- Import and export data
- Create and use computing resources
- Run code in notebooks
- Create jobs and pipelines using visual tools
- Train models using Automated Machine Learning
- View details of trained models, including evaluation metrics, responsible AI information, and training parameters
- Deploy trained models for real-time and batch inference
- Import and manage models from a comprehensive model catalog

![image](https://github.com/user-attachments/assets/1bf25fdf-ff49-4caa-a5f1-1e3694265d2f)

## Reference

[https://learn.microsoft.com/ko-kr/training/modules/fundamentals-machine-learning/](https://learn.microsoft.com/ko-kr/training/modules/fundamentals-machine-learning/)

