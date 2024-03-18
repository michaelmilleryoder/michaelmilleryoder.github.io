---
layout: class
title: Homework 4 (CS 2731 Spring 2024)
---

# Homework 4: Sequence labeling ([CS 2731 Spring 2024](https://michaelmilleryoder.github.io/cs2731_spring2024/))
**Due 2024-03-25, 11:59pm**. *Instructions last updated 2024-03-18.*

In this assignment, you will manually decode the highest-probability sequence of part-of-speech tags from a trained HMM using the Viterbi algorithm. You will also fine-tune BERT-based models for part-of-speech (POS) tagging for English and Norwegian.

The learning goals of this assignment are to:
* Demonstrate how the Viterbi algorithm takes into account emission and transmission probabilities to find the highest-probability sequence of hidden states in an HMM
* Fine-tune a transformer-based model on sequence labeling
* Find and use pretrained models from Hugging Face

# 1. POS tagging with an HMM
Consider a Hidden Markov Model with the following parameters:
postags = {NOUN, AUX, VERB}, words = {'Patrick', 'Cherry', 'can', 'will', 'see', 'spot'}

Initial probabilities:

&nbsp; | $$\pi$$
--|--------
NOUN|0.6
AUX|0.2
VERB|0.2

Transition probabilities: 
The format is P(column\_tag \| row\_tag), e.g. P(AUX \| NOUN) = 0.3.

 &nbsp;| NOUN | AUX | VERB
--|---|---|--
NOUN|0.2|0.3|0.5
AUX|0.4|0.1|0.5
VERB|0.8|0.1|0.1

Emission probabilities:

 &nbsp;| Patrick | Cherry | can | will | see | spot
--|---|---|--|--|--|--
NOUN|0.3|0.2|0.1|0.1|0.1|0.2
AUX|0|0|0.4|0.6|0|0
VERB|0|0|0.1|0.2|0.5|0.2

See chapter 8 in the Jurafsky & Martin textbook for details on the Viterbi algorithm.
Using the Viterbi algorithm and the given HMM, find the most likely tag sequence for the following 2 sentences.
1. “Patrick can see Cherry”
1. “will Cherry spot Patrick”

To get you started on the Viterbi tables, here are the first 2 columns for the first sentence with backtraces.

POS state | Patrick | can | see| Cherry
----|---|----|---|---
NOUN|0.18|0.0036<br>backtrace:NOUN| |
AUX|0|0.0216<br>backtrace:NOUN| |
VERB|0|0.009<br>backtrace:NOUN| |


## Deliverables for part 1
In your report, show your work for calculating the Viterbi tables or lattices for both example sentences. This should include backtraces and calculations for probabilities.
Report the most likely tag sequences for these 2 sentences.


# 2. Fine-tune BERT-based models for POS tagging
In this section, you will fine-tune pretrained BERT-based models for part-of-speech tagging in English and Norwegian.

Copy this [skeleton Colab notebook](https://colab.research.google.com/drive/1X0wmJbH-ySZg5DASEDGTV_SrkdzMXq89?usp=sharing), run the cells, and fill in the places that are specified.

## Deliverables for part 2
In your report, include:
1. The 5 most frequent POS tags for English and Norwegian datasets (specified in the notebook) and how many tokens are tagged with each
1. For each of the 5 most frequent POS tags for English and Norwegian datasets, provide the 5 most frequent word types annotated with that tag in the training data
1. The names of the pretrained BERT-based models you chose for both English and Norwegian
1. A brief discussion of any choices you made about hyperparameters in training
1. *(Optionally, for extra credit)* A description of changes you made or different pretrained models you tried and what accuracy you obtained on the dev set. 1 point of extra credit will be given if any changes result in an improved accuracy on the dev set.
1. Accuracy of the fine-tuned models on the test set for both English and Norwegian
1. POS tags predicted for the words of a sentence of your choice in both English and Norwegian
4. A link to your copied and filled out Colab notebook

## Submission
Please submit the following items on Canvas:

* Your report with results and answers to questions in Part 1 and Part 2, named `report_{your pitt email id}_hw4.pdf`. No need to include @pitt.edu, just use the email ID before that part. For example: `report_mmy29_hw4.pdf`.
* A `README.txt` file explaining
	* any additional resources, references, or web pages you've consulted
	* any person with whom you've discussed the assignment and describe the nature of your discussions
	* any generative AI tool used, and how it was used
	* any unresolved issues or problems

## Grading
This homework assignment is worth 56 points.
See rubric on Canvas.


## Acknowledgments
Part 1 of this assignment is based on homework assignments by Prof. Hyeju Jang and Prof. Diane Litman. Part 2 is adapted from Jacob Eisenstein and Prof. Yulia Tsvetkov.
