---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: 신경망 Weight & Bias
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231214
tags: 신경망
lang: ko
---

## 1. Weight 와 Bias
![Image](/assets/images/ai/deeplearning/single_neural.png)

단일 뉴런 코드에서 다양한 가중치 값에서 출력을 확인해 본다.
```python
import numpy as np
import matplotlib.pyplot as plt

#input 값 배열로 저장
X = np.arange(-1.0, 1.0, 0.2)
Y = np.arange(-1.0, 1.0, 0.2)

#출력값 2차원 배열 생성
Z = np.zeros((10,10))

#두 입력값의 가중치
w_x = -2.5
w_y = -3.0

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
Z의 값은 x의 input과 y의 input 에 각 가중치를 곱한후 bias 의 결과를 최종 sigmoid 의 출력값이다.


### Weight 의 변화에 따른 출력값 변화
w_x = 2.5, w_y = -3.0

![Image](/assets/images/ai/deeplearning/single_neural_output.png){:width="400px" height="400px"}


w_x = -2.5, w_y = -3.0

![Image](/assets/images/ai/deeplearning/weight_1.png){:width="400px" height="400px"}

w_x = 0, w_y = 3.0

![Image](/assets/images/ai/deeplearning/weight_2.png){:width="400px" height="400px"}

w_x = 2.5, w_y = 0

![Image](/assets/images/ai/deeplearning/weight_3.png){:width="400px" height="400px"}
