---
layout: class
title: Final Project (CS 2731 Fall 2023)
---

# Final Project ([CS 2731 Fall 2023](https://michaelmilleryoder.github.io/cs2731_fall2023/))
A major component of this course is a hands-on final project guided by students' own interests. In this project, students will demonstrate an ability to summarize and implement current approaches and challenges in a subfield of NLP and make a contribution to this NLP research area.

## Groups
Projects will be done by 1-3 students, usually 2 students. Groups will be assigned by the instructor and TA based on interests and skills, and group preferences from students, in a survey.

## Deliverables
1. **Project survey**. This survey asks about NLP research areas of interest, skills, project ideas, and any group preferences. The survey will be available as a Google Form. It will be used by the instructor and TA to match groups with similar project interests and complimentary abilities.
2. **Project area and type of contribution**. You will provide the type of contribution you are interested in pursuing within a specific research area, as well as any inkling of idea you have, in a form. The instructor and TA will provide some feedback and guidance on this direction in office hours.
3. **Project proposal and literature review**. This proposal will be a report with answers to the following questions:
	1. What type of contribution are you making?
	2. What is the problem or task you are focusing on?
	3. What is the nature of your contribution?
	4. How does your contribution build on or extend prior work? This literature review will be of papers relevant to your project area. It will group and summarize relevant papers into types of tasks, datasets, and/or approaches.
	5. What data are you using (or contributing)?
	6. What algorithm or approach are you taking to address the task?
	7. How are you evaluating your contribution? What performance metrics are you going to use?
	8. What kinds of ethical issues may be raised by your model or data?
