---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/nlp.png
title: 텍스트 전처리과정
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231227
tags: preprocessing
lang: ko
---
`텍스트 전처리`{:.success}

문서 혹은 텍스트는 프로그래밍 언어 안에서 문자열로 표현이 된다. 문장 혹은 문자열들은 각각의 단어들로 구성되어 있고 그 단어들의 순서에 따라 이해를 한다.
따라서 컴퓨터에게 어떤 문장을 이해시키려면 문장을 단어 단위로 나눈 후에 리스트 형태로 변환해 주어야 한다. 이 과정에서 쓸모 없는 문자들은 제거를 한다.

<!--more-->
## 1. 텍스트 전처리 단계
### 정제(cleaning)
분석에서 불 필요한 noise 제거하는 작업이다. noise 제거 작업은 토근화 이전에 이루어지나 토큰화 이후에도 필요한 경우 계속 일어난다. 사전에 유의미한 단어라도 분석결과 의미 없는 단어라면 제거하게 되는데 이를 불용어제거(stopword removal)이라고 한다.

### 토큰화(Tokenization)
텍스트를 원하는 단위로 나누는 작업을 말한다. 원하는 단위가 문장인 경우 문장 토큰화라고 하고, 단어인 경우에는 단어 토큰화라고 한다.

### 정규화
같은 의미를 가진 동일한 단어임에도 불구하고 다른 형태로 쓰여진 단어들을 통일시켜서 표주 단어로 만드는 작업이다. 예를 들어 go 와 gose 는 인칭에 따라서 다른 문법이지만 같은 단어로 봐야 할 때도 있다.

### 품사 태깅
품사는 단어를 문법적인 기느에 따라 분류한 것을 말하며, 명사, 대명사, 동사, 형용사 등이 있다. 앞서 토큰화된 단어에 품사를 파악해 부착하는 것을 의미한다.

## 2. 문장 토큰화
문장의 단위로 토큰화를 진행한다.
```python
from nltk.tokenize import sent_tokenize

para = "Hello everyone. It's good to see you. Let's start our text mining class!"
print(sent_tokenize(para))
```
위 코드는 nltk module 를 사용하여 문장 단위로 토큰활르 진행하는 작업이다. 문장의 기준은 마침표 단위로 문장을 나누게 된다. 따라서 결과는 아래와 같다.

```text
['Hello everyone.', "It's good to see you.", "Let's start our text mining class!"]
```
