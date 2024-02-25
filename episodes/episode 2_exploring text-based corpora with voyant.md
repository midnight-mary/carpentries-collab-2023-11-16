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

- Load data into Voyant and perform inductive analysis
- Define key terms relating to textual analysis
- Identify affordances and constraints of a frequency-based approach to corpus analysis

::::::::::::::::::::::::::::::::::::::::::::::::

::: challenge

 Correct this command to generate a list of token words, excluding punctuation symbols. You should only have to change one word. 
 
 ``` 
 doc = nlp(text)    
 word_tokens = [token.text      
                for token in text if not token.is_punct]     
print(word_tokens)     
```

:::::: solution

```
doc = nlp(text)    
 word_tokens = [token.text      
                for token in doc if not token.is_punct]     
print(word_tokens)
```  

::::::  

:::

::::: keypoints  

1. The Voyant website allows you to dive into your corpus right away by uploading a document or several to its server.  
2. Most of Voyant's dashboard tools such as Cirrus, Termsberry and Contexts, rely on token frequency counts and collocations.  
3. These types of tools can yield insights into the lexical diversity of the corpus, which terms in a given corpus are most or least prominent, and the other words with which they frequently appear. This can highlight patterns or trends that can then be further analysed with other tools.

::::: 

