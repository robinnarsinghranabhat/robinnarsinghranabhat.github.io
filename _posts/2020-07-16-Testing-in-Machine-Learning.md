---
title:  "Unit Testing in Machine learning ?"
date:   2020-09-19 23:35:38 +0545
classes : wide
categories:
  - Data-Science
  - Testing
excerpt: Compilation of necessary  discussion on usefulness of unit testing in data science projects

header:
  og_image: /assets/images/sentence_embedding_image.jpg
  teaser: /assets/images/sentence_embedding_image.jpg
---

Testing is not a data scientist's best practice in software engineering. Because of constant experimentation, adding test would seem like an unnecessary overhead.



## Why test ?


When your Machine learning code is in production, with all intermediate pipelines,  

- incoming messy data from server (raw text of customer review) , 
- preprocessing/ feature extraction,  
- stochastic algorithm

we generally make lot of assumptions on how data is like, and how it's being processed. Well, that's just assumptions. What if irrelevant values, columns were added in data warehouse, which is not common. System would break. 

Test helps to make sure, where it broke.

Key reason to tests : 

- Is code working as expected ( confidence that results are indeed correct ) , like adding assertions in code to check duplicated data, missing values where it's not supposed to . 
  Minimal test you can add is : assertions
- Make experimental changes rapidly without fearing to break the code
- Other people more confident in our code
-Helps catch bugs
-Understand the code for new users
-Help code development and refactoring
- less amazed at, like, don't get suprised when code breaks due to faulty production data in pipeline
- Code works not just in one computer, but across all the other users computer
- Show em data scientists can actually write good code !!



## When and what to test ?

It's an iterative process. You write code, you add test to make sure code does what you meant it to do. You make new changes, you add test.

Say a function that calculates mean, you write a test, and check it actually calculates mean. 

You test the answer is corrent. not internal computation.
Example, your code calculates mean :

```python
## simple example.py
def weighted_mean( array , weights ) :
  assert array.istype(np.array)
  assert weights.istype(np.array)
  return  np.sum(array * weights) / len(array)

## test_mean.py
def test_weighted_array( ):
  assert(weighted_mean( [1,2,3,4,5] , [0.5,0.5,0.5,0.5,0.5] )) == 3

```



TOOL OF CHOICE : pytest !!

Wait no unit tests .. Umm no, as much as headache testing already is, I won't want
to add more boilerplates, which unit tests does.



### General Example : 

Assume the folder structure : 

![](2021-01-19-23-45-43.png)

```python
## In capitalize.py, we have  function `capitalize_reverse`
## The function is supposed to capitalize text and reverse it, while ignoring numbers
def capitalize_reverse(text):
    return text[::-1].upper()
```

We make a separate file *test_deme.py* and write test for above function 

```python
## test our reverse function
def test_capitalize_reverse():
  assert capitalize_reverse('age') == 'EGA'
  assert capitalize_reverse('1243') == '3421'
```

In the shell, run the test as : **pytest test_demo.py**.

We get following output of successful testing :

![](/assets/images/testing_machine_learning/2021-01-19-23-45-43.png)


### More Data Science Specific Tests


