---
layout: class
title: Homework 1 (CS 2731 Fall 2023)
---

# Homework 1: Vector space word similarity ([CS 2731 Fall 2023](https://michaelmilleryoder.github.io/cs2731_fall2023/))
**Due 2023-09-14, 11:59pm.** *Instructions last updated 2023-09-05.*

In this assignment, you'll build representations for documents and words based on the bag-of-words model. You'll implement 2 popular weighting schemes for these vectors: tf-idf and PPMI, both discussed in Chapter 6 of the [textbook](https://web.stanford.edu/~jurafsky/slp3/). Then you'll compare these weighting schemes on learning word similarity and apply one of them, PPMI, to examine social bias in an NLP corpus.

## Datasets and skeleton code
Here are the materials that you should download for this assignment:

* [Skeleton Python code](hw1/skeleton.py). You will need to have a Python environment with scipy and numpy packages. Some functions are stubs in the python code. You will need to fill them out.
* [CSV of the complete works of Shakespeare](hw1/shakespeare_plays.csv)
* [Vocab of the complete works of Shakespeare](hw1/vocab.txt)
* [List of all plays in the dataset](hw1/play_names.txt)
* [SNLI corpus](hw1/snli.csv)
	* This corpus is selections from SNLI, a corpus used for the NLP task of "natural language inference" (see [Bowman et al. 2015 dataset paper](https://aclanthology.org/D15-1075/)). Each line contains a sentence that is either a "premise" (an image caption) or a "hypothesis" produced by annotators to be in a certain logical relation with the associated premise (entailment, neutral, contradiction). You don't need to worry about these details, but the `sentenceID` column is a unique index for each sentence and `captionID` is an ID for all sentences associated with same caption/premise.
* [List of identity labels](hw1/identity_labels.txt) from [Rudinger et al. 2017](https://aclanthology.org/W17-1609/)

## Part 1: Vector spaces

### 1.1 Term-document matrix
Write code to compile a term-document matrix for Shakespeare&rsquo;s plays, following the description in the textbook:
<blockquote>
    <p>In a<span>&nbsp;</span><em>term-document matrix</em>, each row represents a word in the vocabulary and each column represents a document from some collection. The figure below shows a small selection from a term-document matrix showing the occurrence of four words in four plays by Shakespeare. Each cell in this matrix represents the number of times a particular word (defined by the row) occurs in a particular document (defined by the column). Thus<span>&nbsp;</span><strong>clown</strong><span>&nbsp;</span>appeared 117 times in <strong>Twelfth Night</strong></p>
</blockquote>

<table>
    <thead>
        <tr>
            <th>&nbsp;</th>
            <th>As You Like It</th>
            <th>Twelfth Night</th>
            <th>Julius Caesar</th>
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

#### Tasks for section 1.3
* Fill out the function stub `create_term_document_matrix`.

### 1.2 Term-Context Matrix

Instead of using a term-document matrix, a more common way of computing word similarity is by constructing a term-context matrix (also called a term-term or word-word matrix), where columns are labeled by words rather than documents. The dimensionality of this kind of a matrix is $$\vert V \vert$$ by $$\vert V \vert$$. Each cell represents how often the word in the row (the target word) co-occurs with the word in the column (the context) in a training corpus.

#### Tasks for section 1.2
* Implement the `create_term_context_matrix` function. This function specifies the size word window around the target word that you will use to gather its contexts. For instance, if you set that variable to be 4, then you will use 4 words to the left of the target word, and 4 words to its right for the context. In this case, the cell represents the number of times in Shakespeare’s plays the column word occurs in +/-4 word window around the row word.

### 1.3 Evaluating vector spaces

So far we have created 2 vector spaces for the words in Shakespeare, one with a dimension of $$D$$ and another of dimension $$\vert V \vert$$. Now we will try to evaluate how good our vector spaces are. We can do this with an intrinsic evaluation approach by seeing what words within the vocab are most similar to each other/are synonyms with each other and assessing if the output is reasonable. Implement the `rank_words` function which will take a target word index and return a list sorted from most similar to least similar using the cosine similarity metric. For the purposes of the assignment, let's just look at the top 10 words that are most similar to a target word between both the term-document matrix and the term-context matrix. Are those 10 words good synonyms? The skeleton code provides an example of using `rank_words` and looking at similar words using the word 'juliet'. 
One example won't be enough so pick out at least 5 more words from the vocab as you answer these questions.

#### Tasks for section 1.3
* Implement `rank_words`

*For the report:*
* In our term-document matrix, the rows are word vectors of $$D$$ dimensions. Do you think that’s enough to represent the meaning of words? 
* Which vector space (term-document or term-context) produce similar words that make more sense than the other and why do you think that is the case? 
* Consider any decisions you made in the prior sections when implementing your functions, such as whether you allowed a word to co-occur with itself. How might any decisions you make impact our results now?

### 1.4 Weighting terms with tf-idf and PPMI
Your term-context matrix contains the raw frequency of the co-occurrence of two words in each cell and your term-document matrix contains the raw frequency of words in each of the documents. Raw frequency turns out not to be the best way of measuring the association between words. There are several methods for weighting words so that we get better results. 


#### Tasks for section 1.4
* Take your term-document matrix and implement the weighting schemes <em>Term frequency inverse document frequency (tf-idf)</em> and <em>Positive pointwise mutual information</em> which are defined in Sections 6.5-6.6 of the textbook. These are the function stubs `create_tf_idf_matrix` and `create_ppmi_matrix`.

*For the report:*
* Redo the analysis in section 1.3 with ranked words and compare using tf-idf and PPMI with unweighted term-document and term-context matrices. 
* Discuss findings from comparing approaches. Do some approaches appear to work better than others, i.e produce better synonyms? Do any interesting patterns emerge? 
* How does weighting with tf-idf compare to using the unweighted term-document matrix? How does weighting with PPMI compare with using the unweighted term-context matrix? How does term-context/PPMI compare to term-document/TF-IDF? Include results and discussion.


## Part 2
In this part, you will measure associations between words in a commonly used NLP corpus, SNLI, and comment on the potential for encoding problematic social biases. There is no skeleton code for this section, but you can reuse code from Part 1.


### Tasks for Part 2
* First, write a loader for text from the SNLI corpus into a similar format as the Shakespeare corpus was loaded. You can use the `sentenceID` column as the document name, though this will not be as important since you'll only be building a term-context matrix. You'll still want to tokenize and lowercase the input as was done with the Shakespeare corpus. 

* Build a term-context matrix in a similar fashion as with the Shakespeare corpus and apply PPMI weighting. The context window can be your choice; you can also use the whole sentence as the context. If this matrix is too big or taking too long to calculate, filter to just words that occur over some frequency threshold in the entire corpus.

*For the report:*
* With that PPMI-weighted term-context matrix, find the vectors for identity labels in the provided list. Look at the top associated context words for identity labels of your choice. Do you see any that may reflect social stereotypes? It is helpful to compare the top PMI words for certain identity terms with other related ones (such as men compared with women). Discuss and provide selected results in the report.

* Qualitative analysis: Find specific examples from the dataset where an identity label occurs with a top-associated term that shows some social bias or does not. Look at 1-2 examples for at least 4 different identity labels.  Provide selected results and discuss findings in the report. Do you see evidence for representational harms learned by a bag-of-words model of this SNLI corpus? If so, which type do you see?

* Here is a description of *representational harms* in machine learning from [Blodgett et al. 2020](https://aclanthology.org/2020.acl-main.485/).
<blockquote>
Representational harms arise when a system (e.g., a search engine) represents some social groups in a less favorable light than others, demeans them, or fails to recognize their existence altogether.
</blockquote>
Types of representational harms from [Blodgett et al. 2020](https://aclanthology.org/2020.acl-main.485/) include:
<blockquote>
1. Stereotyping that propagates negative generalizations about particular social groups.   
2. Differences in system performance for different social groups, language that misrepresents the distribution of different social groups in the population, or language that is denigrating to particular social groups.
</blockquote>


## Deliverables
* Your implementations for the functions in the skeleton code `hw4_skeleton_{your pitt id}.py`. You are welcome to put code for Part 2 in the same or a different file. If it's different, please where it is in the README.txt.
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
This assignment is adapted from Prof. Diane Litman and Prof. Mark Yatskar, as well from [Rudinger et al. 2017](https://aclanthology.org/W17-1609/).
