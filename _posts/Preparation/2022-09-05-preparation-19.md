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
   Before feeding word sequences into BERT, 15% of the words in each sequence are replaced with a [MASK] token. The model then attempts to predict the original value of the masked words, based on the context provided by the other, non-masked, words in the sequence.

   ![download1](https://user-images.githubusercontent.com/96654391/188531248-8bf6007f-0289-434d-a94f-79556ef41e40.png)

   1. Adding a classification layer on top of the encoder output.
   2. Multiplying the output vectors by the embedding matrix, transforming them into the vocabulary dimension.
   3. Calculating the probability of each word in the vocabulary with softmax. <br>

2. Next Sentence Prediction (NSP)

   During training, 50% of the inputs are a pair in which the second sentence is the subsequent sentence in the original document, while in the other 50% a random sentence from the corpus is chosen as the second sentence. The assumption is that the random sentence will be disconnected from the first sentence. <br>
   이런 문제가 있어서 BERT에서는 문장 시작 부분에 [CLS] 끝나는 부분에 [SEP]을 붙혀서 토큰화, 임베딩을 한다. <br>

   ![download2](https://user-images.githubusercontent.com/96654391/188532302-3ae6c9dc-f3a2-42b8-a662-32450e7e3ce5.png) <br>

   To predict if the second sentence is indeed connected to the first, the following steps are performed: <br>

   1. The entire input sequence goes through the Transformer model.
   2. The output of the [CLS] token is transformed into a 2×1 shaped vector, using a simple classification layer (learned matrices of weights and biases).
   3. Calculating the probability of IsNextSequence with softmax.

### How to use BERT (Fine-tuning)

In the fine-tuning training, most hyper-parameters stay the same as in BERT training, and the paper gives specific guidance (Section 3.5) on the hyper-parameters that require tuning. The BERT team has used this technique to achieve state-of-the-art results on a wide variety of challenging natural language tasks, detailed in Section 4 of the paper. <br>

BERT’s bidirectional approach (MLM) converges slower than left-to-right approaches (because only 15% of words are predicted in each batch) but bidirectional training still outperforms left-to-right training after a small number of pre-training steps.

## BERT 설명 pdf

<https://arxiv.org/pdf/1706.03762.pdf>

## BERT language model

<https://www.techtarget.com/searchenterpriseai/definition/BERT-language-model#:~:text=BERT%2C%20which%20stands%20for%20Bidirectional,calculated%20based%20upon%20their%20connection>

### How BERT works

The transformer is the part of the model that gives BERT its increased capacity for understanding context and ambiguity in language. The transformer does this by processing any given word in relation to all other words in a sentence, rather than processing them one at a time. the Transformer allows the BERT model to understand the full context of the word, and therefore better understand searcher intent. <br>

BERT uses a method of masked language modeling to keep the word in focus from "seeing itself" -- that is, having a fixed meaning independent of its context. => ?

## Fine-tune BERT Model for Sentiment Analysis in Google Colab

<https://www.analyticsvidhya.com/blog/2021/12/fine-tune-bert-model-for-sentiment-analysis-in-google-colab/#:~:text=Introduction%20to%20BERT%20Model%20for,negative%2C%20or%20neutral%20about%20it.>

### What is BERT Tokenizer?

The tokenizers should also match the core model that we would like to use as the pre-trained, e.g. cased and uncased version. <br>

<https://huggingface.co/docs/transformers/model_doc/bert#berttokenizer> : BERT 하이퍼 파라미터 정리 <br>

## Transformer와 Tensorflow를 가지고 fine-tunning 해보기

<https://velog.io/@jaehyeong/Fine-tuning-Bert-using-Transformers-and-TensorFlow>