It is recommended to start on the literature review early on, since existing work will inform your specific direction (somebody may have already tried your idea!). The instructor and TA will provide feedback on this proposal and a meeting in office hours if needed. There is no required length or format for this report, but you could use the ACL format that the final report will be formatted in.
4. **Project proposal presentation**. Groups will make a brief presentation to the class outlining their proposed project, with Q&A and opportunities for feedback from other students. This presentation should also mention any changes planned based on proposal feedback from the instructor and TA.
5. **Basic working system**. A brief (1-2 page) progress report of a basic working system. Not everything needs to be done or fully functional, but there needs to be some sort of basic functionality. This report should be in the ACL format that the final report will be in.
6. **Final presentation**. Groups will present their finished work to the group, with Q&A and feedback opportunities from students.
7. **Final report and code**. At the end of the course, groups will provide a written report of their project. This report will be in the ACL format found [here](https://github.com/acl-org/acl-style-files) (Overleaf template [here](https://www.overleaf.com/project/5f64f1fb97c4c50001b60549)). Ideally this would be of a quality and structure that could be submitted to an NLP workshop or conference.

## Types of contributions
Your goal is to make a contribution, even a small one, to NLP research or practice. You can select from the following types of contributions, combine multiple of them, or define a different type of contribution with instructor approval. Example project ideas and projects are provided (with a significant bias toward computational social science and hate speech, the instructor's research area). Groups are also encouraged to come up with their own ideas! Projects can be related to students' research, but should not be projects for other classes.

### 1. New dataset, annotations, or analysis of existing datasets
Data is at the heart of machine learning and NLP systems; it enables further modeling and encapsulates what NLP systems "know".

#### Example project ideas
* Hate speech is often expressed in a "joking" manner, yet hate speech classifiers struggle to identify hate speech in irony and humor. Build a dataset of hate speech in jokes ("light talk") to aid future NLP classifiers. This dataset could be collected from sites that are known for both hateful content and a "humorous" tone, and portions could be annotated for hate speech and/or types of humor. This could be an expansion of prior work that provides a dataset of offense in humor: [https://competitions.codalab.org/competitions/27446](https://competitions.codalab.org/competitions/27446) 
* Hate speech is culturally specific, yet the majority of NLP work focuses on English in North American and European contexts. A quantitative analysis of different features of datasets annotated for hate speech in multiple languages and from multiple cultural contexts would illuminate global similarities and culturally specific contexts.
* Speech acts are the "actions" that speakers intend with utterances (such as asking a question or giving an explanation). Emojis may help automated systems determine speech acts. Build a dataset of utterances with and without emojis and annotate these for speech acts. Build a simple classifier with interpretable features and see if emojis are informative.
* Build a dataset of text from different personas from fiction roleplaying sites ("language cosplaying" in China). This could be useful for dialogue systems that adopt personas, or for story generation.

#### Example projects
* [Newell et al. 2017](https://aclanthology.org/I17-1076.pdf): "Verifiability" of claims made in news. New datasets often accompany the introduction of a new NLP task, which could be a previously unstudied phenomenon like verifiability in this one.

### 2. New approach or application 
This is perhaps the most common sort of NLP research contribution, in which a new method or algorithm for approaching a task (which could be a new task) is presented. Applying an existing method in a new context or task (as might be necessary in an industry setting) would also fit within this contribution.

#### Example project ideas
New tasks and applications:
* Automatically identify the targeted group of hate speech in English from individual posts. This may seem "easy" by simply recognizing identity terms in the text, but there are many difficult cases where multiple identities are mentioned, or references to groups are ambiguous or indirect. Hate speech annotated for targeted identities would be provided by the instructor and could act as training data. This classifier could be applied to audit the distribution of targeted identities in commonly used hate speech datasets.
* New identity terms are commonly developed in online communities, some of them hateful. Develop methods to find in-group hate jargon and identity terms.
* Hate speech identification without the text: Identify the discourse contexts in which hate speech is likely to occur, without allowing classifiers to look at the exact text of the hate speech.
* Stancetaking, a concept from sociolinguistics, is when sepakers take an evaluative position toward the concept ("No, I actually don't like Taylor Swift's music that much, but she's great"). Develop automated methods for identifying the "stance object", who the speaker is evaluating, likely from Reddit data that would be provided by the instructor.
* From a set of descriptions of characters, develop a classifier for which ones will generate the most fanfiction? This could be a lens into online community and media norms.
* Examine the framing of different entities in police Facebook posts from the [Plain View Project](https://www.plainviewproject.org/)

Existing tasks (some ideas are pulled from Graham Neubig's Advanced NLP class):
* Lexicons are often used to identify emotional language or other concepts text analysts may be interested in measuring in large corpora. Develop and evaluate approaches for expanding lexicons to specific contexts. This could be applied to expand lists of identity terms in a variety of online communities, with data supplied by the instructor.
* Any of the [SemEval 2021 tasks](https://semeval.github.io/SemEval2021/tasks)
* [X-FACTR multilingual knowledge probing in QA](https://x-factr.github.io/)
* [GoEmotions Fine-grained Emotion Detection Dataset](https://github.com/google-research/google-research/tree/master/goemotions)
* [SciREX Scientific Information Extraction](https://github.com/allenai/SciREX)
* [Subjective Intent Classification in Discourse](https://github.com/elisaF/subjective_discourse)
* [Very Low Resource machine translation](http://statmt.org/wmt21/unsup_and_very_low_res.html)
* Predict the points at which speakers switch languages when code-switching
* Sign language translation
* Develop best approaches for training hate speech classifiers that generalize across target identities. Data would be provided by the instructor
* Develop new approaches for hate speech detection by comparing with knowledge bases or pretrained models of stereotypes from a stereotype dataset


### 3. New evaluation
Good automated evaluations of machine learning systems are hard to come by. Ideally they correlate with human judgments of quality and capture key elements of the phenomenon being modeled while also being robust to adversarial attacks. This may be a difficult contribution to make without being very familiar with a research area, but there is often a need for new evaluations for specific NLP applications.

#### Example projects
* [Moosavi and Strube 2016](https://aclanthology.org/P16-1060/). New coreference resolution metric.
* [Freitag et al. 2022](https://aclanthology.org/2022.wmt-1.2.pdf). Neural evaluation metrics for machine translation.

### 4. New survey or position paper
Surveys are especially needed for new, emerging research areas. All projects will require a literature review, but a survey paper would be both broader and go much more in depth. It would summarize key approaches and key challenges and present lines for future work. Some sort of implementation is necessary for this type of contribution as well, such as applying multiple established methods to a new dataset or in a new context to show challenges that need to be addressed. Position papers argue for a certain viewpoint or shortcoming of existing approaches, e.g. arguing for the utility of techniques from a discipline outside NLP in NLP tasks.

#### Example project ideas
* Survey how NLP is used and applied in other fields. What has ben our most useful contributions to scholars in the social sciences, physical sciences, or humanities? This survey would assemble papers across disciplines for mentions of NLP and summarize what is most useful, what is lacking, and what approaches from NLP could be helpful to others.
* Computational social science using NLP generally relies on data from online communities. But this is missing non-online interactions and the practices of those who are not active online. Survey datasets and approaches that use quantitative and computational techniques on recordings of offline linguistic interaction.
* A growing area of research in computational social science aims to capture the framing and portrayal of entities across large text corpora (such as in [news media](https://ojs.aaai.org/index.php/ICWSM/article/download/3358/3226/)). Survey existing approaches and challenges.


## NLP research areas
Early on, groups will select an NLP research area to focus their project on (or multiple areas, if applicable). Here is a list of NLP research areas in alphabetical order, drawn from the [ACL Rolling Review list](https://aclrollingreview.org/cfp). You can also pursue a project in a different area with instructor permission.

* *Computational Social Science and Cultural Analytics*. Using NLP to study societies and cultural texts, as well as developing tools that process language in social context. This is the instructor's main research area and many of the example project ideas focusing on hate speech would fit within this area.
* *Dialogue and Interactive Systems*. NLP systems that interact conversationally, as well as systems that analyze human conversation.
* *Discourse and Pragmatics*. Discourse here refers to linguistic structure beyond the a sentence level. This includes predicting the coherence of different sentences together (discourse coherence) and the relations between sentences (discourse relations). It also includes parsing rhetorical structures of texts such as essays.
* *Efficient/Low-Resource Methods for NLP*. This includes computational and energy efficiency. How do we get similar performance with models with fewer parameters and less demanding computational requirements?
* *Ethics, Bias, and Fairness*. There's a lot of focus on this area with LLMs right now.
* *Generation*. This includes language and code generation, as well as interesting applications like story and narrative generation.
* *Information Extraction*. This includes extracting and linking events and particular types of entities, timelines, and locations.
* *Information Retrieval and Text Mining*. This includes searching for particular kinds of information from large text corpora.
* *Interpretability and Analysis of Models for NLP*. Many NLP and ML models are quite uninterpretable; this area addresses this.
* *Linguistic theories, Cognitive Modeling and Psycholinguistics*. This area includes work that applies or evaluates linguistic and cognitive theories of language with computational models.
* *Machine Learning for NLP*. This area includes core ML improvements for NLP, as well as applying new ML methods to language.
* *Machine Translation*. Automatic translation between languages.
* *Multilinguality and Language Diversity*. Too much NLP work is solely in English or other "high-resource" languages. This area addresses this problem and also handles language diversity such as code-switching.
* *Multimodality and Language Grounding to Vision, Robotics and Beyond*. Language is often used by humans in tandem with vision and motion. NLP models within this area take this into account.
* *NLP Applications*. This area would include applications such as educational applications (like automated essay grading) or in areas such as human rights (see aporaphobia paper) or industry settings.
* *Phonology, Morphology and Word Segmentation*. This area includes linguistic areas that study how sounds and parts of words fit together to produce meaning. Computational approaches from NLP can extract and model this subword information at scale.
* *Question Answering*. Automatically answering questions posed by humans.
* *Semantics: Lexical*. Approaches that model word meanings and semantic relationships between words.
* *Semantics: Sentence-level Semantics, Textual Inference and Other areas*. This area includes tasks of natural language inference and coreference resolution.
* *Sentiment Analysis, Stylistic Analysis, and Argument Mining*. Extracting and analyzing sentiments (pro vs con), styles, and arguments.
* *Speech recognition, text-to-speech and spoken language understanding*.
* *Summarization*. Automatic approaches to summarizing texts.
* *Syntax: Tagging, Chunking and Parsing*. Computational approaches to extracting grammatical structure from text, including part-of-speech tagging, dependency parsing, and constituency parsing.
