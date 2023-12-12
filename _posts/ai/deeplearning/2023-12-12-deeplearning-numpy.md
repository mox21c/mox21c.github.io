---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/deeplearning/deeplearning.png
title: Numpy(Deep Learning)
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231212
tags: numpy
lang: ko
---
numpy 는 파이썬의 확장 모듈로서 간단한 코드로 데이터를 효율적으로 처리할 수 있다.
다차원 배열을 충실하게 지원하며 내부는 C언어로 구현되어 있어 실행 속도가 빠르다. 또한 방대한 수학함수 라이브러리를 내장하고 있어 연산 기능이 충실하다.
딥러닝을 구현할 때는 벡터나 행렬을 자주 다루기 때문에 넘파이는 딥러닝에 매우 유용한 도구 이다.

<!--more-->

## 넘파이 배열
### 1차원 배열생성
```python
a = np.array([0,1,2,3,4,5])
```
### 2차원 배열생성
```python
b = np.array([0,1,2],[3,4,5])
```
### 3차원 배열생성
```python
c = np.array([[0,1,2],[3,4,5]],[[5,4,3],[2,1,0]])
```
### 배열의 형태와 원소수
```python
print(np.shape(c))
print(np.size(c))
-------------------------
(2,2,3)
12
```
### 배열을 생성하는 다양한 함수
```python
np.zeros(10)    #모든값이 0인 배열
np.ones(10)     #모든값이 1인 배열
np.random.rand(10)     #난수로 생성되는 배열
```
