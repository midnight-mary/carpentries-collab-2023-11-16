---
title: "Starting with Voyant"
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
  
 doc = nlp(text)    
 word_tokens = [token.text      
               for token in text if not token.is_punct]     
print(word_tokens)     

:::::: solution

doc = nlp(text)    
 word_tokens = [token.text      
               for token in doc if not token.is_punct]     
print(word_tokens)  

::::::

:::
                
