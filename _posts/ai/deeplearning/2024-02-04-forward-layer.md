---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: 신경망 Forward Layer
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20240204
tags: forwarding layer
lang: ko
---
행렬를 통한 Forward Layer 에 대하여 기술한다. 
<!--more-->
![Image](/assets/images/ai/deeplearning/matrix_layer.png)
위 그림은 배치 학습과 미니 배치 학습에서 이용되는 행렬의 형식을 나타낸다. 각층으로의 입력, 각 층에서의 출력, 정답을 표현하는 3개의 행렬이 표시되어 있다.   
이 행렬에서 행 수는 배치 사이즈와 같고 각 열 수는 각 층으로의 입력 수와 출력 수, 정답 수이다. 출력 수는 층의 뉴런 수와 같다.   
예를 들어 배치 사이즈가 8, 입력수(앞 층의 뉴런 수)가 3이면 입력을 표현하는 행렬크기는 $$8 \times 3$$이 된다.   
배치 사이즈가 1, 층의 뉴런 수가 3이면 출력을 표시하는 행렬 크기는 $$1 \times 3$$ 이 되고 벡터와 같은 형태가 된다.

## 행렬을 이용한 순천파
순전파에서 행렬 곱으로 입력과 가중치 곱셈의 합을 구할 수 있다.   
뉴런 수가 n인 층에서 순전파를 생각하면 배치 사이즈를 h, 입력수(앞 측의 뉴런 수)를 m이라고 하면 입력을 표현하는 행력의 크기는 $$h \times m$$ 이 된다.
![Image](/assets/images/ai/deeplearning/forward_matrix.png)
각 원소가 입력과 가중치의 곱의 합이 되는 행렬을 구할 수 있다.   
이 행렬은 행 수가 배치 사이즈이고 열 수가 층의 뉴런 수가 된다. 이 행렬에 편향을 더하면 아래의 행렬이 된다.
![Image](/assets/images/ai/deeplearning/forward_matrix_bias.png)