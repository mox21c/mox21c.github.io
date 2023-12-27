---
layout: article
article_header:
  type: cover
  image:
    src: /assets/images/ai/nlp.png
title: 텍스트 전처리과정
sidebar:
  nav: doc-ai-ko
aside:
  toc: true
key: 20231227
tags: preprocessing
lang: ko
---
`텍스트 전처리`{:.success}

문서 혹은 텍스트는 프로그래밍 언어 안에서 문자열로 표현이 된다. 문장 혹은 문자열들은 각각의 단어들로 구성되어 있고 그 단어들의 순서에 따라 이해를 한다.
따라서 컴퓨터에게 어떤 문장을 이해시키려면 문장을 단어 단위로 나눈 후에 리스트 형태로 변환해 주어야 한다. 이 과정에서 쓸모 없는 문자들은 제거를 한다.

<!--more-->
## 1. 텍스트 전처리 단계


