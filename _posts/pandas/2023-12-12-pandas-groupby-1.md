---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/pandas/pandas.png
title: PANDAS GroupBY
sidebar:
  nav: doc-pandas-ko
aside:
  toc: true
key: 20231212
tags: pandas groupby
lang: ko
---

## PANDAS GROUPBY AGG #1
PANDAS
{: .label .label-blue}

GROUPBY
{: .label .label-green}

AGG
{: .label .label-green}

groupby 함수는 데이터를 그룹으로 분할하여 각 그룹별 집계를 한다.
{: .fs-6 .fw-300 }

## AGG(집계) 함수
groupby.agg() 함수는 `sum`, `min`, `max`, `mean`, `count`, `variance` 계산을 하고, agg 함수를 사용하였을 때 Return 값은 Dataframe, Series 의 두 가지 형태가 있다.

- Dataframe 를 리턴하는 방법
    - agg 함수에 dic or list 를 전달하면 된다. 또한 as_index 값을 사용하여 Dataframe 형태로 값을 return 받아 올 수 있다.
    - `as_index` : 기본적으로 groupby작업이 끝나면 pandas는 모든 그룹화 열을 인덱스에 넣는다. 이동작을 피하려면 .groupby 메서드의 as_index 매개변수를 False로 설정할 수 있다. agg 함수에 문자열을 넣어 Series를 반환해야 하지만 as_index=False를 옵션을 주어 Dataframe를 반환한다.

```python
(
     flights
     .groupby('AIRLINE')
     .agg({'ARR_DELAY':'mean'})
)

(
    flights
    .groupby(['AIRLINE'], as_index=False)
    ['DIST']
    .agg('mean')
    .round(0)
)
```

- Series 를 리턴하는 방법
  - agg 함수에 문자, numpy 사용하지 않고 함수 사용 한다.

```python
(
     flights
     .groupby('AIRLINE')
     .agg('mean')
)

(
    flights
    .groupby(['AIRLINE'])
    ['DIST']
    .agg(np.mean)
)

(
    flights
    .groupby(['AIRLINE'])
    ['DIST']
    .mean()
)
```

## AGG(집계) 함수 - 여러 개의 열 사용
```python
(
     flights
     .groupby(['AIRLINE','WEEKDAY'])
     ['CANCELLED']
     .agg('sum')
)
```
![groupby_1](/assets/images/pandas/groupby_agg_1_agg_1.png)
```python
(
     flights
     .groupby(['AIRLINE','WEEKDAY'])
     [['CANCELLED','DIVERTED']]
     .agg(['sum','mean'])
)
```
![groupby_2](/assets/images/pandas/groupby_agg_1_agg_2.png)
```python
(
     flights
     .groupby(['ORG_AIR','DEST_AIR'])
     .agg(
        {
            'CANCELLED':['sum','mean','size'],
            'AIR_TIME':['mean','var'],
        }
     )
)
```
![groupby_3](/assets/images/pandas/groupby_agg_1_agg_3.png)

## Named Agg - 네임드 집계
데이터를 집계한 후 column 명을 자유롭게 하고 열을 펼치게 한다.
```python
(
     flights
     .groupby(['ORG_AIR','DEST_AIR'])
     .agg(
        sum_cancelled=pd.NameAgg(column='CANCELLED', aggfunc='sum'),
        mean_cancelled=pd.NameAgg(column='CANCELLED', aggfunc='mean'),
        size_cancelled=pd.NameAgg(column='CANCELLED', aggfunc='size'),
        mean_air_time=pd.NameAgg(column='AIR_TIME', aggfunc='mean'),
        var_air_time=pd.NameAgg(column='AIR_TIME', aggfunc='var'),
     )
)
```
![named_agg](/assets/images/pandas/groupby_agg_1_named_agg_1.png)

위 그림을 보면 열이 펼쳐져 있는것을 볼 수 있다.
## to_flat_index
named agg 를 사용하지 않고 여러 열이 겹칠 때 to_flat_index 함수를 사용하요 열을 펼칠 수 있다.
```python
res = (
     flights
     .groupby(['ORG_AIR','DEST_AIR'])
     .agg(
        {
            'CANCELLED':['sum','mean','size'],
            'AIR_TIME':['mean','var'],
        }
     )
)
res.columns = ['_'.join(x) for x in res.columns.to_flat_index()]
res
```
코드가 이쁘게 보이지 않아 pipe() 함수를 사용하여 보다 보기 간단하게 정리를 한다.
```python
def flatten_cols(df):
    df.columns = ['_'.join(x) for in df.columns.to_flat_index()]
    return df

res = (
     flights
     .groupby(['ORG_AIR','DEST_AIR'])
     .agg(
        {
            'CANCELLED':['sum','mean','size'],
            'AIR_TIME':['mean','var'],
        }
     ).pipe(flatten_cols)

res
```
pandas 는 여러 열로 그룹화 할 때 계층적 인덱스나 다중 인덱스를 만든다는 것을 명심하자.

## 카티션 곱
그룹별로 분류할 열중 하나가 범주형(object 형식이 아닌 category 형식인 경우 pandas 는 모든 조합의 카티션 곱을 만든다.
```python
res = (
     flights
     .assign(ORG_AIR=flights.ORG_AIR.astype('category'))
     .groupby(['ORG_AIR','DEST_AIR'])
     .agg(
        {
            'CANCELLED':['sum','mean','size'],
            'AIR_TIME':['mean','var'],
        }
     )

res
```
![cartesian](/assets/images/pandas/groupby_agg_1_cartesian.png)

## 카티션 곱 해결 - observe
카티션 곱은 조합에 따른 폭발 문제를 발생할 수 있다. 이를 해결하기 위해서 observe = True 매개변수를 사용하여 해결할 수 있다.
```python
res = (
     flights
     .assign(ORG_AIR=flights.ORG_AIR.astype('category'))
     .groupby(['ORG_AIR','DEST_AIR'], observe = True)
     .agg(
        {
            'CANCELLED':['sum','mean','size'],
            'AIR_TIME':['mean','var'],
        }
     )

res
```
