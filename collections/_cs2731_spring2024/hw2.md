---
layout: class
title: Homework 2 (CS 2731 Spring 2024)
---

# Homework 2: Text classification ([CS 2731 Spring 2024](https://michaelmilleryoder.github.io/cs2731_spring2024/))
**Due 2024-02-15, 11:59pm**. *Instructions last updated 2024-01-30.*

## Learning objectives
After completing this assignment, students will be able to:
* Demonstrate how weights adjust to better fit training input in stochastic gradient descent
* Implement a text classification system using both feature-based and neural network approaches
* Identify informative features in a feature-based text classification system
* Analyze errors in an NLP system


## Part 1: Learning weights in logistic regression
You are training a classifier for reviews of a new product recently released by a company. You design a couple of features, $$x_1$$ and $$x_2$$. You will be using logistic regression.
With an initialization of the weights $$w_1$$, $$w_2$$ and $$b$$ (the bias) all set = 0 and a learning rate $$\eta=0.2$$, calculate the weights after processing each of the following 3 inputs:
1. $$x_1 = 2, x_2 = 1, y = 1$$
2. $$x_1 = 1, x_2 = 3, y = 0$$
3. $$x_1 = 0, x_2 = 4, y = 0$$

During calculations, keep at least 3 significant digits for values. Points will not be taken off for slight differences due to rounding.

### Deliverables for Part 1
In the report:
* Give weights after training on each data point (3 total weight changes, one after each timestep/data point).
* Show your work in calculating the values of the weights after training on each data point.
* Briefly comment on any shift in weights from positive to negative or negative to positive and why this was the case.

## Part 2: Implement a politeness classifier
In this portion, you will design and implement a program to classify if an online comment is polite or not. You can use any packages you want for this (scikit-learn, spaCy, NLTK, Gensim, code from Homework 1, etc). Any packages used should be specified in the `README.txt` file, along with version numbers for Python and all packages. If you will be using a language other than Python, please let us know before submitting. Your script should be able to take the name of a dataset as a single keyword argument.

## Dataset
Here is the dataset that you should download for this assignment:

* [`politeness_train.csv`](hw2/politeness_train.csv). This dataset has 3 fields:
	* `utterance_id`: a unique identifier for the post
	* `conversation_id`: a unique identifier for the conversation the post came from
	* `text`: the text of the comment
	* `polite`: a binary class label of whether or not the comment was annotated to be polite (1) or not (0)
* [`politeness_test.csv`](hw2/politeness_test.csv) (only necessary if participating in the optional challenge). This data has the same fields as the training data. You will use this in the optional challenge competition hosted on Kaggle.


