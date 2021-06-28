---
title: "[네이버 부스트 캠프] AI Pre Course"
categories: codingtest
tags: python
published: true
---

## Python Data Structure & Pythonic Code

---

> 스택 & 큐  
> 튜플 & 집합  
> 사전  
> Collection 모듈

## Python Data Structure

### 스택

- 나중에 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- LIFO
- Push Pop

### 큐

- 먼저 넣은 데이터를 먼저 반환하도록 설계된 메모리 구조
- FIFO
- Stack과 반대

### 튜플

- 값의 변경이 불가능한 데이터
- 선언 시 "[]" 가 아닌 "()"를 사용
- 리스트의 연산, 인덱싱, 슬라이싱 등을 동일하게 사용

  <br>

  왜 쓸까?

- 프로그램을 작동하는 동안 변경되지 않은 데이터의 저장
  ex) 학번, 이름, 우편변호 등
- 사용자에 실수에 의한 변경을 없애기 위해서
- t=(1, ) 이렇게 쓰기

### 집합(set)

- 값을 순서없이 저장, 중복 불허 하는 자료형
- set 객체 선언을 이용하여 객체 생성
- 선언 시 "{}" 나 set( ~~ ) 으로 사용
- 수학에서 사용하는 기본적인 집합연산 가능  
   : intersection / difference / Union /

### 사전(dictionary)

- 데이터를 저장 할 때는 구분 지을 수 있는 값을 함께 저장
  예) 주민 번호, 모델 번호
- 구분을 위한 데이터 고유 값을 Identifier 또는 Key 라고 함.
- Key 값을 활용하여, 데이터 값(Value)를 관리함.
- 선언 시 "{key : value}" 나 dict( ~~ ) 로 사용

### collections

- List, Tuple, DIct에 대한 Python Built-in 확장 자료 구조 (모듈)
- 편의성, 실행 효율 등을 사용자에게 제공함

```python
from collections import deque
from collections import Counter
from collections import OrderDict
from collections import defaultdict
from collections import namedtuple
```

deuqe

- Stack과 Queue 를 지원하는 모듈
- List에 비해 효율적인=빠른 자료 저장 방식을 지원함
- rotate, reverse 등 Linked List의 특성을 지원

defaultDict

- 하나의 지문에 같은 문제가 몇 개나 들어있는지 검사할 때 쓰일 수 있다.
- dict로 값을 찾을 때, 없다면 error가 뜸. 그 초기값을 만들어주는 것이다.

Counter

- Set의 연산들을 지원한다.
- Set에서 키 값들의 갯수를 찾을 때 쓰인다.

namedtuple

- Tuple 형태로 Data 구조체를 저장하는 방법
- 저장되는 data의 variable을 사전에 지정해서 저장함.
