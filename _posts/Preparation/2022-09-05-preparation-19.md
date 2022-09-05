---
title: "[NLP] What is BERT?"
excerpt: "[NLP] What is BERT?"
categories: [Preparation]
tags: [Preparation, Python]
toc: true
toc_sticky: true
---

## BERT Explained: State of the art language model for NLP

<https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270> <br>

### How BERT works

BERT makes use of Transformer, an attention mechanism that learns contextual relations between words (or sub-words) in a text. In its vanilla form, Transformer includes two separate mechanisms — an encoder that reads the text input and a decoder that produces a prediction for the task. <br>
<br>

As opposed to directional models, which read the text input sequentially (left-to-right or right-to-left), the Transformer encoder reads the entire sequence of words at once. Therefore it is considered bidirectional, though it would be more accurate to say that it’s non-directional. This characteristic allows the model to learn the context of a word based on all of its surroundings (left and right of the word). <br>
<br>

When training language models, there is a challenge of defining a prediction goal. 빈칸에 들어가는 단어를 예측하는데 어려움이 있다. 왜? directional approach 자체의 한계점이다. 이를 극복하기 위해서 BERT는 2가지 전략을 사용한다.

1. Masked LM (MLM)
   Before feeding word sequences into BERT, 15% of the words in each sequence are replaced with a [MASK] token.

2. Next Sentence Prediction (NSP)
