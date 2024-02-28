---
layout: post
math: true
toc: true
---
Tokenization in natural language processing (NLP)involves breaking down text into smaller units called tokens. These tokens can be words, characters, or subwords. This process is for preparing text for further processing.

## Word Tokenization
Word tokenization is the process of splitting text into individual words. 

Example: Input: "I like doing NLP" 

Tokens: ["I", "like", "doing", "NLP"]

## Byte-Pair Encoding Tokenization
It’s used by a lot of Transformer models, including GPT, GPT-2, RoBERTa, BART, and DeBERTa. BPE training starts by computing the unique set of words used in the corpus, then iteratively merge the most frequently occurring character or byte pairs in a given dataset until a desired vocabulary size is reached.

Example: word "low" appear 5 times, "lowest" appear 2 times, "newer" appear 6 times, "wider" appear 3 times, "new" appear 2 time in the corpus.

Step 1: Initial Vocabulary

corpus&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;vocabulary

5&nbsp;&nbsp;&nbsp;l o w _ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; _, d, e, i, l, n, o, r, s, t, w

2&nbsp;&nbsp;&nbsp; l o w e s t _

6&nbsp;&nbsp;&nbsp; n e w e r _

3&nbsp;&nbsp;&nbsp; w i d e r _

2&nbsp;&nbsp;&nbsp; n e w _

Step 2: Count and Merge Frequent Pairs (er appear 9 times)

corpus&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;vocabulary

5&nbsp;&nbsp;&nbsp;l o w _ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; _, d, e, i, l, n, o, r, s, t, w, er

2&nbsp;&nbsp;&nbsp; l o w e s t _

6&nbsp;&nbsp;&nbsp; n e w er _

3&nbsp;&nbsp;&nbsp; w i d er _

2&nbsp;&nbsp;&nbsp; n e w _

step 3: continues to count and merge Frequent Pairs (er_ appear 9 times) 

corpus&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;vocabulary

5&nbsp;&nbsp;&nbsp;l o w _ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; _ , d, e, i, l, n, o, r, s, t, w, er, er_

2&nbsp;&nbsp;&nbsp; l o w e s t _

6&nbsp;&nbsp;&nbsp; n e w er_

3&nbsp;&nbsp;&nbsp; w i d er_

2&nbsp;&nbsp;&nbsp; n e w _

step n: continues until the max vocabulary set is reached.

Algorithm:

<img width="747" alt="Screenshot 2024-02-28 at 12 27 59 AM" src="https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/3dc6166e-d4fb-4cf7-bce4-0929b904b315">
### Implementation
I've implemented both word tokenizer and BPE tokenizer in python from scratch:
<i class="far fa-hand-pointer fa-rotate-90"></i>
[dataset](https://github.com/zhiweilin27/NLP/blob/main/a1_tweets.txt)
<i class="far fa-hand-pointer fa-rotate-90"></i>
[python code](https://github.com/zhiweilin27/NLP/blob/main/a1_p1_lin_112845768.py)
<i class="far fa-hand-pointer fa-rotate-90"></i>
[output](https://github.com/zhiweilin27/NLP/blob/main/a1_p1_lin_112845768_OUTPUT.txt)


## Logistic Regression for Word Sense Disambiguation (WSD)
WSD is the process of identifying which sense of a word (i.e., its meaning) is used in a sentence when the word has multiple meanings.
For example, the word "return" has different meanings such as:
1. come back to a place or situation.
2. To yield a profit or result.

This task is crucial for many natural language processing (NLP) applications, such as machine translation, information retrieval, and text understanding. Logistic Regression is a simple (easy to interpret) and useful model to identify the sense of a word in a sentence, but the pitfall of logistic regression is it might not come with the most accurate result. 

More details about logistic regression or generalized linear regression can be seen in this [post](https://zhiweilin27.github.io/2023/10/22/Generalized-Linear-Regression.html#logistic-regression)

### Implementation
I've implemented logistic regression using PyTorch for Word Sense Disambiguation (WSD) from scratch:
(One also can use CNN, RNN, or transformer to do this task, as those may yield better accuracy)
<i class="far fa-hand-pointer fa-rotate-90"></i>
[dataset](https://github.com/zhiweilin27/NLP/blob/main/a1_wsd_24_2_10.txt)
<i class="far fa-hand-pointer fa-rotate-90"></i>
[python code](https://github.com/zhiweilin27/NLP/blob/main/a1_p2_lin_112845768.py)
<i class="far fa-hand-pointer fa-rotate-90"></i>
[output](https://github.com/zhiweilin27/NLP/blob/main/a1_p2_lin_112845768_OUTPUT.txt)



