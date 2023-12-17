---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: 신경망 역전파(BackPropagation)
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231217
tags: 역전파
lang: ko
---
역전파(backpropagation)는 신경망을 학습 시킬 때 이용하는 알고리즘으로서 출력값과 접답의 오차를 네트워크에서 역전파시켜 네트워크의 가중치와 편향을 최적화 시킨다.
<!--more-->

## 1. 역전파란
순전파로 얻은 출력값과 정답과의 오차를 하나씩 층을 거슬러 올라가며 역방향으로 전파시킨다. 이때 전파시킨 오차에 근거해 각 층의 가중치와 편향의 수정량을 구한다.
이후 모든 층의 가중치와 편향을 조금씩 수정해 나간다. 이 과정을 반복하면 네트워크에서는 점차 오차를 최소화시키도록 최적화되어가는 학습이 진행된다.
학습에 성공한 네트워크는 임의의 입력값에 대해 유연하게 인지, 판단을 할 수 있게 된다.

## 2. 손실함수(loss function)
신경망의 출력값과 정답의 오차를 정의하는 함수를 손실함수(loss function)라고 한다. 오차는 정답과 출력값의 차이이다. 오차가 클수록 신경망이 바람직하지 않다는 의미이다.
학습은 이 오차를 최소화시키도록 진행이 되어야 한다.

### 오차제곱합(Sum of Squares for Error)

### 교차 엔트로피(Cross Entropy Error)

## 3. 경사 하강법(Gradient Method)
