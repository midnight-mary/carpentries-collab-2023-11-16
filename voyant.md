---
title: "Exploring Text-Based Corpora with Voyant"
teaching: 0
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do I start using Voyant?
- What are the principles underpinning its dashboard tools?
- What kinds of insights do they yield?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Define key terms relating to textual analysis
- Load data into Voyant and conduct inductive analysis
- Identify affordances and limitations of a frequency-based approach to corpus analysis

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction to Voyant

[Voyant](https://voyant-tools.org/) is a simple, powerful and user-friendly open-source reading and analysis environment for digital texts founded by Stéfan Sinclair and now maintaned by Geoffrey Rockwell, Andrew MacDonald and Cecily Raynor at the Universities of McGill and Alberta in Canada. It is browser-based and allows you to upload documents or copy and paste text directly into the interface, which Voyant then automatically analyses according to some core Natural Language Processing (NLP) principles.

Voyant is a useful tool for those new to NLP because its 'Dashboard' landing site provides an instant, synchronic and customisable overview of many facets of the corpus uploaded while keeping the workings 'under the hood'. This allows you to dive straight into exploring the linguistic features of your corpus intuitively, without getting bogged down in the linear, incremental coding workflow of NLP libraries such as the Natural Language Toolkit, spaCy and Flair. 

::::::: callout
Voyant **does not require any prior programming knowledge** and enables **inductive, corpus-driven** observations to be made with relative ease. This allows you to **refine your research questions** in response to the data you are working with, and then move on to using other tools in a more targeted way.
::::::::

## Core NLP Terminology

Before we start using Voyant to explore our text corpora in more detail, it is useful to define some core NLP concepts so that you can understand what Voyant is looking for as it reads text data.

First of all, Voyant needs to parse the text as a sequence of characters (or **string**) and identify meaningful linguistic units such as words, numbers and punctuation. A **token** is a defined unit within a string, such as an individual appearance of word or number, usually separated from other tokens by whitespace. A **type**, on the other hand, is a unique word form, which may appear many times in a corpus. The relationship between tokens and types, i.e. how many unique word forms there are in a corpus versus how many times they are used, is a measure of the **lexical diversity** of the corpus. 


::::: keypoints  

1. The Voyant website allows you to dive into your corpus right away by uploading a document or several to its server.  
2. Most of Voyant's dashboard tools such as Cirrus, Termsberry and Contexts, rely on token frequency counts and collocations.  
3. These types of tools can yield insights into the lexical diversity of the corpus, which terms in a given corpus are most or least prominent, and the other words with which they frequently appear. This can highlight patterns or trends that can then be further analysed with other tools.

::::: 

