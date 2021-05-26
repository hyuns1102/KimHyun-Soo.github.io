---
title: "[이코테 2021] 알고리즘 경향 분석 및 파이썬 문법 - 3"
categories: codingtest
tags: python
published: true
---

## [이코테 2021] 알고리즘 경향 분석 및 파이썬 문법 - 3

> 모든 예시 코드는 Repl을 이용해서 확인해본다.

---

### 함수와 람다식

- 함수(Function)란 특정한 작업을 하나의 단위로 묶어 놓는 것
- 불필요한 소스코드의 반복을 줄인다.

- 함수의 종류

  - 내장 함수: 기본적으로 제공 함수
  - 사용자 정의 함수: 함수를 사용자가 직접 정의해서 사용한다.

- ex)

  ```python
  def 함수명(매개변수):
      실행할 소스코드
      return 반환 값
  ```

- 파라미터의 변수를 직접 지정 가능

  ```python
  def add(a,b):
      print('함수의 결과:', a+b)
  add(b=3, a=7)
  ```

- global 키워드 (전역변수) : 함수 내에서 선언해줘야 한다.
  - 가져온 상태에서 산술 연산 가능 / array가 생성되면 추가하는 것 가능

```python
a = 10
array = [1,2,3,4,5]
def func():
    global a, array
    a += 1
    array.append(6)
    print(a, array)

func()
```

- 파이썬은 함수 안에서 여러 개의 반환 값을 가질 수 있다.
  - 여러 개의 반환 값을 **Packing** 이라고 한다.
  - 반환 값을 차례 대로 받는 결과(a, b, c, d)를 **Unpacking**이라고 한다.

```python
def operator(a,b):
    add_var = a+b
    subtract_var = a-b
    multiply_var = a*b
    divide_var = a/b
    return add_var, subtract_var, multiply_var, divide_var

a, b, c, d = operator(5, 3)
print(a, b, c, d)
```

### 람다 표현식

- 함수를 더 간단하게 작성할 수 있다.

  - 특정한 기능을 수행하는 함수를 한 줄에 작성할 수 있다.
  - 예제는 같은 계산 과정을 가진 함수와 람다식이다.

  ```python
  def add(a,b):
    return a+b
    print(add(3,7))

  print((lambda a, b: a+b)(3,7))
  ```
