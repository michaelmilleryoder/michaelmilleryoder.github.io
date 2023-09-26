---
layout: class
title: Homework 2 (CS 2731 Fall 2023)
---

# Homework 2: Text classification ([CS 2731 Fall 2023](https://michaelmilleryoder.github.io/cs2731_fall2023/))
**Due 2023-10-05, 11:59pm**. *Instructions last updated 2023-09-25.*

## Part 1: Learning weights in logistic regression
You are training a classifier for reviews of a new product recently released by a company. You design a couple of features, $$x_1$$ and $$x_2$$. You will be using logistic regression.
With an initialization of the weights w1, w2 and b (the bias) all set = 0, calculate the weights after processing each of the following 3 inputs
x1 = 2, x2 = 1, y = 1
x1= 1, x2 = 3, y = 0
x1 = 0, x2 = 4, y = 0

### Deliverables for Part 1
* In a PDF report, show the values of the weights you calculated after training on each data point. 
Briefly comment on any shift in weights from positive to negative or negative to positive and why this was the case.

## Part 2: Implement a program for politeness classification
In this portion, you will design and implement a program to classify if a Wikipedia talk page post is polite or not. You can use any packages you want for this (scikit-learn, spaCy, NLTK, PyTorch, Keras, code from Homework 1, etc), but these must be specified in the README.txt file, along with version numbers for Python and all packages. We will attempt to run your code on a held-out test set, so the exact environment must be specified. If you will be using a language other than Python, please let us know before submitting. Your script should be able to take the name of a dataset as a single keyword argument.

## Dataset
Here is the dataset that you should download for this assignment:

* [Skeleton Python code](hw1/skeleton.py). You will need to have a Python environment with scipy and numpy packages. Some functions are stubs in the python code. You will need to fill them out.
* [CSV of the complete works of Shakespeare](hw1/shakespeare_plays.csv)
* [Vocab of the complete works of Shakespeare](hw1/vocab.txt)
* [List of all plays in the dataset](hw1/play_names.txt)
* [SNLI corpus](hw1/snli.csv)
	* This corpus is selections from SNLI, a corpus used for the NLP task of "natural language inference" (see [Bowman et al. 2015 dataset paper](https://aclanthology.org/D15-1075/)). Each line contains a sentence that is either a "premise" (an image caption) or a "hypothesis" produced by annotators to be in a certain logical relation with the associated premise (entailment, neutral, contradiction). You don't need to worry about these details, but the `sentenceID` column is a unique index for each sentence and `captionID` is an ID for all sentences associated with same caption/premise.
* [List of identity labels](hw1/identity_labels.txt) from [Rudinger et al. 2017](https://aclanthology.org/W17-1609/)

## 2.1 Feature-based logistic regression models
In this section, you will build a logistic regression model based on features, some that are specified and some that you design. You can do whatever preprocessing you see fit. You will report performance using 5-fold cross-validation on the dataset, which you will set up. 

### Tasks for section 2.1
Implement and try the following feature and model combinations:
* *Logistic regression with bag-of-words (unigram) features*. Build a logistic regression classifier that uses bag-of-words (unigram) features.
* *Logistic regression with tf-idf transformed bag-of-words (unigram) features*. Build a logistic regression classifier that uses tf-idf features.
* *Logistic regression with your own features/change in preprocessing*. Design and test at least one of your own custom features or change the preprocessing in at least one way. Good features for logistic regression are more prevalent or less prevalent with one class than the other. Possible features/changes to add and test include:
	* Counts from custom word lists
	* Any other custom-designed feature (such as length of input, number of capitalized words, etc)
	* N-gram features (sequences of words) beyond the single words used for the bag-of-words features
	* Different preprocessing (stemming, different tokenizations, stopword removal)
	* Reducing noisy features with feature selection
	* Anything else you can think of!

In the report, please provide:
* A table of performance scores for models trained on each set of features. Include precision and recall for the positive (polite) class, as well as accuracy.
* For each feature or change in input text processing:
	* Describe your motivation for including the feature (sampling and examining the test data is one good idea for this)
	* Discussion of results: Did it improve performance or not? (Either result is fine.)
* For your best-performing feature-based model:
	* List the top 2 most informative features that are mostly strongly positively and negatively associated with politeness. Discuss if these are surprising or not and any other comments you might have. You may adapt code provided by the instructor in the Naive Bayes example (notebook [here](https://colab.research.google.com/drive/187yqGR_M_OVYrV28_nzjPY50mm6x-fxJ?usp=sharing)), use another source online, or write your own.
	* Do an error analysis. Provide a confusion matrix and sample multiple examples from both false negatives and false positives. Do you see any patterns in these errors? How might these errors be addressed with different features or if the system could understand something else? (You don’t have to implement these, just speculate.)

## 2.2 Static word embeddings with logistic regression
In this section, you will build and evaluate a logistic regression model with static word embedding features.

### Tasks for section 2.2
* Implement a logistic regression model with pre-trained static word embedding features as input. These can be Word2vec, GloVe, FastText or another pretrained static embedding. To represent the document, you can take the average or some other function of the word embedding for each token.

In the report, please provide:
* Performance scores for this model. Include precision and recall for the positive (polite) class, as well as accuracy. This can be an additional row in the table with other performance scores.
* Discuss the motivation for any choices you made as far as word embedding types, pretraining dataset, and/or how you represented the document, or if you experimented with multiple of these options.

## 2.3 Static word embeddings with feedforward neural network
In this section, you will build and evaluate a feedforward neural network that uses pre-trained static word embeddings as input. You can freeze the word embedding layer or allow it to be trained. You can choose which activation function to use.

### Tasks for section 2.3
* Implement a feedforward neural network with static word embeddings as input.

In the report, please provide:
* Performance scores for this model. Include precision and recall for the positive (polite) class, as well as accuracy. This can be an additional row in the table with other performance scores.
* Discuss the motivation for any choices you made as far as network architecture (number and dimensions of hidden layers) or hyperparameters (learning rate, number of epochs, etc). Note if you experimented with any of these options.

## Notes
* *5 bonus points will be awarded for the best-performing feature-based classifier and 5 bonus points for the best neural network classifier.* 
* Optionally, you may incorporate any form of regularization that you like
* This homework is designed to be able to be run on a laptop with CPUs, not GPUs. Let the instructor/TA know if you are having difficulty completing it with the resources you have.


## Deliverables
* A README.txt file explaining
	* how to run your code
	* the computing environment you used; what programming language you used and the major and minor version of that language; what packages did you use in case we replicate your experiments (a `requirements.txt` file for setting up the environment may be useful if there are many packages).
	* any additional resources, references, or web pages you've consulted
	* any person with whom you've discussed the assignment and describe the nature of your discussions
	* any generative AI tool used, and how it was used
	* any unresolved issues or problems
* Your report with results and answers to questions in Part 1 and Part 2, named `report_{your pitt email id}.pdf`. 
* Your code in a file named `hw2_{your pitt email id}.py`. **This script should be able to take the name of a new dataset, which will be in the same format as the cross-validation set, as a single keyword argument, as in the command `python hw2_{your pitt email id}.py data.csv`.** We will attempt to run this code on a held-out test set.

Please submit all of this material within a zipped directory on Canvas. We will grade your report and attempt to run your code.

## Acknowledgments
This assignment is inspired from a homework assignment by Prof. Diane Litman. Data is from [paper link]().
