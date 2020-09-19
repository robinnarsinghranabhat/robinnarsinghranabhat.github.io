---
title:  "Unit Testing in Machine learning ?"
date:   2020-09-19 23:35:38 +0545
classes : wide
categories:
  - Data-Science
  - Testing
excerpt: A discussion on usefulness of unit testing in data science projects

header:
  og_image: /assets/images/sentence_embedding_image.jpg
  teaser: /assets/images/sentence_embedding_image.jpg
---


 In case of Data science, unit testing should more of the part of project, not goal of project. At the end of the day, Client care about delivery of predictions, patterns and forecasts. And unit tests assist to  ensure that the forecasts are at least not insensible.


## Why test ?

> Is code working as expected ( confidence that results are indeed correct)
> Make experimental changes rapidly without fearing to break the code
> Other people more confident in our code

Demo :

```python
## In this sample code, we see a basic testing
## We test our function ***capitalize_reverse***
## The function is supposed to capitalize text and reverse it, while ignoring numbers

## We make a separate file test_demo.py and run the code below as : **pytest test_demo.py**

def capitalize_reverse(text):
    return text[::-1].upper()

def test_capitalize_reserse( ):
  assert capitalize_reverse('age') == 'EGA'
  assert capitalize_reverse('1243') == '3421'

def test_capitalize_reserse( ):
    assert capitalize_reverse('age') == 'EGA'
    assert capitalize_reverse('1243') == '3421'

```python

We get following output of successful testing :

![](assets/images/test_1.png){:.align-center}  


## Why not test ?

> Time taking

## How to assert code is actually correct ?

> Manual sanity checks in head ( Try ways to break the code)
> Defensive Programming ( Tons of if else , exception handling , assertions )
> tests
