---
title:  "Computational Graph in Model Agnostic Meta Learning"
date:   2023-08-14 22:35:1 +0545
classes : wide
categories:
  - torch
  - meta-learning

excerpt: how torch handles second order derivative

header:
  og_image: /assets/images/sentence_embedding_image.jpg
  teaser: /assets/images/sentence_embedding_image.jpg
---

I found meta-learning amusing for the start especially this paper `Model Agnostic Meta Learning`. 


## Meta Learning Idea
It's fancy name for training neural-networks in such a way that, they can generalize to a new task with few training examples. For example, training a classification algorithm on your custom-usecase where you have only 5 training examples available for each class.  

Internet is full of resources for meta-learning. But I am interseted in discussion of a specific model architecture called MAML.
More specifically, I will visualize the computationl graph in this architecture because it involves second-order optimization.

## Dissecting MAML Algorithm
WIP. I have drawn out things. But need to validate stuffs which haven't got time to.
