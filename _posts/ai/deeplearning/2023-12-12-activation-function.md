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

하이퍼볼릭 탄젠트(hyperbolic tangent)는 -1과 1 사이에서 매끄러운 곡선으로 변화하는 함수이다. 곡선의 형태는 시그모이드 함수와 비슷한데 0을 중심으로 대칭 형태이기 때문에 밸런스가 좋은 활성화 함수이다.

$$
y = \dfrac{exp(x) - exp(-x)}{exp(x) + exp(-x)}
$$

## 4. ReLU 함수
![Image](/assets/images/ai/deeplearning/relu_function.png)

Rectified Linear Unit 는 램프 함수(ramp function)라고도 불린다.
x > 0 범위에서 우상향 방향으로 뻗어 올라가는 모양이 특징인 활성화 함수이다.

$$
y = \begin{cases} 0 & (x \leq 0) \\ x & (x > 0) \end{cases}
$$

함수의 입력값 x가 음수인 경우 함수의 출력값 y는 0이 되고, x가 양수인 경우 y는 x와 같은 값이 된다.

## 5. Leaky ReLU 함수
![Image](/assets/images/ai/deeplearning/leaky_relu_function.png)

$$
y = \begin{cases} 0.01x & (x \leq 0) \\ x & (x > 0) \end{cases}
$$

ReLU 그래프와 비슷한 듯 보이지만 x가 음수의 영역에서 그래프 직선이 조금 기울어져 있다.
ReLU에서는 출력이 0이 되어 더 이상 학습이 진행되지 않는 뉴런이 다수 발생하는 dying ReLU라는 현상이 알려져 있다.
Leaky ReLU는 x 가 음수인 영역에서 아주 자은 기울기를 만들어 이 dying ReLU 문제를 피할 수 있따.

## 6. Softmax 함수
![Image](/assets/images/ai/deeplearning/softmax_function.png)

활성화 함수의 출력값을 y 입력값을 x로 하고 같은 층의 뉴런의 수가 n이라면 한다면 SoftMax 함수는 아래와 같이 표현된다.

$$
y = \dfrac{exp(x)}{\sum_{k=1}^{n}exp(x_{k})}
$$

우변의 분모 $$\sum_{k=1}^{n}exp(x_{k}) \notag$$ 는 같은 층의 각 활성화 함수에 입력되는 $$x_{k} \notag$$ 를 $$exp(x_{k}) \notag$$로 계산해 더한 값이다.
또한 다음의 관계에서 표현되는 것처럼 같은 층의 모든 활성화 함수의 출력값을 더하면 1이 된다.

$$
\sum_{i=1}^{n}(\dfrac{exp(x_{l})}{\sum_{k=1}^{n}exp(x_{k}})) = \dfrac{\sum_{i=1}^{n}exp(x_{l})}{\sum_{k=1}^{n}exp(x_{k})} = 1
$$

지수함수 값은 보통 0보다 큰 특성이 있어서 식 (7)의 y 는 0 < y < 1 이 된다.
한 층에 여러 개의 뉴런이 있고 각 뉴런에서 활성화 함수를 통과한 값는 0에서 1 사이 이다. 이러한 이유로 softmax 함수 값은 분류 문제에서 각 뉴런이 측정 한 범주로 분류될 확률을 나타낼 때 쓰일 수 있다.
