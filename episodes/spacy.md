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

## The (Very) Basics of Python

In progress...

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
Once you have input your text, you need to create a ```doc``` variable which you will use to call spaCy's ```nlp``` function onto your ```text```. It is good practice to use the ```print()``` function immediately after creating the ```doc``` (or indeed any new variable) to double-check that the output appears as you expect it to.
```python
greeting_doc = nlp(text)
print(greeting_doc)
```
As expected, the output reads ```Let's get started with spaCy :) .```.

One of the advantages of using spaCy is that it automatically tokenizes text and is able to recognise sentences, grammatical attributes and dependencies, named entities, and token lemmas. You can find out more about the features of the ```en_core_web_lg``` pipeline by visiting [spaCy's documentation pages](https://spacy.io/models/en#en_core_web_lg).

You can calculate the length of your ```greeting_doc``` by using the ```len()``` function, which will output the number of tokens in your text doc. If you want to see a list of the tokens spaCy has identified and counted, you should create a new variable and use **list comprehension** syntax to extract the tokens from the text **array**:
```python
greeting_tokens = [token for token in greeting_doc]
print(greeting_tokens)
```
:::::: challenge

Manually count what you would classify as tokens in your ```greeting_doc```. Then, in Jupyter Notebook, use the ```len()``` function to check your answer. Do they match? If not, what might be an explanation? 

:::::::::::::::::: hint 
Use the list comprehension method from above to create the ```greeting_tokens``` variable to see the tokens spaCy identified.
::::::::::::::::::

::::::::: solution
```python
len(greeting_doc)
```
```
8
```

```python
greeting_tokens = [token for token in greeting_doc]
print(greeting_tokens)
```
```
[Let, 's, get, started, with, spacy, :), .]
```
:::::::::
::::::

From this, we can see that spaCy recognises the smiley face emoji as a single token rather than two punctuation marks. We can also see that it recognises the 's as a single token dependency of the previous token, not as two separate tokens. 

spaCy automatically indexes objects in an array based on their position so that they can be called by their individual index number. It is important to note that **indexes in Python begin with zero**: the first object is assigned the index 0, the second object the index 1, and so on. 

Index numbers, which are always integers, are presented in [] brackets. You can specify a single index number or a range, by using a semicolon between the numbers inside square brackets, to extract them from your overall text array. For example, this could be useful if you had a set of texts and wanted to compare how they began but were not interested in their middles or endings.
```python
greeting_doc[0]
```
```
Let
```
```python
greeting_doc[0:5]
```
```
Let's get started with
```

::::::::: callout
### Indexing in Python
**Remember** If the length is *n*, the first index is 0 and the last index is *n-1*. 

In an index range, the output will be from the object indexed as the number before the colon **up to but not including** the number after the colon.
:::::::::


::::::::::: keypoints

1. spaCy is a free and open-source Python library for Natural Language Processing which is based on pre-trained processing pipelines. 

:::::::::::
