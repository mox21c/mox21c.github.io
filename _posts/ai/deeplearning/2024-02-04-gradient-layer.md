---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: 신경망 역전파 - Layer Gradient
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20240204
tags: gradient layer
lang: ko
---



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

즉 가중치 기울기 $$\dfrac{\partial E}{\partial w_{jk}} 를 $$y_{j}$$ 와 $$\delta_{k}$$ 곱으로 표시할 수 있다.
![Image](/assets/images/ai/deeplearning/gradient-image-2.png)

### 3.2 출력층의 편향 기울기


## 4. 출력층에서 입력값 기울기