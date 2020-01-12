---
title:  "Intro to ML by Parth Mehta"
date:   2019-04-17 10:00:00 -0500
categories: Tech
toc: true
toc_label: "On this page"
toc_icon: "list"
excerpt: "Tech session conducted by me teaching ML basics to engineers at Yahoo"
---

# Supervised Machine Learning Models

# Focus of the talk

- Understand core concepts and terminologies for Machine Learning
- How to build Machine Learning models for classification problems and evaluate them
- Supervised Learning models
- Solve an actual ML problem posted on Kaggle

# What is Machine Learning (ML)?

- Machine learning is about extracting knowledge from data.
- We want to learn, from a large dataset, to make decisions based on future observations.				
- You input to a machine learning program a dataset, and it learns to make decisions on future observations by itself.

# Why Machine Learning?

- Creating rule-based system requires deep understanding of how the rules should be made, by an expert.
- The logic required to make a decision is specific to a single domain and task. Changing the task even slightly might require a rewrite of the whole system.
- You cannot create RULES for everything - eg. image recoginition

# Types of Machine Learning

1. **Supervised Learning**    <==   Our focus for today
2. Unsupervised Learning
3. Reinforcement Learning (RL)


# Supervised Learning
- Machine learning algorithms that learn from input/output pairs are called supervised learning algorithms
- The desired outputs (Y vector in the image below) provided for each example act as a “supervisor” to the algorithms to help them learn. 

- Most common type of ML in industry and research currently.

- A common example is spam filtering.
![data-table.png](./data-table.png)

# Mathematically Speaking

Supervised learning is where you have **input variables (x)** and an **output variable (Y)** and you use an algorithm to learn the mapping function from the input to the output.

*Y = f(X)*

The goal is to approximate the mapping function so well that when you have new **input data (x)** that you can predict the **output variables (Y)** for that data.

# Unsupervised Learning in contrast
- In unsupervised learning, even for the given dataset, only the input data is known, and no known output data is given to the algorithm.

- A common example is `Identifying topics in a set of blog posts`

# Reinforcement Learning (RL)
- This branch is increasingly ganining popularity. Alpha Go program from DeepMind company, that defeated the world champion in the game of Go used RL.

- Reinforcement learning is about an agent learning to interact with an environment, with some ultimate goal. When the agent performs a desired action, the algorithm rewards the agent, and when it makes a mistake, the algorithm penalizes the agent. This helps the agent learn.

# Important Python Libraries

Some important python libraries and their uses:

**scikit-learn or sklearn** - scikit-learn is a very popular tool, and the most prominent Python library for machine learning. It contains a number of state-of-the-art machine learning algorithms, as well as comprehensive documentation about each algorithm.

**NumPy** - scikit-learn takes in data only in the form of NumPy arrays. It contains functionality for multidimensional arrays, and complex math operations.

**matplotlib** - matplotlib is the primary scientific plotting library in Python.

**pandas** - pandas is a Python library for data wrangling and analysis. A pandas DataFrame is a table, similar to an Excel spreadsheet. pandas also provides the ability to ingest data from variety of file formats like CSV, SQL, excel files, etc.

# Basic Terminology

To understand the concepts and examples that follow, we need to grasp on some basic terminology used in Machine Learning.

Let's do that with an example


```python
from sklearn import datasets
digits = datasets.load_digits() #pre-loaded labelled dataset

print(digits.keys())
```

    dict_keys(['data', 'target', 'target_names', 'images', 'DESCR'])



```python
print("Dimensions of the data\n{}".format(digits.images.shape))
```

    Dimensions of the data
    (1797, 8, 8)


This tells us that in my dataset, there are 1797 images, each with dimensions 8 x 8 (64 pixels)

This is a very small and simple image dataset.
Every single image is a grayscale image, where each pixel is represented by a brightness value from 0 to 16.

Let's look at how these images look like:


```python
% matplotlib inline
import matplotlib.pyplot as plt
images_and_labels = list(zip(digits.images, digits.target))
for index, (image, label) in enumerate(images_and_labels[:8]):
    plt.subplot(2, 4, index + 1)
    plt.axis('off')
    plt.imshow(image, cmap=plt.cm.gray_r, interpolation='nearest')
    plt.title('Labels: %i' % label)
```


![png](ML_BOF_TALK_files/ML_BOF_TALK_14_0.png)


Let's see how a single image looks like in code.


```python
print("Arrangement of pixels in first image of the dataset\n\n{}".format(digits.images[0]))
```

    Arrangement of pixels in first image of the dataset
    
    [[ 0.  0.  5. 13.  9.  1.  0.  0.]
     [ 0.  0. 13. 15. 10. 15.  5.  0.]
     [ 0.  3. 15.  2.  0. 11.  8.  0.]
     [ 0.  4. 12.  0.  0.  8.  8.  0.]
     [ 0.  5.  8.  0.  0.  9.  8.  0.]
     [ 0.  4. 11.  0.  1. 12.  7.  0.]
     [ 0.  2. 14.  5. 10. 12.  0.  0.]
     [ 0.  0.  6. 13. 10.  0.  0.  0.]]


# Data representation

Since Machine Learning largely includes various mathematical operations over data, **we need to represent our data in a way that we can apply these math operations in an optimized way**

The way we do it is to represent data in the form of matrices, or in programming terms, a 2D array.

Since, each our image is an 8 x 8 matrix and we have about 1800 images, our data is currently represented in 3 dimensions (1800 x 8 x 8).

So instead, we represent each image as a 1 x 64 matrix (or a vector). By doing this, our dataset of images would be a 2D matrix (1800 x 64)