This dataset consists of requests among Wikipedia editors posted on user talk pages, as well as posts on the coding help forum Stack Exchange (see the Stanford Politeness Corpus, [Danescu-Niculescu-Mizil et al. 2013](https://aclanthology.org/P13-1025)). 

## 2.1 Feature-based logistic regression models
In this section, you will build a logistic regression model based on bag-of-word features and/or features of your own design. You can do whatever preprocessing you see fit. You will report performance using 5-fold cross-validation on the dataset, which you will set up. Make sure to just extract features (bag-of-words, etc) from the training set and not the test folds within cross-validation.

### Tasks for section 2.1
Implement and try the following feature and model combinations:
* *Logistic regression with bag-of-words (unigram) features*. Build a logistic regression classifier that uses bag-of-words (unigram) features.
* *Logistic regression with your own features/change in preprocessing*. Design and test at least two of your own custom features or change the preprocessing in at least one way. Note that these features can be used in conjunction with bag-of-words features or by themselves. Possible features/changes to add and test include:
	* Tf-idf transformed bag-of-words features
	* Changing count bag-of-words features to binary 0 or 1 for the presence of unigrams
	* N-gram features (sequences of words) beyond the single words used for the bag-of-words features
	* Different preprocessing (stemming, different tokenizations, stopword removal)
	* Reducing noisy features with feature selection
	* Counts from custom word lists
	* Static word embeddings of your choice (do not use any contextualized word embeddings, such as BERT, for this part)
	* Any other custom-designed feature (such as length of input, number of capitalized words, etc)

You will thus have 3 total logistic regression models: one using bag-of-word features and 2 with your own selected features or preprocessing changes.

In the report, please provide:
1. A table of 5-fold cross-validation performance scores for models trained on each set of features. Include accuracy as well as precision, recall, and f1-score for the positive (polite) class.
1. For each feature or change in input text processing:
	1. Describe your motivation for including the feature
	1. Discussion of results: Did it improve performance or not? (Either result is fine. It is not necessary to beat logistic regression with unigram features.)
1. For a feature-based model of your choice:
	1. List the top 2 most informative features that are mostly strongly positively and negatively associated with politeness. Discuss if you find these surprising and any other comments you might have. You may adapt code provided by the instructor in the Naive Bayes example (notebook [here](https://colab.research.google.com/drive/1QFYJjqkdKDh-OFr3aqdD4OkddYtq3QLB?usp=sharing)), use another source online, or write your own. Give specific informative features, such as particular words (e.g. "actually") for bag-of-words features, instead of sets of features like "tf-idf unigram features".
	1. Do an error analysis. Provide a confusion matrix and sample multiple examples from both false negatives and false positives. Do you see any patterns in these errors? How might these errors be addressed with different features or if the system could understand something else? (You don’t have to implement these, just speculate.)

## 2.2 Neural network-based approaches
In this section, you will build and evaluate neural network-based classifier on politeness classification. For example, you could implement a feedforward neural network that uses pre-trained static word embeddings (word2vec, GloVe, FastText, etc) as input. To represent the document, you could take the average word embeddings of the input sentence or choose another function. You can choose which activation function to use and other hyperparameters. You are also welcome to try other methods we haven't yet covered in class, such as LSTMs, convolutional neural networks, BERT, or other LLMs. As long as the technique uses neural networks at some point in its architecture and involves some sort of training or fine-tuning of a model, it will be accepted. Simply prompting a pre-trained LLM to classify the instances ("zero-shot" or "in-context" learning) will not be sufficient. If you have questions about what is acceptable, ask the instructor or TA.

You will again use 5-fold cross validation on the dataset. There is no need for this model to outperform the logistic regression model you made.

### Tasks for section 2.2
* Implement a neural network-based politeness classifier, such as a feedforward neural network with static word embeddings as input.

In the report, please provide:
* Performance scores for this model. Include accuracy as well as precision, recall, and f1-score for the positive (polite) class. This can be an additional row in the table with other performance scores.
* Discuss the motivation for any choices you made as far as neural classifier, word embedding types, pretraining dataset, and/or how you represented the document, or if you experimented with multiple of these options.
* Discuss the motivation for any choices you made as far as network architecture (number and dimensions of hidden layers) or hyperparameters (learning rate, number of epochs, etc). Note if you experimented with any of these options.

## 2.3 (*optional*) Submit your classifier in the class challenge
Optionally, you can submit your classifier to run on a hidden held-out test set as part of a class competition. Bonus points will be awarded in the competition as follows, as measured by accuracy on our held-out test set.
* 5 bonus points for the best-performing logistic regression classifier
* 5 bonus points for the best neural network classifier
* 3 bonus points for the 2nd best-performing logistic regression classifier
* 3 bonus points for the 2nd best-performing neural network classifier
* 1 bonus point for scoring in the top 50% of logistic regression classifiers
* 1 bonus point for scoring in the top 50% of neural network classifiers

### How to submit your classifier
Please see the [Kaggle competition page](https://www.kaggle.com/t/2ee28c56ec2d43beb8f75f54a277f2c4) for instructions on how to submit for the challenge competition.

You will need to create a Kaggle account to submit. Please provide your Kaggle username used in the competition in your report so we can assign any bonus points. Note that this username will be visible in a leaderboard to other challenge competition participants.

## Notes
* Don't feel like you need to write things from scratch; use as many packages as you want. Google and Stack Overflow and NLP/ML software documentation are your friend! Adapting and consulting other approaches is fine and should be noted in comments in the code and/or in the `README.txt`. Just don't use complete, fully-formed implementations for this (including from generative AI tools). Use resources as an aid, not as a final product.
* Optionally, you may incorporate any form of regularization that you like
* This homework is designed to be able to be run on a laptop with CPUs, not GPUs. Let the instructor/TA know if you are having difficulty completing it with the resources you have.


## Deliverables
* Your report with results and answers to questions in Part 1 and Part 2, named `report_{your pitt email id}.pdf`. No need to include @pitt.edu, just use the email ID before that part. For example: `report_mmy29_hw2.pdf`.
	* If participating in the challenge, the Kaggle username you used to submit your predictions
	* If participating in the challenge, your code used for that in a file named `hw2_{your pitt email id}_test.py`. 
* Your code used to train models and estimate performance with cross-validation in a file named `hw2_{your pitt email id}_train.py`.
* A `README.txt` file explaining
	* how to run the code you used to train your models and estimate cross-validation performance
	* the computing environment you used, including the names and versions of programming languages and packages used, in case we replicate your experiments. A `requirements.txt` file for setting up the environment is useful if there are many packages.
	* any additional files needed to run the code, such as the names and versions of pretrained embeddings
	* any additional resources, references, or web pages you've consulted
	* any person with whom you've discussed the assignment and describe the nature of your discussions
	* any generative AI tool used, and how it was used
	* any unresolved issues or problems

Please submit all of this material on Canvas. We will grade your report and look over your code.

## Grading
See rubric on Canvas.

## Acknowledgments
This assignment is inspired from a homework assignment by Prof. Diane Litman. Data is from [Danescu-Niculescu-Mizil et al. 2013](https://aclanthology.org/P13-1025).
