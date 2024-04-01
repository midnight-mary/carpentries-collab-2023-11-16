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

```python
! pip -U install spacy
import spacy
```
Then, you need to load one of spaCy's language pipelines, in this case the large English pipeline, and assign it with the variable name 'nlp'. Variables are assigned by typing in the name of the new variable, the equals sign, and the name and location of the object you want to assign to that variable.
```python
nlp = spacy.load("en_core_web_lg")
```
Now, let's input some simple text to begin processing. For Jupyter, Python and spaCy to recognise what we input *as* structured text rather than code, a different variable name or an undefined string, we will need to assign it a variable name, e.g. ```text```, and place the text itself into quotation marks. Either single or double quotation marks can be used, but consistency is key.
```python
text = "Let's get started with spacy :) ."
```
Once you have input your text, you need to create a ```doc``` variable onto which you can call spaCy's ```nlp``` function. It is good practice to use the ```print()``` function immediately after creating the ```doc``` or indeed any new variable to double-check that the output appears as you expect it to.
```python
greeting_doc = nlp(text)
print(greeting_doc)
```
As expected, the output reads ```Let's get started with spaCy :) .```.

One of the advantages of using spaCy is that it automatically tokenizes text in ```doc``` objects, and is able to generate token vectors, and recognise sentences, grammatical attributes and dependencies, named entities and token lemmas. You can find out more detail on the ```en_core_web_lg``` pipeline by visiting [spaCy's documentation pages](https://spacy.io/models/en#en_core_web_lg).


::::::::::: keypoints

1. spaCy is a free and open-source Python library for Natural Language Processing which is based on pre-trained processing pipelines. 

:::::::::::