```python
print("Dimensions of the data\n{}\n".format(digits.data.shape))
print("Representation of a single image\n{}".format(digits.data[0]))
```

    Dimensions of the data
    (1797, 64)
    
    Representation of a single image
    [ 0.  0.  5. 13.  9.  1.  0.  0.  0.  0. 13. 15. 10. 15.  5.  0.  0.  3.
     15.  2.  0. 11.  8.  0.  0.  4. 12.  0.  0.  8.  8.  0.  0.  5.  8.  0.
      0.  9.  8.  0.  0.  4. 11.  0.  1. 12.  7.  0.  0.  2. 14.  5. 10. 12.
      0.  0.  0.  0.  6. 13. 10.  0.  0.  0.]


So let's say this is the data we would be working on. 

## GOAL:  To create a model, that learns what digit the images represent and predict accurately the digit in a new image given to it.


Now, that we have the data and have set our goal, we are ready to learn some terms:

## Sample: 
Each sample refers to a single row in a dataset. In our case, a sample would be a single image.
## Feature:
Each column in the dataset is known as a feature vector and each entry in a sample is a feature. For our images, the pixel value is a feature. So our images have 64 features each.

Features are the properties of a sample, that help the machine understand and learn about the sample.

## Label:
Ground truth value of a sample. These are the values against which we check how accurate our predictions are. In our example, the label array tells us the actual value of the digits in the images.



```python
print("Dimensions of the labels array\n{}\n".format(digits.target.shape))
print("Target labels of the images\n{}".format(digits.target))
```

    Dimensions of the labels array
    (1797,)
    
    Target labels of the images
    [0 1 2 ... 8 9 8]


### Generalization, Training Data, Test Data

One of the most important concepts to learn in supervised machine learning, is of generalization.

 - We want to build a machine learning model from this data that can predict the number in a new image. We need some data on which we can assess how our model is doing.

- Unfortunately, we cannot use the data we used to build the model, to evaluate it too. This is because our model can always simply remember the whole training set, and will therefore always predict the correct label for any point in the training set. 


- This **“remembering”** does not indicate to us whether our model will also perform well on new data (in other words, whether it will **generalize** well).


- To assess the model’s learning at every step, we show it new data (data that it hasn’t seen while learning), but for which we have labels. 


- This is usually done by splitting the labeled data we have collected (our 1797 images) into two parts. One part of the data is used to build our machine learning model, and is called the training data or training set. The rest of the data will be used to assess how well the model works; this is called the test data, test set, or hold-out set.


- Think of this as your Math exam in school!!



```python
from sklearn.model_selection import train_test_split
from sklearn import svm

# separating out data for training and testing
X_train, X_test, y_train, y_test = train_test_split(
        digits['data'], digits['target'], random_state=0)

# setting parameters for our model
classifier_model = svm.SVC(gamma=0.01, C=100.)

# training the model on the train data only!
classifier_model.fit(X_train, y_train)

# Let's check how well the model has learned on the training data
train_accuracy = classifier_model.score(X_train, y_train)
print('Train accuracy: {}%\n'.format(train_accuracy * 100))
```

    Train accuracy: 100.0%



Training accuracy only indicates that our model has learned the training set properties well. It doesn't say how well it will perform on new data.


```python
# Now I have a model that has learned to predict the digits, given images. Let's test it out on 1 new image
single_prediction = classifier_model.predict(X_test[0].reshape(1, -1))

print('prediction on new image \n{}\n'.format(single_prediction))

# Now let's see if this matches with the actual label (ground-truth)
plt.imshow(X_test[0].reshape(8,8), cmap=plt.cm.gray_r, interpolation='nearest')
print('label of the new image \n{}\n'.format(y_test[0]))

```

    prediction on new image 
    [2]
    
    label of the new image 
    2




![png](ML_BOF_TALK_files/ML_BOF_TALK_25_1.png)



```python
# Let's check how accurate our model is, using the test data
test_accuracy = classifier_model.score(X_test, y_test)
print('Test accuracy: {}%\n'.format(test_accuracy * 100))
```

    Test accuracy: 86.8888888888889%



- Now, I can infer from this that my model is **87% likely to recognise a new image correctly**. This problem is commonly known as `Optical Character Recognition`

    The above problem is also a good example of a certain type of a Machine Learning problem - **Classification problems**. We want to classify the images into categories.


- A more relatable, but a very similar problem is a spam filter for emails. The goal is simple here: classify my email into either of 2 classes - spam or not spam.

    The interesting question is: what are the features for every email sample?


- The `canIPush` program we are trying to build, is also a perfect example of a classification problem.



# Supervised Machine Learning Problems

- Classification - the goal is to predict a class label, which is a choice from a predefined list of possibilities.
- Regression - the goal is to predict a continuous number.

Example: Predicting a person’s annual income from their education, their age, and where they live is an example of a regression task. When predicting income, the predicted value is an amount, and can be any number in a given range. 



# ML Workflow


![ML workflow chart](./ml-workflow.png)

# Focus today - Building Supervised Learning Models

# So what are ML Models?

- Models are what make the machines "intelligent". 
- They are the algorithms that help the machines learn using the available data, which you can then use as an input/output blackbox to get predictions on real-world input.
- You don't explicitly program the algorithm to answer for the new input. You help it learn from the data samples, and it tries and generalizes it to predict the answer to the new input.

# Model Complexity, Overfitting and Underfitting
![generalization_curve.png](./generalization_curve.png)

# Linear Models for Classification

In our example above, we just used a linear classification model to classify our digits data. We used a library function with an in-built machine learning algorithm with a certain set of parameters.

But how does these classification models work? It is important to know this to select the right model for the right use case, and also to tune a model with correct parameters.

Dhruv will help us answer this question.

# References

Introduction to Machine Learning in Python (IMLP) - https://www.oreilly.com/library/view/introduction-to-machine/9781449369880/
