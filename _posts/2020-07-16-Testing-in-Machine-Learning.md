---
title:  "Software Testing Practices in Data Science"
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

## Part 1 : Software Testing from first principles

Imagine you are a Machine leanring Engineer/ Data scientist making a `featurization` package, that teams across the company will utilize to develop new features.

Suppose this is your file structure for your package.

```
Some_Root_folder
|-- requirements.txt
|-- pyproject.toml
|-- .gitignore.txt
|-- featurizer
|   |-- featurizer.py 
|   |-- utils.py
|-- tests
|   |-- test_featurizer.py
```

`featurizer` directory will hold all your sub-packages and modules. Assume `tests` as a folder where you maintain unit-tests for all everything. Don't worry about other files and also, I am assuming you the `what exactly is a unit-test? and why i should bother` kind of audience.

```python
## Content of featurizer/featurizer.py
def weighted_mean( array , weights ) :
  ''' This function calcuales weighted mean of an array '''
  return  np.sum(array * weights) / len(array)

## Content of tests/test_featurizer.py
def test_weighted_array( ):
  ''' This is a test for above writter function '''
  assert(weighted_mean( np.array([2,4,4]) , np.array([0.5,0.25,0.25]) )) == 3
```

"But wait, isn't this just checking if the function works as expected for some really trivial input", you may ask. Exactly, that's what I am doing. 

The code `test_featurizer.py` partly ensures your implementation is indeed correct. But, it's much more than that. 

Assume in your large organization, Say, new novice developer changed the implementation of the `weighted_mean` function to address **lists input** instead of **numpy array** to suit his needs. This is really common ...

Now, how `tests` folder is employed in software development practice is, all files inside `tests` folder needs to be successfully executed during each commit. If they don't, commit is cancelled. So, first thing new developer sees is, he cannot push the changes because his push will cause `test_weighted_array` function to fail that assumes a numpy array. 

So realisizing there was a unit test for that function, this new developer can look at the unit test and find more insights on  what the original code-writer assumed when the function `weighted_mean` was written. And gets enlightened.


Furthermore, When you have a really good set of tests that test different functionalities and the combinations of those, you become more sure, new changes to codebase won't break some other part of code in some unexpected ways you will find only 2 weeks later. 

### How to include tests as part of development ? 

Remember, i said how we employ  software test is, we write scripts containing functions that check implementation of functions from our package, we stack scripts containing those checks in some folder and we configure a git hook to run another python script or shell command that will execute all the .py files inside our specified tests folder. 

Or, You can can install a test-runner application that will handle those boilerplate steps for you. 

For our purposes, we will use `pytest`
```
pip install pytest
```

Make sure your pyproject.toml will look like : 

```python
# pyproject.toml
[tool.pytest.ini_options]
minversion = "6.0"
addopts = "-ra -q"
testpaths = [
    "tests",
]
```
We are just telling pytest to grab all tests inside `tests` folder and execute files inside it. Note, by default, pytest will only run scripts with prefix `test_` in naming. 

**Executing your test**
```python
pytest ./tests 
```

Now, I talked about this being executed everytime we commit. For that, 
we will use a git-hook called Pre-commit hooks, whose only job is to run certain checks locally when you try to commit, catching problems before they reach your repository.

for a minimal setup, lets first install the library as -
> precommit install

Them add this file in the root. <br/>
`.pre-commit-config.yaml`
```yaml
repos:
  - repo: local
    hooks:
      - id: pytest
        name: pytest
        stages: [commit]
        language: system
        entry: pytest  ./tests
        types: [python]
```
git is automatically configured to read `.pre-commit-config.yaml` in the root for any pre-commit hooks. 

**That's all. Now you have a project setup where you will automatically run tests before each commit.**

Note there are several other useful hooks that will automatically sort your code (isort) and reformat code according to pep standards (flake8 and black) or do static type checks (mypy) that you can employ before any developer pushes changes. 

Just to show this, this would how your `.pre-commit-config.yaml` would look like with those included.

```yaml
repos:
  - repo: local
    hooks:
      - id: isort
        name: isort
        stages: [commit]
        language: system
        entry: python -m isort ./featurizer ## sorts all py files inside featurizer folder
        types: [python]

      - id: black
        name: black
        stages: [commit]
        language: system
        entry: python -m black ./featurizer  ## reformats py files inside featurizer folder
        types: [python]

      - id: flake8
        name: flake8
        stages: [commit]
        language: system
        entry: python -m flake8 ./featurizer ## similar to black ..
        types: [python]
```


### Conclusion 


So, A tests basically  :
- Makes sure new changes to codebase doesn't break/change something undesirably
- Makes sure the developer's implementation is at least minimally correct. 
- Makes it easier for teams to understand logic of a function 

That's all right. Obviously not. The most important advantage comes with practice of test-driven-development.

## Part 2 :  Test Driven Developement (T.D.D)

This software developement practice that has saved me countless hours of writing and debugging code. 

Going back to that earlier `featurization` packaage, imagine you as a ML engineer, need to add another function that will convert any letter into its corresponding index.

Before you start with the following.
```python
## Content of featurizer/featurizer.py
def letter_to_index( letter ) :
  ''' This function maps letter to a integer '''
  pass
```

```python
## Content of tests/test_featurizer.py
def test_letter_to_index_function( ):
  ''' test for letter_to_index function '''
  assert letter_to_index( 'a' ) = 0
  assert letter_to_index( 'z' ) = 25
```

Now you start writing your implementation for `letter_to_index` function. 
This practice forces developer to think rigourously about the problem, what kind of input function expects and what the output would be. Biggest byproduct is, your write better and structured code. 

Note, test shines best as the when project is convoluted or your are implementing more ridiculous functions. 

### Conclusion 
I understand, like that math's teacher who does question number 1 and expcets you to complete the rest of difficult exercise, I gave some really trivial examples. But your code is obviously more notorious. Maybe, it's really difficult to write test for your system. Maybe your system interacts with database or API, or the code itself is super convoluted and thus difficult to import functions, initialize classes and test one specific behaviour.

For problem number 1, where external components is required, we do something called 'mock' and can easily mitigate. For the second part, as I have mentioned, you don't introduce tests 6 months after starting your project. It's a part of software dev from start, and if you start T.D.D from the beginning, you are forced to write code that makes unit-testing easier. As a byproduct, makes the overall code better and structured. Think about it, you are building a package that's to be used by other developers. And as you import your functions in those scripts inside `tests` folder and use them, you get more insight to your modules will be used. 

**Implementing this will be the best way to get a hang of it, whether in your current codebase, or, if it's a new one, the better.**

## Part 3 :  Data science specific Testing
In Data Science domain , testing usually revolves around : 

- Checking DataFrames after some operation (like merge, transformation) is as expected
- Models with non-deterministic outcomes
- Checking the Data itself. For machine learning, we replace conditional logics with matrix multiplication happening inside a trained Model weights. These weights depend on Data itself. Hence, Data is the new code. Don't worry, it's really easy.



