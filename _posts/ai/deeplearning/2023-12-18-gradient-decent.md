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
오차를 차례 차례 이전 층으로 전파시켜 가중치와 편향을 조금씩 수정하면서 최적화하기 위해서 경사 하강법(fradient decent) 라는 알고리즘을 이용한다.
<!--more-->

## 1. 경사하강법
어떤 파라미터 $$x_{k}$$의 변화량에 대한 함수 $$y(x_{1},x_{2}, \cdot \cdot \cdot, x_{k}, \cdot \cdot)$$ 의 변화율, 즉 기울기 $$dy/dx_{k}$$ 를 구해 이 기울기에 따라 파라미터를 조정하고 y를 최정화하는 알고리즘을 경사법이라고 한다.
경사 하강법은 경사법의 한 종류로서 결과가 y의 최소값을 향해 내려가도록 파라미터 $$x_{k}$$를 변화시킨다.

역전파에서는 손실 함수로 구한 오차값을 기점으로 신경망의 반대 방향으로 가중치와 편향을 수정해 나가는데 이때 경사 하강법으로 수정량을 결정한다. 경사 하강법에서는 오차가 줄어들도록 신경망의 가중치와 오차를 조정한다.

![Image](/assets/images/ai/deeplearning/gradient_decent_graph.png)

그래프에서 x축은 가중치이고, y출력의 오차이다. 즉 가중치에 따라 오차가 변화는데 오차가 최소가 되는 방향으로 가중치를 변화시킨다. 신경망의 모든 가중치를 이 곡선에서 오차가 하강하도록 변화시키면 오차를 조금씩 줄여갈 수 있다.
이때 각 가중치의 변화량과, 편향의 변화량은 이 곡선의 기울기로 결정된다.

경사 하강법으로 가중치와 편향을 수정할 때 w를 가중치, b를 편향, E를 오차라고 하면 아래의 식으로 표현할 수 있다.

$$
w <- w - \eta\dfrac{\partial E}{\partial w}
$$

$$
b <- b - \eta\dfrac{\partial E}{\partial b}
$$

$$\eta$$ 는 학습률(learning rate) 라고 부르는 상수이다. 학습률은 학습의 속도를 결정하는 상수로 작으면 작을 수록 시간이 오래걸리고, 국소 최적해에 빠지는 문제가 발생한다.
반변 학습률이 너무 커도 오차가 수렴되기 때문에 어려운 문제가 발생한다. 이 때문에 효율적으로 전역 최적해에 도달하기 위해서 학습률을 적절하게 설정할 필요가 있다.

## 2. 기울기를 구하는 방법

![Image](/assets/images/ai/deeplearning/gradient-image-0.png)

이 신경망에는 입력층, 은닉층, 출력층의 3개 층이 있고, 은닉층과 출력층에 가중치와 편향이 있다. 입력층은 입력값을 받아 다음 층으로 전달하는 역할을 하고 가중치와 편향은 없다.
출력층에서는 오차를 이용해 가중치와 편향의 기울기를 구하고, 출력층으로 들어오는 입력값의 기울기도 오차를 이용해 구한다.

순전파는 각 층의 출력값을 전파시키지만, 역전파에서는 입력값 오차의 기울기를 전파시킨다. 은닉층에서는 이 값들을 받아 가중치 기울기와 편향 기울기, 은닉층으로 들어오는 입력층의 기울기를 구한다.

## 3. 출력층 기울기
$$w_{jk}$$ 를 출력증에서의 가중치, $$b_{k}$$를 편향, $$u_{k}$$를 가중치와 입력값 곱셉의 총합에 편향을 더한 값으로 표시한다.
가중치는 은닉층의 출력과 관련 있기 때문에 은닉층 뉴련의 출력은 $$y_{j}$$ 라고 표시하면 아래와 같은 그림이 된다.

![Image](/assets/images/ai/deeplearning/gradient-image-1.png)

### 3.1 출력층의 가중치 기울기
가중치의 기울기, 즉 오차를 가중치로 편미분한 값을 구할 수 있고 다음과 같이 표현할 수 있다.   

$$
\partial w_{jk} = \dfrac{\partial E}{\partial w_{jk}}
$$

가중치의 기울기는 연쇄 법직을 이용해 전개할 수 있다.   

$$
\partial w_{jk} = \dfrac{\partial E}{\partial w_{jk}} = \dfrac{\partial E}{\partial u_{k}}\dfrac{\partial u_{k}}{\partial w_{jk}}
$$

여기에서 우변의 $$\dfrac{\partial u_{k}}{\partial w_{jk}}$$ 부분은 분자가 은닉층에 있는 여러 뉴런의 출력값과 가중치의 곱의 합에 편향을 더한 것이다.    

$$
\begin{matrix}
\dfrac{\partial u_{k}}{\partial w_{jk}} &=& \dfrac{\partial(\sum_{q=1}^{m}y_{q}w_{qk}+b_{k})}{\partial w_{jk}} \\
&=& \dfrac{\partial}{\partial w_{jk}}(y_{1}w_{1k} + y{2}w_{2k} + \cdot \cdot \cdot + y_{j}w_{jk} + \cdot \cdot \cdot + y_{m}w_{mk} + b_{k}) \\  
&=& y_{j}
\end{matrix}
$$

편미분하므로 $$$w_{jk}$$ 가 곱해진 항 이외에는 모두 0이 된다.

(4)번 식의 우변 $$\dfrac{\partial E}{\partial u_{k}}$$ 부분은 출력층 뉴런의 출력을 $$y_{k}$$ 로 하는 연쇄 법칙에 따라 다음과 같이 식이 된다.

$$
\dfrac{\partial E}{\partial_{uk}} = \dfrac{\partial E}{\partial_{yk}}\dfrac{\partial_{yk}}{\partial_{uk}}
$$

즉 $$\dfrac{\partial E}{\partial_{uk}}$$ 부분은 오차를 출력층 뉴런의 출력으로 편미분한 것과 그 출력값을 $$u_{k}$$ 로 편미분한것의 곱이 된다.   
$$\dfrac{\partial E}{\partial_{yk}}$$는 손실 함수를 편미분해서 구할 수 있고, $$\dfrac{\partial_{yk}}{\partial_{uk}}$$ 는 활성화 함수를 편미분 해서 구할 수 있다.

$$
\delta = \dfrac{\partial E}{\partial_{uk}} = \dfrac{\partial E}{\partial_{yk}}\dfrac{\partial_{yk}}{\partial_{uk}}
$$


(4)번식을 정리하면

$$
\partial w_{jk} = y_{j}\delta_{k}
$$

![Image](/assets/images/ai/deeplearning/gradient-image-2.png)

### 3.2 출력층의 편향 기울기

## 4. 출력층에서 입력값 기울기


## 5. 은닉층 기울기

### 5.1 가중치 기울기


### 5.2 편향 기울기