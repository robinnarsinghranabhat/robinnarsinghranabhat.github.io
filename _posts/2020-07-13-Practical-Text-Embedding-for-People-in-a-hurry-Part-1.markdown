---
title:  "Keeping up with the Sentence Embeddings: 2020"
date:   2020-07-13 23:35:38 +0545
classes : wide
categories:
  - NLU || Text-Embedding
excerpt: A guide on generating unsupervised sentence embedding

header:
  og_image: /assets/images/sentence_embedding_image.jpg
  teaser: /assets/images/sentence_embedding_image.jpg
---

Few years past with introduction of word vectors, NLP research has again rapidly escalated again with idea of Pretrained Language modeling, which in turn gave significant boost in field of generating unsupervised contextual embedding of sentences.

We will look into series of notable papers and compare their performance in SentEval task to calculate sentence similarity.

### Wait .. Why need unsupervised embeddings ?

Apart from lack of supervised data-set for most of real world problems,  contextual embedding of text is one decent leap towards make computer close to humans in language Understanding. But don't worry, we are nowhere there yet. The ideas discussed below may be state of the art , but just good in a restricted settings.

In my own experience as ML Practitioner, when working on real life problems related to Natural Language Understanding like, Question Answering with FAQ, Fact checking systems e.t.c,  chief problem is lack of supervised dataset. Say a Garage company approaches to you and tells, they need automation of emails through FAQs they have prepared to generic queries. Before that, a human had to manually search the FAQ and reply to clients mail.


We will discuss the following sentence embedding techniques and their performance in senteval task.


## Word2vec||PAPER:LINK,
 by michilov brought along significant boost in NLP research with notion of deep learning based transfer learning.  Further research extended to using word vectors to generate sentence embedding, most significant to mention are these  techniuqes below

#### 1. Simple Average of Each words of sentences

It's mathmatically proved that, simple average of words gives empirically correct sentence embeddings.

#### 2. A SIMPLE BUT TOUGH-TO-BEAT BASELINE FOR SENTENCE EMBEDDINGS


#### 3. Skip Thought Vectors

##### 3.1 Basic Architecture
Trained in similar way as skip-gram word2vec model was trained. We have a encoder decoder architecture, closely resembling same one as in landmark paper neural machine translation||PAPER_LINK .

As with any encoder decoder architecture, encoder will generate a thought vector, which is processed by the decoder to generate the words


The training architecture is , (s_(i-1) , s_i , s_(i+1)  ) , the encoder takes in s_i , which itself is composed of **t** words.





<!-- along with it's modifications variants



1. Word Vectors
  - Average of words vectors
  - A simple but tough to beat baseline sentence embedding
  - Concatenated Power Mean Word Embeddings as Universal Cross-Lingual Sentence Representations


2. Infersent
2. Universal Sentence Encoder
3. BERT and it's variations



## use here and see which outperformes , visualize the vector space of sentence embedding
 https://github.com/brmson/dataset-sts/tree/master/data/sts/semeval-sts


## Use simple text classification dataset, and check how
## nearest neighbour on classification performs with these unsupervised approaches. i.e without training
 -->




{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}
