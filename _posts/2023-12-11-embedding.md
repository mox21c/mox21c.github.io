---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/nlp.png
title: 임베딩(Word Embedding)
sidebar:
  nav: docs-ko
aside:
  toc: true
key: 20231211
tags: embedding
lang: ko
---

`EMBEDDING`{:.success} `word embedding`{:.success} `ONE-HOT ENCODING`{:.success}

각 문서에서 중요한 단어를 추출하여 벡터로 표현하여 수치화 하기 위한 작업으로, 문장의 벡터를 원하는 크기로 축소한다.

<!--more-->

##희소 표현(Sparse Representation)
단어의 갯수가 아래와 같이 3개(A,B,C)인 경우 벡터 또는 행렬로 표현은 one-hot 벡터로 표현할 수 있다.
우선 단어의 one-hot 벡터에 대해 먼저 확인을 먼저 해보자.
A, B, C 의 단어가 있을 때 one-hot 벡터로 표현하면 아래와 같다.

$$
\begin{bmatrix} A \\ B \\ C \end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}
$$

이 된다.

### One-hot matrix 단점
10 만개의 단어가 있을 때 해당 단어의 one-hot 벡터로 표현하면 10만개 차원의 행렬로 된다. 즉 엄청난 차원의 **비효율적인 행렬**로 표현이 된다.

one-hot 행렬로 표현 했을 때의 또다른 문제점은 **단어간 의미의 파악이 불가능** 하다는 것이다.

## 밀집 표현(Dense Representataion)
희소 표현과 반대되는 표현으로 밀집표현이 있다. 밀집 표현은 벡터의 차원을 단어 집합의 크기로 상정하지 않는다. 사용자가 설정된 값으로 모든 단어의 벡터 표현의 차원을 맞춘다.
예를들어 단어의 갯수가 10,000개 이고, 강아지란 단어를 벡터로 표현하게 된다면 아래와 같다.
강아지 = [0 0 0 0 1 0 0 0  .......]
하지만 사용자가 밀집표현의 차원을 128로 설정한다면 10,000개의 차원의 벡터는 128개의 차원으로 줄어들고 모든 값이 변하게 된다.
강아지 = [0.2 0.3 -2.1 0.4 .......]
이렇게 벡터의 차원이 조밀해졌다고 하여 밀집 벡터라고 하고, 워드 임베딩(Word Embeddding) 이라고 한다.

### Embedding 을 하는 이유
embedding 은 one-hot matrix 의 범주형 데이터를 연속적 값을 갖는 상대적으로 작은 크기의 벡터로 변환하는 작업으로 단어 간의 의미적 유사도를 계산할 수 있고, 단어의 의미적인 정보를 함축함으로 연산이 가능하게 된다. 또한 전이학습을 가능하게 한다.

## Embedding processing
sequence of word -> one-hot vector -> embedding vector 형태의 프로세스를 가진다.
![embedding_process](/assets/images/ai/embedding_process.png)

사실 여기에서 의문점이 하나 생길 수 있다. BOW 와 임베딩은 똑같이 문장을 단어로 만들어 벡터화 하는 작업으로 어떤 차이점이 있을까? BOW는 단어들의 빈도를 벡터 형태로 표현한다. 카운트 기반의 문서 표현에는 희소 벡터를 밀집 벡터로 표현하는 과정이 없으로 이것도 하나의 embedding 작업이다. 학습이나 통계적 기법으로 희소 벡터를 축소해 밀집벡터로 변환하고 그 벡터로 분석을 수행한다면 좀 더 완전한 embedding 으로 볼 수 있다.

카운트 기반의 문서 표현은 코사인 유사도와 같은 방법으로 희소 벡터 자체로 유사도를 계산할 수 있다. 즉 범주형 변수에 대한 one-hot encoding 와 다르게 어느 정도 문서의 의미가 반영 돼 있다.
### BOW 와 Embedding 의 차이점
BOW는 단어가 아닌 문서 단위로 embedding 이 이뤄진다 **이 과정에서 단어의 순서 정보를 잃으므로 사실상 문백에 대한 파악은 이뤄지지 않는다.**

## Embedding 종류
embedding 기법은 여러가지 종류가 있고, 아래와 같다.
- Word2Vec
- GloVe
- FastText
- ELMo(Embedding from Language Model)
- Item2Vec
- Node2Vec

