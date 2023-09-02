---
title:  "RL notes"
date:   2020-07-15 23:35:38 +0545
classes : wide
categories:
  - Reinforcement-Learning
excerpt: A guide to use Deep neural nets to train a lunar lander bot based on visual information

header:
  og_image: /assets/images/sentence_embedding_image.jpg
  teaser: /assets/images/sentence_embedding_image.jpg
---

## Planning

### Classical Planning
Given a start state in an environment (block a on b, block c on table), a model/Planner finds the sequence action to reach a goal-state (say a,b,c on top of each other with c at top and a at bottom).

Reference : https://www.sci.brooklyn.cuny.edu/~parsons/courses/3410-fall-2012/notes/lect07.pdf
 
### Planning in RL
Improving value function and policies with just compute, without interaction with environment
Reference : https://youtu.be/FKl8kM4finE?list=PLqYmG7hTraZDVH599EItlEWsUOsJbAodm&t=926


### Model Based vs Model Free
In Model-Based RL problems, there's a notion of model. We can send state-action into the model and get 
next state-reward. Example : Dreamer Paper.   

## What is DQN ??

It's simple a variation of regular   Q-learning algorithm to continuous state and action spaces.

## Policy Gradient

Say we have a function parametrized by thetha that gives use action-probabilites given a state.
We want to update theta in a direction that increments the Expected-Reward for above policy.

Practically, we can only estimate this. So, we run that same policy on a given state for say 20 times.
Collect all the actions and corresponding return value of those actions from all 20 episodes.

[Awesome Graphical Explanation](https://youtu.be/cQfOQcpYRzE) by Youtuber Elliot Waite.


