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

검은색 출력값이 0, 즉 뉴련이 흥분하지 않은 상태를 나타내며, 흰색은 출력값 1, 즉 뉴런이 흥분한 상태를 나타낸다.
좌상단부의 검은색 영역, 즉 출력값이 0에 가까운 영역에서 우하단부의 흰색 영역, 출력값이 1에 가까운 영역까지의 출력값은 연속적으로 변화하고 있다.
활성화 함수로 시그모이드 함수를 이용했기 때문에 0과 1사이를 표현하는 이유로 나타나는 현상이다.

## 3 Layer Network(회귀)
![Image](/assets/images/ai/deeplearning/3_layer_network.png)

이 신경망은 입력층(뉴런수 : n=2), 은닉층(n=w), 출력층(n=1) 의 3층 구조이다. 은닉층의 활성화 함수는 sigmoid 함수이며 출력층의 활성화 함수는 회귀 문제에 적합한 항등함수이다.

### 각 층의 구현
#### 은닉층 구현
```python
def middle_layer(x,w,b):
    u = np.dot(x,w) + b
    return 1/(1+np.exp(-u))
```
이 함순느 은닉층으로 입력(x), 가중치(w) 와 편향(b)를 인수로 받는다.

$$
\vec{u}_{j} = \vec{x}_{j}W + \vec{b}_{j}
$$

계산된 값 u를 활성화 함수인 sigmoid 함수에 입력하고 은닉층의 출력값을 구할 수 있다.

#### 출력층 구현
```python
def output_layer(x, w, b):
    u = np.dot(x,w) + b
    return u
```
인수와 u의 계산은 은닉층과 같고 활성화 함수는 항등함수로 구현했다.

#### weight(가중치) 초기화
입력층의 뉴런 수는 2이고 중간층의 뉴런수는 2이므로, 은닉층에는 2$$\times$$2=4개의 가중치가 필요하다. 또한 은닉층의 뉴런 수는 2이고 출력층의 뉴런 수는 1이므로, 출력층에는 2$$\times$$1=2개의 가중치가 필요하다.
```python
# 은닉층 2*2 행렬
w_im = np.array([[4.0, 4.0],
                 [4.0, 4.0]])

# 출력층 2*1 행렬
w_mo = np.array([[1.0],
                 [-1.0]])
```

#### bias(편향) 초기화
편항 수는 뉴런의 수와 일치하므로 은닉층에는 2개, 출력층에는 1개의 편항이 필요하다.
```python
# 은닉층
b_im = np.array([3.0, -3.0])
# 출력층
b_mo = np.array([0.1])
```

### 전체 코드
```python
%matplotlib inline

import numpy as np
import matplotlib.pyplot as plt

X = np.arange(-1.0, 1.0, 0.2)
Y = np.arange(-1.0, 1.0, 0.2)

Z = np.zeros((10,10))

# 가중치
# 은닉층 2*2 행렬
w_im = np.array([[4.0, 4.0],
                 [4.0, 4.0]])

# 출력층 2*1 행렬
w_mo = np.array([[1.0],
                 [-1.0]])

# 편향
# 은닉층
b_im = np.array([3.0, -3.0])
# 출력층
b_mo = np.array([0.1])

def middle_layer(x,w,b):
    u = np.dot(x,w) + b
    return 1/(1+np.exp(-u))

def output_layer(x, w, b):
    u = np.dot(x,w) + b
    return u

for i in range(10):
    for j in range(10):

        # 순전파
        inp = np.array([X[i], Y[j]]) # 입력층
        mid = middle_layer(inp, w_im, b_im) # 은닉층
        out = output_layer(mid, w_mo, b_mo) # 출력층

        Z[j][i] = out[0]

plt.imshow(Z, "gray", vmin = 0.0, vmax = 1.0)
plt.colorbar()
plt.show()
```
![Image](/assets/images/ai/deeplearning/3_layer_network_result.png)
