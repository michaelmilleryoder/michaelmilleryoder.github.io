---
layout: class
title: Homework 1 (CS 2731 Fall 2023)
---

# Homework 1: Vector space word similarity ([CS 2731 Fall 2023](https://michaelmilleryoder.github.io/cs2731_fall2023/))
In this assignment, you'll build representations for documents and words based on the bag-of-words model. You'll implement 2 popular weighting schemes for these vectors: tf-idf and PPMI, both discussed in Chapter 6 of the [textbook](https://web.stanford.edu/~jurafsky/slp3/). Then, you'll compare these weighting schemes on learning word similarity and apply one of them, PPMI, to examine social bias in an NLP corpus.

## Datasets and skeleton code
Here are the materials that you should download for this assignment:

* [Skeleton Python code](hw1/skeleton.py)
* [CSV of the complete works of Shakespeare](hw1/shakespeare_plays.csv)
* [Vocab of the complete works of Shakespeare](hw1/vocab.txt)
* [List of all plays in the dataset](hw1/play_names.txt)
* [SNLI corpus](hw1/snli_1.0.zip)
	* Use the training data CSV or JSON lines file (`snli_1.0_train.jsonl`) in the SNLI corpus. The sentence1 column with premise that was supplied to annotators, and the sentence2 column is the hypotheses that annotators came up with. See other details about the corpus format in the README supplied with SNLI. [POSSIBLY ARRANGE/COMBINE SENTENCES]
* [List of identity labels](hw1/identity_labels.txt) from Rudinger et al. 2017

## Deliverables
* Your implementations for the functions in the skeleton code `hw4_skeleton_{your pitt id}.py`
	* You are welcome to import any packages you need but please don't modify the function that has already been implemented
* Your report that illustrates your experiment named `report_{your pitt id}.pdf`
	* Should have any discussion/reasoning below each result
* A README.txt file explaining
	* how to run your code
	* the computing environment you used; what programming language you used and the major and minor version of that language; what packages did you use so that we can replicate your experiments.
	* any additional resources, references, or web pages you've consulted
	* any person with whom you've discussed the assignment and describe the nature of your discussions
	* any generative AI tool used, and how it was used
	* any unresolved issues or problems

[COMBINE with "your tasks in part I"]

## Part 1: Vector spaces
Projects will be done in groups of 2-4 students. Groups will be assigned by the instructor and TA based on interests and skills, and group preferences from students, in a survey.

### 1.1 Term-document matrix
You will write code to compile a term-document matrix for Shakespeare&rsquo;s plays, following the description in the textbook:
<blockquote>
    <p>In a<span>&nbsp;</span><em>term-document matrix</em>, each row represents a word in the vocabulary and each column represents a document from some collection. The figure below shows a small selection from a term-document matrix showing the occurrence of four words in four plays by Shakespeare. Each cell in this matrix represents the number of times a particular word (defined by the row) occurs in a particular document (defined by the column). Thus<span>&nbsp;</span><strong>clown</strong><span>&nbsp;</span>appeared 117 times in **Twelfth Night**</p>
</blockquote>

<table>
    <thead>
        <tr>
            <th>&nbsp;</th>
            <th>As You Like It</th>
            <th>Twelfth Night</th>
            <th>Julias Caesar</th>
            <th>Henry V</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>battle</strong></td>
            <td>1</td>
            <td>1</td>
            <td>8</td>
            <td>15</td>
        </tr>
        <tr>
            <td><strong>soldier</strong></td>
            <td>2</td>
            <td>2</td>
            <td>12</td>
            <td>36</td>
        </tr>
        <tr>
            <td><strong>fool</strong></td>
            <td>37</td>
            <td>58</td>
            <td>1</td>
            <td>5</td>
        </tr>
        <tr>
            <td><strong>clown</strong></td>
            <td>5</td>
            <td>117</td>
            <td>0</td>
            <td>0</td>
        </tr>
    </tbody>
</table>

The dimensions of your term-document matrix will be the number of documents $$D$$ (in this case, the number of Shakespeare’s plays that we give you in the corpus) by the number of unique word types $$\vert V \vert$$ in that collection. The columns represent the documents, and the rows represent the words, and each cell represents the frequency of that word in that document.

In your code you will write a function to `create_term_document_matrix`.

### 1.2 Term-Context Matrix

Instead of using a term-document matrix, a more common way of computing word similarity is by constructing a term-context matrix (also called a word-word matrix), where columns are labeled by words rather than documents. The dimensionality of this kind of a matrix is $|V|$ by $|V|$. Each cell represents how often the word in the row (the target word) co-occurs with the word in the column (the context) in a training corpus.

For this part of the assignment, you should write the `create_term_context_matrix` function. This function specifies the size word window around the target word that you will use to gather its contexts. For instance, if you set that variable to be 4, then you will use 4 words to the left of the target word, and 4 words to its right for the context. In this case, the cell represents the number of times in Shakespeare’s plays the column word occurs in +/-4 word window around the row word.

Something to report: Can a word co-occur with itself in a Term-Context Matrix? The matrix will have a cell for where the target word and the context word aligns for example, position (1,1). Will this cell always stay zero? You will have to make this decision and discuss in the report, with text examples, when it makes sense for a word to co-occur with itself and when it does not?

### 1.3 Evaluating vector spaces

So far we have created 2 vector spaces for the words in Shakespeare, one with a dimension of $D$ and another of dimension $|V|$. Now we will try to evaluate how good our vector spaces are. We can do this with an intrinsic evaluation approach by seeing what words within the vocab are most similar to each other/are synonyms with each other and assessing if the output is reasonable. Implement the `rank_words` function which will take a target word index and return a list sorted from most similar to least similar using the cosine similarity metric. For the purposes of the assignment, let's just look at the top 10 words that are most similar to a target word between both the term-document matrix and the term-context matrix. Are those 10 words good synonyms? The skeleton code provides an example of using `rank_words` and looking at similar words using the word 'juliet', one example won't be enough so pick out at least 5 more words from the vocab as you answer these questions.

In our term-document matrix, the rows are word vectors of $D$ dimensions. Do you think that’s enough to represent the meaning of words? Which vector space (term-document or term-context) produce similar words that make more sense than the other and why do you think that is the case? Consider the decisions you made in the prior sections when implementing your functions. How do you think those decisions are impacting our results now?

### 1.4 Weighting terms with tf-idf and PPMI
Your term-context matrix contains the raw frequency of the co-occurrence of two words in each cell and your term-document matrix contains the raw frequency of words in each of the documents. Raw frequency turns out not to be the best way of measuring the association between words. There are several methods for weighting words so that we get better results. Take your term-document matrix and implement the weighting scheme <em>Term frequency inverse document frequency (tf-idf)</em> and <em>Positive pointwise mutual information</em> which are defined in Chapter 6 of the textbook [WHICH SECTIONS?].

You can now redo the analyses in Section 1.3 and discuss the impact of weighting terms in the matrix.

### 1.5 Your Tasks in Part 1
#### 1.5.1 Implementing functions

All of the following are function stubs in the python code. You just need to fill them out.

Create matrices:

fill out `create_term_document_matrix`
fill out `create_term_context_matrix `
fill out `create_tf_idf_matrix       `
fill out `create_ppmi_matrix       `

Do some ranking:

fill out `rank_words`

#### 1.5.2 Report

In the ranking tasks, play with different vector representations. Does one appear to work better than another, i.e produce better synonyms? Do any interesting patterns emerge? Is weighting with PPMI better than not weighting? How do term-context/PPMI compare to term-document/TF-IDF? Include results and discussion in your report.

## Part 2
In this part, you will measure associations between words in a commonly used NLP corpus, SNLI, and comment on the potential for encoding problematic social biases.

First, load in the SNLI corpus into a similar text format as the Shakespeare corpus. [ISSUES with HYPOTHESIS vs PREMISE, POSSIBLE PREPROCESSING ISSUES]. Then, compute PPMI between the identity labels in the provided list and all other words in the SNLI training corpus. Look at the top associated words for identity labels of your choice. Do you see any that may reflect social stereotypes? It is helpful to compare the top PMI words for certain identity terms with other related ones (such as men compared with women). Note that some terms in the list do not occur in the data [SHOULD DROP THEM THEN].

Qualitative analysis: Find specific examples from the dataset where an identity label occurs with a top-associated term that shows some social bias or does not. Look at 1-2 examples for at least 5 different identity labels.

Include each of these analysis in the report for this assignment.

## Acknowledgments
This assignment is adapted from Prof. Diane Litman and Prof. Mark Yatskar, as well from Rudinger et al. 2017.
