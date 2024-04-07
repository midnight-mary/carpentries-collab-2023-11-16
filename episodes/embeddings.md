---
title: "Introduction to Word Embeddings"
teaching: 40
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are word embeddings and what are they for?
- How can I create embeddings using spaCy?
- How can I visualise the results?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the principles behind word embeddings.
- Use Python, spaCy and Pandas to create word embeddings for a corpus of musical terms.
- Use Google TensorFlow's Embedding Projector tool to visualise and interpet the results.

::::::::::::::::::::::::::::::::::::::::::::::::

The dataset for this episode, containing terms from Boomkat's 'Grime / FWD' and 'Industrial / Wave / Electro' subgenre corpora, can be accessed via the ['Episode 5' Zenodo repository](https://zenodo.org/records/10931458).

::::::::::::::::::challenge

You may have noticed that the ```merge_embeddings_genre_df``` has more rows than the unduplicated ```grime_ind_terms_df``` we created earlier. Why could that be? Can you amend the code used to create the ```grime_ind_embeddings_df``` to make the number of rows match the number of unduplicated terms?

::::::::::::::::::::::::hint 

The terms in our lists are word **types** but are not necessarily single **tokens**. As you will recall from our first encounter with spaCy, it treats possessives like 's as separate tokens. This means that the process of creating a list of doc objects of terms based on their tokens, spaCy's ```nlp``` function has added rows (and vectors) for these tokens.

We can override this by specifying that only the first token in each ```doc``` is necessary to represent the term and that others should be discounted.

:::::::::::::::::::::::::

:::::::::::::::::::::::::::::solution

```python
embeddings = []
for doc in docs:
    token = doc[0]
    embeddings.append([token.text] + token.vector.tolist())
grime_ind_embeddings_df = pd.DataFrame(embeddings)
grime_ind_embeddings_df.shape
```
```
(685, 301)
```

::::::::::::::::::::::::::::::

::::::::::::::::::


:::::::::::::::::discussion

In breakout rooms of pairs or groups of three, go to the website for Google TensorFlow's [Embedding Projector Tool](https://projector.tensorflow.org/) and load the grime_industrial_embedding data and metadata files. Play around with the settings and the projection and use the Etherpad to write down questions and observations to share with the whole group.

::::::::::::::::::::hint 

Use the 'Color By' function to differentiate terms by genre. This will assign a different colour to Grime versus Industrial terms and allow you to visually identify semantic themes that are more prevalent in one or the other genre.

Enable the 3D labels mode to see the terms themselves rather than points.

::::::::::::::::::::

::::::::::::::::::

::::::::::: keypoints

1. Word embeddings rely on a conception of language (as a finite vocabulary) as a totality that occupies multi-dimensional space.
2. Word embeddings are sets of vectors that position a given word in this multi-dimensional space, with every word orthogonal to every other word.
3. Embeddings are trained by unsupervised machine learning on large text corpora which looks for collocations between words, syllables and characters, and builds predictions as to the probability of given n-grams occuring in proximity. This presupposes that words that are semantically close (i.e. have similar meanings or usages) will be close together in the multi-dimensional space, while words that are semantically different will be far apart.
5. There are many established statistical methods for manipulating and interpreting word embeddings.
6. Google TensorFlow's Word Embedding Projector has built-in functions for dimensionality reduction which create intuitively readable visualisations of embeddings in 2- or 3-dimensional space.

::::::::::: 
