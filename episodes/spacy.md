---
title: "Introduction to Natural Language Processing with spaCy"
teaching: 25
exercises: 35
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is spaCy and what can I do with it?
- What are the steps in its English-language processing pipeline?
- How can I get started with Python and spaCy?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the steps involved in spaCy's text processing pipeline.
- Understand the fundamentals of Python syntax.
- Write simple Python code in Jupyter Notebook to run spaCy commands.

::::::::::::::::::::::::::::::::::::::::::::::::

## The (Very) Basics of Python

In progress...

## Getting Started with spaCy

SpaCy is a free, open-source software library for Natural Language Processing that uses the Python and Cython programming languages. One of the advantages of using spaCy is that it automatically tokenizes text and is able to recognise sentences, grammatical attributes and dependencies, named entities, and token lemmas. It can also calculate text similarity and perform classification and training tasks. 

Unlike other NLP libraries like NLTK and Flair, however, spaCy was developed for professional and commercial rather than educational purposes. Practically, this means it has a different learning curve because while some basic tasks are automatically built into its language pipelines, others are more idiosyncratic. You can find out more about its features by visiting [spaCy's documentation pages](https://spacy.io/usage/spacy-101). 

To begin, open Jupyter Notebook. You should already have installed spaCy as part of the lesson set-up instructions. If not, you need to do so **before** you import the package. 

```python
! pip -U install spacy
import spacy
```
Then, you need to load one of spaCy's language pipelines, in this case the large English pipeline, and assign it with the variable name ```nlp```. Variables are assigned by typing in the name of the new variable, the equals sign, and the name or pathway of the object you want to assign to that variable. From now on, spaCy will working with this pipeline every time you call nlp funtions.
```python
nlp = spacy.load("en_core_web_lg")
```
Now, let's input some simple text to begin processing. For Jupyter, Python and spaCy to recognise what we input *as* structured text rather than code, a different variable name or an undefined string, we will need to assign it a variable name, e.g. ```text```, and place the text itself into quotation marks. Either single or double quotation marks can be used for the same purpose, but consistency is key.
```python
text = "Let's get started with spaCy :) ."
```
Once you have input your text, you need to create a ```doc``` variable which you will use to call spaCy's ```nlp``` function onto your ```text```. It is good practice to use the ```print()``` function immediately after creating the ```doc``` (or indeed any new variable) to double-check that the output appears as you expect it to.
```python
greeting_doc = nlp(text)
print(greeting_doc)
```
As expected, the output reads ```Let's get started with spaCy :) .```

You can calculate the length of your ```greeting_doc``` by using the ```len()``` function, which will output the number of tokens in your text doc. If you want to see a list of the tokens spaCy has identified and counted, you should create a new variable and use **'for' loops** with **list comprehension** syntax to iterate through the ```greeting_doc``` and extract the tokens every time they are encountered in the text **array**:
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

From this, we can see that spaCy recognises the smiley face emoji as a single token rather than two punctuation marks. We can also see that it recognises the 's as a single token dependency of the previous token, not as two separate tokens. This is pretty clever, and shows that spaCy already has a contextual view of the text loaded into it.

In part, this has to do with spaCy's understanding of the tokens in the text as a specific sequence. SpaCy automatically indexes objects in an array based on their position so that they can be called by their individual index number, which is always an integer, and is presented in [] brackets. 

It is important to note that **indexes in Python begin with zero**: the first object is assigned the index 0, the second object the index 1, and so on. You can specify a single index number or a range by using a semicolon between the numbers inside square brackets to extract them from your overall text array. 
```python
greeting_doc[0]
```
```
Let
```
```python
greeting_doc[2:5]
```
```
get started with
```
If you don't want to specify a beginning or end index number, but want to go from or to there from a specified point, you can omit either the number before or after the colon. For example, this could be useful if you had a set of texts and wanted to compare their endings.
```python
greeting_doc[3:]
```
```
started with spaCy :) .
```
::::::::: callout
### Indexing in Python
**Remember**: if the length of your array is *n*, the first index is 0 and the last index is *n-1*. 

In an index range, the output will be from the object indexed as the number before the colon **up to but not including** the number after the colon.
:::::::::
## Recognizing Parts Of Speech

Being able to identify and extract specific parts of speech can be incredibly useful when working with large text corpora. Helpfully, spaCy's nlp pipelines have been trained on large language datasets to be able to automatically, and quite reliably, recognise certain linguistic attributes such as parts of speech, grammatical functions, named entities, and so on. For example, with the Boomkat corpus we have already explored in the previous episode, you might want to further analyse the descriptive words it contains and their sentiments, or isolate named entities such as record labels and place names to begin to construct a network. 

Tasks such as these require understanding how spaCy parses text and classifies parts of speech, as well as using 'for' loops to iterate through text arrays to extract relevant information. Let us inspect our ```greeting_doc``` in this more systematic way to extract the different token attributes that form part of spaCy's nlp pipeline. 
```python
for token in greeting_doc:
    print(token.text, token.lemma_, token.pos_, token.tag_, token.dep_,
    token.shape_, token.is_alpha, token.is_stop)
```
```
Let let VERB VB ROOT Xxx True False
's us PRON PRP nsubjpass 'x False True
get get AUX VB auxpass xxx True True
started start VERB VBN ccomp xxxx True False
with with ADP IN prep xxxx True True
spaCy spaCy PROPN NNP pobj xxxXx True False
:) :) PUNCT . punct :) False False
. . PUNCT . punct . False False
```
Here, every line of the output pertains to a single token in the greeting doc, and displays the token text, the lemmatized form of the token, the part of speech it represents, its tag, its dependency, and its letter case shape. Using Boolean True or False values, it also outputs whether the token is an alphanumeric character, and whether it is part of spaCy's default stopwords list.

Some of the output text is intuitively understandable but, if not, you can always use the ```spacy.explain()``` function to find out more. For example:
```python
spacy.explain("NNP")
```
```
'noun, proper singular'
```
From this, we can tell that spaCy has recognised its own name as a noun, not as an adjective meaning space-like. This is an accurate reading in this example not only because of the syntactic positioning of this word in our text but also because of the token shape, which includes the characteristic uppercase C that forms part of spaCy's brand identity. 

Let us now move on to a more complex text example. In Jupyter Notebook, create a new ```text``` variable which takes the whole of the first description from the 'modern_classical_ambient_desc_only' spreadsheet you downloaded during the [last episode](https://acceleratingdigitalskills.github.io/Processing-Text-Based-Corpora/voyant.html). 

Note that Jupyter often auto-fills quotation marks and this can get confusing if your text also has quotation marks within it, so double-check that they match at the beginning and end of your text. Use the ```print()``` function to check that the text looks as you expected.
```python
text = "'Clouds' is a perfectly measured suite of warm and hazy downbeats from Gigi Masin, Marco Sterk (Young Marco), and Johnny Nash recorded in the heart of Amsterdam's red light district over one weekend in April, 2014.It's all about louche vibes and glowing notes, gently absorbing and transducing the buzz of the streets outside the studio's open windows into eight elegantly reserved improvisations segueing between lush ambient drift, dub-wise solo piano pieces, and chiming late night jazz patter. In that sense, there's striking similarities between 'Clouds' and the recent Sky Walking album by Lawrence and co., but where they really go for the looseness, Gaussian Curve keep it supple yet tight, bordering on adult contemporary suaveness anointed with finest hash oil. Imbibe slowly."
print(text)
```
```
'Clouds' is a perfectly measured suite of warm and hazy downbeats from Gigi Masin, Marco Sterk (Young Marco), and Johnny Nash recorded in the heart of Amsterdam's red light district over one weekend in April, 2014.It's all about louche vibes and glowing notes, gently absorbing and transducing the buzz of the streets outside the studio's open windows into eight elegantly reserved improvisations segueing between lush ambient drift, dub-wise solo piano pieces, and chiming late night jazz patter. In that sense, there's striking similarities between 'Clouds' and the recent Sky Walking album by Lawrence and co., but where they really go for the looseness, Gaussian Curve keep it supple yet tight, bordering on adult contemporary suaveness anointed with finest hash oil. Imbibe slowly.
```
Then, turn the text into an ```nlp``` ```doc``` variable, as before, and check the length.
```python
doc = nlp(text)
len(doc)
```
```
147
```

In Python, you can use **'if'** and **'if not' statements** to further refine your 'for' loop list comprehensions, which makes it possible to focus on particular token attributes while ignoring others. These 'for ... in ... if/not ...' statements rely on standard logical conditions from maths, such as equals to (```==```), not equals to (```!=```), greater/less than (```> / <```), etc. 

For example, with the Boomkat ```doc``` from above, we can create a list of tokens that excludes all punctuation marks: 
```python
word_tokens = [token 
              for token in doc
              if not token.is_punct]
print(word_tokens)
```
```
[Clouds, is, a, perfectly, measured, suite, of, warm, and, hazy, downbeats, from, Gigi, Masin, Marco, Sterk, Young, Marco, and, Johnny, Nash, recorded, in, the, heart, of, Amsterdam, 's, red, light, district, over, one, weekend, in, April, 2014.It, 's, all, about, louche, vibes, and, glowing, notes, gently, absorbing, and, transducing, the, buzz, of, the, streets, outside, the, studio, 's, open, windows, into, eight, elegantly, reserved, improvisations, segueing, between, lush, ambient, drift, dub, wise, solo, piano, pieces, and, chiming, late, night, jazz, patter, In, that, sense, there, 's, striking, similarities, between, Clouds, and, the, recent, Sky, Walking, album, by, Lawrence, and, co., but, where, they, really, go, for, the, looseness, Gaussian, Curve, keep, it, supple, yet, tight, bordering, on, adult, contemporary, suaveness, anointed, with, finest, hash, oil, Imbibe, slowly]
```

You can also use equals to (```==```) and Boolean values of ```True``` or ```False``` to obtain the same result. 
```python
word_tokens2 = [token 
              for token in doc
              if token.is_punct==False]
print(word_tokens2)
```
```
[Clouds, is, a, perfectly, measured, suite, of, warm, and, hazy, downbeats, from, Gigi, Masin, Marco, Sterk, Young, Marco, and, Johnny, Nash, recorded, in, the, heart, of, Amsterdam, 's, red, light, district, over, one, weekend, in, April, 2014.It, 's, all, about, louche, vibes, and, glowing, notes, gently, absorbing, and, transducing, the, buzz, of, the, streets, outside, the, studio, 's, open, windows, into, eight, elegantly, reserved, improvisations, segueing, between, lush, ambient, drift, dub, wise, solo, piano, pieces, and, chiming, late, night, jazz, patter, In, that, sense, there, 's, striking, similarities, between, Clouds, and, the, recent, Sky, Walking, album, by, Lawrence, and, co., but, where, they, really, go, for, the, looseness, Gaussian, Curve, keep, it, supple, yet, tight, bordering, on, adult, contemporary, suaveness, anointed, with, finest, hash, oil, Imbibe, slowly]
```

Furthermore, you can use ```or``` and ```and``` conditions to refine your list comprehension. For example, you could specify that you want to extract only nouns and proper nouns from your ```doc```.
```python
nouns_and_proper_nouns = [token 
              for token in doc
              if token.pos_=="NOUN" or token.pos_=="PROPN"]
print(nouns_and_proper_nouns)
```
```
[Clouds, suite, downbeats, Gigi, Masin, Marco, Sterk, Young, Marco, Johnny, Nash, heart, Amsterdam, light, district, weekend, April, 2014.It, vibes, notes, buzz, streets, studio, windows, improvisations, drift, dub, piano, pieces, night, jazz, patter, sense, similarities, Clouds, Sky, Walking, album, Lawrence, co., looseness, Gaussian, Curve, adult, suaveness, hash, oil]
```
::::::::::::::::: challenge
Use **for ... if...** syntax to create a list of adjectives and adverbs with the variable name ```adj_and_adv``` from your ```doc```.

::::::::::hint 
It is a common mistake, but if you use ```and``` in the code you will get a blank ```[]``` result because the ```and``` specifies that an individual token should be both an adjectives **and** an adverb.  This is impossible in this instance, hence the blank result - a distinction that can be missed in casual communication but is key to the formal logic of programming. 

So, you should use ```or``` to avoid this and print only tokens that are **either** adjectives **or** adverbs.
:::::::::::

::::::solution
```python
adj_and_adv = [token 
              for token in doc
              if token.pos_=="ADJ" or token.pos_=="ADV"]
print(adj_and_adv)
```
```
[perfectly, warm, hazy, red, louche, glowing, gently, open, elegantly, lush, ambient, wise, solo, late, recent, really, supple, yet, tight, contemporary, finest, slowly]
```
::::::

:::::::::::::::::::

::::::::callout

Like Voyant, spaCy has sets of stop words for the languages it supports that can be called and modified. For this, you have to ```import``` the ```stop_words``` module which contains the English language ```STOP_WORDS``` set and create a ```stop_words``` variable in your own project.
```python
from spacy.lang.en import stop_words as stop_words
stop_words = stop_words.STOP_WORDS
```
Use this link to find more [information on how to edit spaCy stopword sets](https://github.com/explosion/spaCy/blob/master/spacy/lang/en/stop_words.py).

::::::::

::::::::::: keypoints

1. spaCy is a free and open-source Python library for Natural Language Processing which is based on pre-trained processing pipelines. 

:::::::::::
