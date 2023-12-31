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
Z의 출력값에 대해 설명하자면 검은색의 출력값은 0에 가깝고 흰색의 출력값은 1에 가까운 수이다.
Sigmoid 함수의 특성으로 보면 입력값이 작을 수록 출력값은 0에 가깝고, 입력값이 커지면 출력은 1에 가까워진다.

### Weight 의 변화에 따른 출력값
#### weight 점 대칭
w_x = 2.5, w_y = 3.0

![Image](/assets/images/ai/deeplearning/single_neural_output.png){:width="400px" height="400px"}

w_x = -2.5, w_y = -3.0

![Image](/assets/images/ai/deeplearning/weight_1.png){:width="400px" height="400px"}

위 두 출력값을 보면 결과가 반전된 상태로 볼수 있다. 즉 가중치 값은 특정 input 값의 영향력을 조정한다.
가중치가 0에 가까우면 영향력이 작게 되고, 0보다 커지면 영향력이 확대된다. 음수가 되면 영향력을 반대가 된다.

#### weight 가중치 0
w_x = 0, w_y = 3.0

![Image](/assets/images/ai/deeplearning/weight_2.png){:width="400px" height="400px"}

w_x = 2.5, w_y = 0

![Image](/assets/images/ai/deeplearning/weight_3.png){:width="400px" height="400px"}

첫번째 출력값은 x를 input 의 가중치를 0으로 만든 상태이고, 두번째 출력값은 y의 input의 가중치를 0으로 만든 상태이다.

### bias 의 변화에 따른 출력값
bias = -2.0

![Image](/assets/images/ai/deeplearning/bias_1.png){:width="400px" height="400px"}

bias = 0

![Image](/assets/images/ai/deeplearning/bias_2.png){:width="400px" height="400px"}

bias = 2.0

![Image](/assets/images/ai/deeplearning/bias_3.png){:width="400px" height="400px"}

bias는 전체 출력에 대한 민감도를 조정할 수 있다. 즉 bias는 뉴런이 흥분하기 쉬운 정도를 결정한다.
이 두개의 값(weight, bias) 를 적절하게 조정을 하여 좋은 결과를 도출 할 수 있다.
