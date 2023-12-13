---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: 활성화 함수(activation function)
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231212
tags: 활성화함수
lang: ko
mathjax: true
---

활성화 함수는 뉴런을 흥분시키기 위한 함수이다.
뉴런으로 들어오는 모든 입력에 가중치를 곱하고 그것들을 합산한 값에 편향을 더한 후, 뉴런의 흥분 상태를 표시하는 신호로 전환한다.
활성화 함수가 없으면 뉴런의 연산은 단순한 곱셈의 합이 되어버려 신경망이 갖는 표현력을 잃어 버린다.

<!--more-->

![Image](/assets/images/ai/deeplearning/activation_function.png)

가중치(w)가 달린 입력(x)신호 와 편향(b)의 총합을 계산하고 함수 f에 넣어 출력하는 흐름을 보여준다.
활성화 함수는 비선형 함수를 사용해야 한다. 선형함수로 활성화 함수를 사용하게 된다면 은닉층이 없는 네트워크로 표현이 된다.


## 1. 계단 함수
![Image](/assets/images/ai/deeplearning/step_function.png)

## 2. 시그모이드 함수

## 3. tanh 함수

## 4. ReLU 함수

## 5. Leaky ReLU 함수

## 6. 항등함수

## 7. Softmax 함수

