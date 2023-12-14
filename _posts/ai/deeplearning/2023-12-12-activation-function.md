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

함수의 입력값 x 가 0 이하면 출력값은 0이되고, x 가 0보다 크면 y 는 1이 된다.

$$
y = \begin{cases} 0 & (x \leq 0) \\ 1 & (x > 0) \end{cases}
$$

계단 함수를 이용하면 뉴런의 흥분 상태를 0이나 1로 간단하게 표시할 수 있다. 간단하게 구현할 수 있지만 0과 1의 중간 상태를 나타낼 수 없다는 단점도 있다.
계단 함수는 신경망의 기원이 되는 퍼셉트론에서 이용이 되었다. 페셉트론은 신경망의 일종으로 생각할 수 있으며 모든 신호가 0 아니면 1로 표시되는 매우 간단한 네트워크이다.

## 2. 시그모이드 함수
![Image](/assets/images/ai/deeplearning/sigmoid_function.png)

함수의 입력값 x가 작을 수록 출력값 y는 0에 가깝게 되고, x 가 커지면 y는 1에 근접하게 된다. 시그모이드 함수는 자연상수 $$e$$의 거듭제곱을 표현하는 exp 를 이용해 나타낸다.

$$
y = \dfrac{1}{1+exp(-x)}
$$

x의 값이 음수방향으로 0에서 멀어지면 분모가 커지기 때문에 y는 0에 가까인 간다. 또한 x의 값이 양수방향으로 0에서 멀어지만 exp(-x)가 0에 근접하므로 y는 1에 가깝다.
시그모이드 함수는 0과 1의 중간 상태를 나타낼 수 있고, 이 함수의 장점 중 하나는 미분이 가능하다.

$$
y^{\prime} = (1-y)y
$$

## 3. tanh 함수
![Image](/assets/images/ai/deeplearning/tanh_function.png)
## 4. ReLU 함수
![Image](/assets/images/ai/deeplearning/relu_function.png)
## 5. Leaky ReLU 함수
![Image](/assets/images/ai/deeplearning/leaky_relu_function.png)
## 6. Softmax 함수
![Image](/assets/images/ai/deeplearning/softmax_function.png)
