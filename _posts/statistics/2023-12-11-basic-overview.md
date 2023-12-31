---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/statistics/statistics.png
title: 기초통계(overview)
sidebar:
  nav: doc-statistic-ko
aside:
  toc: true
key: 20231211
tags: 기초통계
lang: ko
---

`모집단`{:.success} `표본`{:.success} `Sampling`{:.success}

물가지수, 경제성장률 등 일상 생활에서 여러 가지 통계에 접하게 된다. 이러한 통계는 유용한 정보를 제공해주고 정책을 수립하거나, 계획 세우는데 중요한 역활을 한다.
하지만 통계자료가 잘못 작성되거나, 고의로 왜곡하여 사용되면 오히려 유해한 결과를 낳게 된다.

<!--more-->

## 1. 서론
### 모집단과 표본
- 모집단 : 연구 대상인 모든 가능한 관측값이나 측벙값의 집합을 말한다.
- 표본 : 통계적 처리를 위하여 모집단에서 실제로 추출한 관측값이나 측정값의 집합을 말한다.

예를들어 어느 공정에서 생상되는 전구의 수명을 검사하고자 할 때, 하나 하나의 전구(또는 전구의 수명)가 추출단위가 되며, 검사를 받기 위해 추출된 일부 전구의 수명이 표본이 된다. 공정에서 생상되는 모든 전구의 수명이 모집단이 된다.

### 자료
- 자료(data) : 실험이나 조사 등을 통해 얻어진 정보
- 관측개체(observation) : 측정값이 얻어지는 개체 (일반적으로 자료의 각 행에 표현)
- 변수 (variable) : 연구 대상 항목(일반적으로 자료의 각 열에 표현)

### 모수와 통계량
- 모수(parameter) : 모집단에 관한 숫자 요약
- 통계량(statistic) : 표본의 숫자 요약

## 2. 자료의 수집
### 자료의 수집
- 정확한 추정(estimation), 검정(testing)을 위해서는 적절한 방식으로 자료를 수집해야 한다.
- 자료의 수집에는 표본에 따른 변동성(variability) 및 측정에 따른 변동성이 존재한다.
- 모수에 대한 정확한 추론을 위해서는 모집단으로부터 표본을 Random Sampling 하는 것이 바람직하다.

### 표본조사
- 단순임의추출(simple random sampling) : 표본추룰 틀 내 모든 개체에게 동일한 추출 기회가 주어짐
- 군집표본추출(cluster random sampling) : 모집단을 군집으로 분류한 후 군집을 단순의의 추출하고 추출된 군집 내 개체들을 표본으로 사용함
- 층화표본추출(stratified random sampling) : 모집단을 층 내의 개체들은 상대적으로 동질적이고 다른 층의 개체들은 상대적으로 이질적이 되도록 층을 나눈 후 층 내에서 독립적인 표본추출을 함

![Image](/assets/images/statistics/sampling.png)

## 3. 자료의 정리
### 변수의 종류
- 범주형 변수(질적변수) : 자료가 가질 수 있는 값이 몇 개의 범주로 구성 됨
  - 명목형 변수 : 범주들이 순위 개념이 없음
  - 순서형 변수 : 범주들이 순위 개념이 있음
- 연속형 변수(양적변수) : 자료가 가질 수 있는 값이 수치적 의미를 지님

### 범주형 변수 요약
- 범주형 변수는 도수분포표(frequency table)로 요약 할 수 있다.
- 도수 : 범주형 자료의 경우 각 범주 별 빈도를 셀 수 있으면 이를 도수(frequency) 라 한다.
- 상대도수(relative frequency) : 도수를 전체 관측개체의 숫자로 나눈 값

[데이터]

![Image](/assets/images/statistics/frequency_data.png){:width="600px" height="200px"}

[도수 & 상대도수]

![Image](/assets/images/statistics/frequency.png){:width="400px" height="200px"}

### 연속형 변수의 요약
- 연속형 변수는 측정값을 대표할 수 있는 요약통계량(summary statistics)를 사용하여 요약함
- 요약통계량은 n개의 자료 $$x_{1}, x_{2}, .....x_{n}$$ 가 어떤 값을 중심으로 분포되어 있는지 위치 척도, 자료들이 산포되어 있는 정도를 나타내는 산포도 척도가 주로 사용됨
- 대표값
  - 평균
  $$
  \bar{x} = \dfrac{x_{1} + x_{2} + ... + x_{n}}{n}
  $$
  - 중위수 : 자료 $$x_{1}, x_{2}, .....x_{n}$$ 을 크기 순으로 나열했을 때 가장 중앙에 위치하는 값. 자료의 개수 n이 홀수일 때는 크기 순으로 나열했을 때 $$\dfrac{n+1}{2}$$ 번째인 값을 의미하고 n이 짝수일 때는 가장 중앙에 위치하는 두개의 값 ($$\dfrac{n}{2}$$번째 값과 $$\dfrac{n+1}{2}$$번째 값) 의 평균값으로 결정한다.
  - 최빈값 : 자료 $$x_{1}, x_{2}, .....x_{n}$$ 들 중 가장 빈도가 높은 값

![Image](/assets/images/statistics/distribution_graph.png)

- 산포도
  - 분산 : $$S^{2} = \dfrac{\sum_{i=1}^{n}()^{x_{i} - \bar{x}}2}{n-1}$$
  - 표준편차 : $$S = \sqrt{S^{2}} = \sqrt{\dfrac{\sum_{i=1}^{n}()^{x_{i} - \bar{x}}2}{n-1}}$$
  - 범위(range) : 최대값 (maximum value) - 최소값(minimum value)
  - 사분위범위(interquartile range, IQR) : $$Q_{4} - Q_{1}$$

[데이터]

![Image](/assets/images/statistics/frequency_data.png){:width="600px" height="200px"}

최소값 : 18
제 1 사분위수 : 19
제 2 사분위수(중위수) : 19.5
평균 : 22.03
제 3 사분위수 : 21
최댓값 : 55
최빈값: 19
분산 : 55.48
표준편차 : $$\sqrt{55.48}$$ = 7.647
범위 : 55-18 = 37
사분위범위 : 21 - 19 = 2
