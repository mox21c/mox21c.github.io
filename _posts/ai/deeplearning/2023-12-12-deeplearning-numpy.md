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

## 1. 넘파이 배열
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
np.zeros((2,3))
np.ones(10)     #모든값이 1인 배열
np.ones((2,3))
np.random.rand(10)     #난수로 생성되는 배열
np.arrange(0, 1, 0.1)  #숫자 0~1까지 0.1 간격으로 배열 생성
np.linspace(0, 1, 11)  #숫자 0~1까지 원소수가 11개인 배열을 생성한다. 원소수 default = 50
```

## 2. 배열 변환
### reshape
배열의 형태를 변환한다.
```python
a = np.array([0,1,2,3,4,5,6,7])
b = a.reshape(2,4)  #a 배열을 (2,4) 형태의 배열로 변환한다.
b = np.reshape(a, (2,4))
c = b.reshape(2,2,2)  #(2, 2, 2) 형태의 3차원 배열로 변환
d = c.reshape(4,2)
e = d.reshape(-1)  #1차원 배열로 변환
```

## 3. 배열 연산
### 배열과 수치연산
```python
a = np.array([0,1,2,3,4,5]).reshape(2,3)
print(a)
[[0 1 2]
 [3 4 5]]

print(a+3)
[[3 4 5]
 [6 7 8]]

print(a*3)
[[0 3 6]
 [9 12 15]]
```
### 배열간 연산
```python
b = np.array([5,4,3,2,1,0]).reshape(2,3)
print(b)
[[5 4 3]
 [2 1 0]]

print(a + b)
[[5 5 5]
 [5 5 5]]

print(a * b)
[[0 4 6]
 [6 4 0]]
```
### 브로드캐스트
```python
a = np.array([[1,1], [1,1]])
b = np.array([1,2])

print(a + b)
[[2, 3]
 [2, 3]]

c = np.array([[1],[2]])
print(a + c)
[[2, 2]
 [3, 3]]
```

## 4. 배열 값 변경
```python
b = np.array([0,1,2],
             [3,4,5])

b[1,2] = 9
[[0,1,2],
 [3,4,9]]

c = np.array([0,1,2],
             [3,4,5],
             [6,7,8])
c[1] = np.array([9,10,11])
[[0,1,2],
 [9,10,11],
 [6,7,8]]
```
### 인덱스에 배열을 지정함
```python
e = np.zeros((3,3))
f = np.array([8,9])
e[np.array([0,2]), np.array([0,1])] = f
[[8,0,0],
 [0,0,0],
 [0,9,0]]

c = np.zerps(18).reshape(2,3,3)
[[[0,0,0]
  [0,0,0]
  [0,0,0]],
 [[0,0,0]
  [0,0,0]
  [0,0,0]]]

c[0,0:2, 0:2] = np.ones(4).reshape(2,2)
[[[1,1,0]
  [1,1,0]
  [0,0,0]],
 [[0,0,0]
  [0,0,0]
  [0,0,0]]]
```
## 5. transpose 메소드
```python
a = np.array([0,1,2],
             [3,4,5])
[[0 1 2],
 [3 4 5]]

print(a.transpose(1,0))
[[0 3],
 [1 4],
 [2 5]]

b = np.arange(12).reshape(2,2,3)
[[[0 1 2]
  [3 4 5]]

 [[6 7 8]
  [9 10 11]]]

b.transpose(1, 2, 0)
[[[0 6]
  [1 7]
  [2 8]]

 [[3 9]
  [4 10]
  [5 11]]]
```
