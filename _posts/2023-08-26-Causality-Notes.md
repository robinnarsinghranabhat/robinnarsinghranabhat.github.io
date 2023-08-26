---
title:  "Notes on Causality"
date:   2023-08-14 22:35:1 +0545
classes : wide
categories:
  - Data-Science
  - Causality

excerpt: Helpful Causality intuition 

header:
  og_image: /assets/images/sentence_embedding_image.jpg
  teaser: /assets/images/sentence_embedding_image.jpg
---

## Intro

Suppose there's a clinic to deal with people having headache. `Patients with headache` come there and consult with the doctor. Some of patients might take the prescribed pill. Especially because they are terminally ill or have exams. Some might not because they are on vacation. And think feel like a good rest will treat it. Suppose it's the policy for all people who come to clinic with headache to update their status tomorrow on whether they got treated. 

Now, suppose a data scientist was assigned to calculate the efficacy of the pill. They use this `historical/observational` data from clinic. Then calculate, amongst the people who took the pill, how many felt well (W) the other day say `P( W , medicine=1  )`. And same for the group who didn't take it as `P(W | medicine=0)`. But we know this calculation is wrong.


## Observation vs Intervention 
Instead of using this historocal data, the correct way would be, get a group of sick people with headache. Randomly divide them into two groups. Force one to take the pill and other to not take the pill. And now calculated those Probabilities.

This time, we write probability of getting treated given a patient takes medicine as : `P( W, do(medicine)=1 )`

This `do` operator is doing something super significant. Telling the reader (like someone going through a research paper) that, there are not other hidden variables that can effect the probabilty.  