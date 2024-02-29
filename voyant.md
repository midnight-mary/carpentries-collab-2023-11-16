---
title: "Exploring Text-Based Corpora with Voyant"
teaching: 35
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is Voyant and what is it used for?
- What are the principles underpinning its dashboard tools?
- What kinds of insights do they yield?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Define key terms relating to Natural Language Processing
- Load data into Voyant and conduct inductive analysis
- Identify affordances and limitations of a frequency-based approach to corpus analysis

::::::::::::::::::::::::::::::::::::::::::::::::
## Introduction to Voyant

[Voyant](https://voyant-tools.org/) is a simple, powerful and user-friendly open-source reading and analysis environment for digital texts. It was created by Stéfan Sinclair and is now maintaned by Geoffrey Rockwell, Andrew MacDonald and Cecily Raynor at the Universities of McGill and Alberta in Canada. It is browser-based and allows you to upload documents or copy and paste text directly into the interface, which Voyant then automatically analyses according to some core Natural Language Processing (NLP) principles.

Voyant is a useful tool for those new to NLP because its dashboard provides an instant and customisable, synchronic overview of many facets of the corpus uploaded while keeping the workings 'under the hood'. This allows users to explore the linguistic features of their corpus intuitively, before getting to grips with the linear, incremental workflow of NLP libraries such as the Natural Language Toolkit (NLTK), spaCy and Flair. 

::::::: callout

Voyant **does not require any prior programming knowledge** and enables **inductive, corpus-driven** observations to be made with relative ease. This allows you to **refine your research questions** in response to the data you are working with, and then move on to using other tools in a more targeted way.

::::::::
## Core NLP Terminology

Before we start using Voyant to explore our text corpora in more detail, it is useful to define some core NLP concepts so that you can understand what Voyant is looking for as it reads text data.

First of all, Voyant needs to parse the text as a sequence of characters (or **string**) and identify meaningful linguistic units such as words, numbers and punctuation. 

- A **token** is a defined unit within a string, such as an individual appearance of a word or number, usually separated from other tokens by whitespace.
- A **type**, on the other hand, is a unique word form, which may appear many times in a corpus.
- A **lemma** is the root form of a derived (inflected) word, e.g. 'music' is the lemma of the types 'musically', 'musician', 'musicking', etc.
- A **hapax legomena** (or simply **hapax**) is a type that appears only once in a corpus.
- A **concordance** is a generated list of all tokens that appear in a digital corpus.

The relationship between tokens and types (or **type-token ratio**), i.e. how many unique word forms there are in a corpus versus how many times they are used, is a measure of the **lexical diversity** of the corpus. 

Besides parsing a corpus for tokens and types, Voyant also analyses the relationships between tokens and their neighbours, in line with the importance placed on knowing the company words keep in computational linguistics, discussed in the [last episode](introduction.md).

- An **n-gram** is a contiguous or consecutive sequence of tokens in a text. For example a **bigram** is a pair of consecutive written units, i.e. characters, syllables or words; a trigram is a sequence of three consecutive written units, and so on. Any number of consecutive units can be specified for an n-gram and it functions somewhat like a sample-rate for extracting information from the text that could be important for predicting aspects of meaning or function.
- A **collocation** is typically a bigram, often at word level, which occurs in a text at a rate greater than chance. For example, type-pairs like 'red wine' and 'string quartet' are collocations in English.

The original and most common application of automated text analysis uses computers to count how often certain words occur in a given text. The analytical strategy employed in a **frequency-based approach** is relatively simple: count the number of occurrences of a specific word token and then normalise this according to how many words there are in the text overall to obtain **relative term frequency**. 

Despite its simplicity, this approach is extremely powerful and versatile. Besides relative term frequency, another common technique used for making frequency counts reflect data more meaningfully is **term frequency-inverse document frequency (TF-IDF)**, especially if working with corpora across multiple documents. This helps to minimise the weighting of frequently occurring but perhaps less significant terms (such as 'the', 'a', etc.) while making less frequent terms have a higher impact. 

::::::: callout

Frequency-based text analysis is often traced back to Father Roberto Busa, a Jesuit Priest who worked with IBM in the 1940s to manually index 11 million medieval Latin words from the writings of St. Thomas Aquinas, count each appearance of the word 'in' and look at its collocations in order to explore the concept of 'presence' in his work. This somewhat quaint story has come to be venerated as the origin myth of the field of humanities computing as a whole, and has more recently been the subject of critique.^[Arun, Jacob. 2021. 'Punching Holes in the International Busa Machine Narrative'. In Kim, Dorothy and Coh, Adeline, Eds. *Alternative Historiographies of the Digital Humanities*. Punctum: 121–139]
:::::::::::
With these core principles in mind, we can now have a go at using Voyant to explore the Boomkat corpus.

:::::::::::::: instructor

 Check for questions before launching the exercise

::::::::::::::::::::::

:::::::::: discussion
In pairs or groups of three, choose one of the subgenre datasets from the ['For Voyant'](https://drive.google.com/drive/folders/1sY2irnuaS4tM9i7PxG3lOz_46E1XYDHb?usp=sharing) folder which you should already have downloaded to your computer. Then, go to the [Voyant website](https://voyant-tools.org/) and click the 'Upload' button to load the data to Voyant's server. This may take a few moments. 

Once the data has loaded, take a few minutes to look around the various panes of the Dashboard and think about:

* What do the individual panels do? Can you describe it using the NLP terms we defined earlier?
* Which tool or finding grabs your attention? Why?
* Are there any problems with how the data appears that prevent a more meaningful analysis?
* Are there any features that you do not understand?

Discuss these with your group and jot down some observations to share with everyone else.
::::::::::
## Fine-Tuning Parameters for Corpus Sensitivity

From this first pass at our corpus, we can see that Voyant has recognised punctuation mark tokens and omitted them from frequency counts, the word cloud, and other analyses. This is useful for readability and can almost go unnoticed. However, it should be remembered that **punctuation marks are tokens** and the **decision to remove** them is an **intentional** one, which other NLP libraries do not perform automatically.

Because Voyant has so far only performed a raw frequency count of the corpus, the most common terms that Voyant has identified are, perhaps unsurprisingly, quite generic (articles, prepositions, etc.). They do not give a sense of what is distinctive about corpus because it could be assumed that a majority of texts would also make regular use of these types of words. Of course, depending on your research question, this could be precisely the type of information you are after - Father Busa's project, after all, was all about the seemingly generic word 'in'. 

If you already have some idea about the kind of linguistic devices you are looking for, either because of your initial research question or through what you have observed from this initial analysis, it is possible to get Voyant to filter out certain terms so that you can fine-tune your findings. This involves creating a list of stopwords, which is a common technique in corpus linguistics and NLP more generally.

# Stopwords 

A **stopword** is a word (or any token) that is automatically omitted from a computer-generated concordance. Many NLP libraries have automatic lists of stopwords specific to individual languages, and these can often be edited to suit your specific needs, or you can create your own. 

In Voyant, you can inspect the stopword lists by clicking the 'settings' icon on the top right corner of the 'Terms' tool. As can be seen, there are lists for the different languages that Voyant supports, as well as an 'auto-detect' list. It can be assumed that the removal of punctuation marks from Voyant's reading of our corpus is a feature of its 'auto-detect' stopword list.

# Sentiment 

::::::::: callout

Remember that data cleaning is an iterative process, not simply an initial step. We have been working with a dataset that has already been converted from .csv to .xlsm, UTF-8 encoded and which contains one uniform data type within it. Consideration of the type of data you are working with and how it is presented for analysis is important in pre-processing but does not end there.

Relatedly, stopword lists and any other filters should be thought through carefully in order to remain sensitive to the discursive priorities of the types of texts being analysed while also being used to streamline the dataset and remove 'noise'. This, too, should be an iterative process and can involve trial and error as you get a feel for the shape and contents of your corpus.
::::::::::::::


::::: keypoints  

1. The Voyant website allows you to dive into your corpus right away by uploading a document (or several) to its server.  
2. Most of Voyant's dashboard tools such as Cirrus, Termsberry and Contexts, rely on token frequency counts and collocations.  
3. These types of tools can yield insights into the lexical diversity of the corpus, which terms in a given corpus are most or least prominent, and the other words with which they frequently appear. This can highlight patterns or trends that can then be further analysed with other tools.

::::: 

