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
Briefly comment on if any weights shifted from positive to negative and why this was the case.

## Part 2: Implement a program for text classification

## Dataset
Here are the materials that you should download for this assignment:

* [Skeleton Python code](hw1/skeleton.py). You will need to have a Python environment with scipy and numpy packages. Some functions are stubs in the python code. You will need to fill them out.
* [CSV of the complete works of Shakespeare](hw1/shakespeare_plays.csv)
* [Vocab of the complete works of Shakespeare](hw1/vocab.txt)
* [List of all plays in the dataset](hw1/play_names.txt)
* [SNLI corpus](hw1/snli.csv)
	* This corpus is selections from SNLI, a corpus used for the NLP task of "natural language inference" (see [Bowman et al. 2015 dataset paper](https://aclanthology.org/D15-1075/)). Each line contains a sentence that is either a "premise" (an image caption) or a "hypothesis" produced by annotators to be in a certain logical relation with the associated premise (entailment, neutral, contradiction). You don't need to worry about these details, but the `sentenceID` column is a unique index for each sentence and `captionID` is an ID for all sentences associated with same caption/premise.
* [List of identity labels](hw1/identity_labels.txt) from [Rudinger et al. 2017](https://aclanthology.org/W17-1609/)


## Deliverables
* Your implementations for the functions in the skeleton code `hw1_skeleton_{your pitt email id}.py`. You are welcome to put code for Part 2 in the same or a different file. If it's different, please where it is in the README.txt.
	* You are welcome to import any packages you need but please don't modify the function that has already been implemented. 
* Your report with results and answers to questions in Part 1 and Part 2, named `report_{your pitt id}.pdf`. 
* A README.txt file explaining
	* how to run your code
	* the computing environment you used; what programming language you used and the major and minor version of that language; what packages did you use in case we replicate your experiments (a `requirements.txt` file for setting up the environment may be useful if there are many packages).
	* any additional resources, references, or web pages you've consulted
	* any person with whom you've discussed the assignment and describe the nature of your discussions
	* any generative AI tool used, and how it was used
	* any unresolved issues or problems

Please submit all of this material on Canvas. We will grade your report and attempt to run your code.

## Acknowledgments
This assignment is inspired from a homework assignment by Prof. Diane Litman. Data is from [paper link]().
