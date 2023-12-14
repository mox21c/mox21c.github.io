---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: 단순 신경망 구현
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231214
tags: 신경망
lang: ko
---

## 1. 단일 뉴런 구현
![Image](/assets/images/ai/deeplearning/single_neural.png)

Input 값 두개를 이용하여 단일 뉴런의 출력을 계산한다.
```python
import numpy as np
import matplotlib.pyplot as plt

#input 값 배열로 저장
X = np.arange(-1.0, 1.0, 0.2)
Y = np.arange(-1.0, 1.0, 0.2)

#출력값 2차원 배열 생성
Z = np.zeros((10,10))

#두 입력값의 가중치
w_x = 2.5
w_y = 3.0

#편향
bias = 0.1

for i in range(10):
    for j in range(10):
        #입력과 가중치 곱의 합 + 편현
        u = X[i]*w_x + Y[j]*w_y + bias

        #출력값으로 저장
        y = 1/(1 + np.exp(-u))  #sigmoid 함수
        Z[j][i] = y
```
위 코드에서 입력과 가중치 곱의 합의 수식은 아래와 같다
```python
u = X[i]*w_x + Y[j]*w_y + bias
```
$$
u = \sum_{k=1}^{n}(x_{k}w_{k}) + b
$$

단일 신경망을 거치지 않은 input에 대한 출력을 시각화 하면 아래의 그립과 같다.

![Image](/assets/images/ai/deeplearning/origin_output.png)

또한 단일 신경망를 거친 input에 대한 출력을 시각화 하면 아래의 그림과 같다.

![Image](/assets/images/ai/deeplearning/single_neural_output.png)

검은색 출력값이 0, 즉 뉴련이 흥분하이 않은 상태를 나타내며, 흰색은 출력값 1, 즉 뉴런이 흥분한 상태를 나타낸다.
좌상단부의 검은색 영역, 즉 풀력밧이 0에 가까운 영역에서 우하단부의 흰색 영역, 즉 풀력값이 1에 가까운 영역까지의 풀력값은 연속적으로 변화하고 있다.
활성화 함수로 시그모이드 함수를 이용했기 때문에 0과 1사이를 표현하는 이유로 나타나는 현상이다.


