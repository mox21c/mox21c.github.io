---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: 신경망 역전파 - 경사 하강법
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231218
tags: 경사하강법
lang: ko
---

## 1. 경사하강법
오차를 차례 차례 이전 층으로 전파시켜 가중치와 편향을 조금씩 수정하면서 최적화하기 위해서 경사 하강법(fradient decent) 라는 알고리즘을 이용한다.
<!--more-->

### 경사하강법 개용
어떤 파라미터 $$x_{k}$$의 변화량에 대한 함수 $$y(x_{1},x_{2}, \cdot \cdot \cdot, x_{k}, \cdot \cdot)$$ 의 변화율, 즉 기울 $$dy/dx_{k}$$


