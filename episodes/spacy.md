---
title: "Introduction to Natural Language Processing with spaCy"
teaching: 25
exercises: 35
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is spaCy and what can I do with it?
- What are the steps in its English-language processing pipeline?
- What are the fundamentals of Python?
- How can I get started with Python and spaCy?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the steps involved in spaCy's text processing pipeline.
- Understand the fundamentals of Python syntax.
- Write basic Python code in Jupyter Notebook to run spaCy commands.

::::::::::::::::::::::::::::::::::::::::::::::::

## Getting Started with spaCy

Open Jupyter Notebook. You should already have installed spaCy as part of the lesson set-up instructions. If not, you need to do so **before** you import the package. 

```{python}
! pip -U install spacy
import spacy
```
Then, you need to load one of spaCy's language pipelines, in this case the large English pipeline, and assign it with the variable name 'nlp'.
```{python}
nlp = spacy.load("en_core_web_lg")
```


::::::::::: keypoints

1. spaCy is a free and open-source Python library for Natural Language Processing which is based on pre-trained processing pipelines. 

:::::::::::
