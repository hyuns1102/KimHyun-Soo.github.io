---
title: "[이코테 2021] 알고리즘 경향 분석 및 파이썬 문법 - 3"
categories: codingtest
tags: python
published: true
---

## [이코테 2021] 알고리즘 경향 분석 및 파이썬 문법 - 3

> 모든 예시 코드는 Repl을 이용해서 확인해본다.

---

### 함수

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

- 람다 표현식 예시-1

  ```python
  def add(a,b):
    return a+b

  print(add(3,7))

  print((lambda a, b: a+b)(3,7))
  ```

- 람다 표현식 예시-2 (조건있는 정렬을 수행할 때 쓰인다.)

  ```python
  array = [('a', 50), ('b', 32),('c', 74)]

  def my_key(x):
      return x[1]

  print(sorted(array, key=my_key))
  print(sorted(array, key=lambda x: x[1]))
  ```

- 람다 표현식 예시-3

  ```python
  list1 = [1, 2, 3, 4, 5]
  list2 = [6, 7, 8, 9, 10]

  result = map(lambda a, b: a+b, list1, list2)
  print(list(result))
  ```

### 실전에서 유용할 표준 라이브러리

> 내장함수 : 기본 입출력 ~ 정렬 함수까지 기본 함수 제공  
> itertools : 반복되는 형태의 데이터를 처리하기 위한 기능 제공  
> (순열과 조합 라이브러리는 코테에 자주 쓰인다!)
> heapq : 힙(heap) 자료구조를 제공합니다. - 우선순위 큐  
> bisect : 이진 탐색(Binary Search) 기능을 제공합니다.  
> collections : 덱(deque), 카운터(Counter)등의 자료 구조 포함  
> math : 필수적인 수학적 기능 제공  

- 자주 사용되는 내장함수

  - sum()
  - min(), max()
  - eval()
  - sorted()
  - sorted() with key, lambda

- 순열과 조합

  - 순열 : 순서를 고려해서 선택했을 때 (`permutations`)

  ```python
  from itertools import permutations

  data = ['A', 'B', 'C']

  result = list(permutations(data,3)) # 3개를 뽑는 순열의 수
  print(result)
  ```

  - 조합 : 순서를 고려하지 않고 선택했을 때 (`combinations`)

  ```python
  from itertools import combinations

  data = ['A', 'B', 'C']

  result = list(combinations(data,2)) # 2개를 뽑는 조합의 수
  print(result)
  ```

  - 중복 순열 & 중복 조합 (`product` & `combinations_with_replacement`)

  ```python
  from itertools import product # 중복 순열
  from itertools import combinations_with_replacement # 중복 조합

  data = ['A', 'B', 'C']

  result = list(product(data, repeat=2)) # 2개를 뽑는 모든 순열의 수 (중복)
  print(result)
  result = list(combinations_with_replacement(data, 2)) # 2개를 뽑는 모든 조합의 수(중복)
  print(result)
  ```

- Collections

  - Counter() : 리스트와 같은 반복 가능한(iterable) 객체가 주어졌을 때 <br>
    <U>내부의 원소가 몇 번씩 등장</U>했는지를 알려줍니다.
  - counter를 dict으로 호출하면 각각 중복 개수가 몇 개인지 알려줍니다.

  ```python
  from collections import Counter

  counter = Counter([1, 2, 3, 3, 2, 4, 1, 4])

  print(counter[3])
  print(counter[2])
  print(counter)
  print(dict(counter))
  ```

- math

  - 최대 공약수 & 최소 공배수 : gcd(a, b), lcm(a, b)

  ```python
  import math

  # def lcm(a, b):
  #     return a*b // math.gcd(a,b)
  # 최소 공배수는 두 수의 곱 나누기 최대 공약수

  a = 21
  b = 14

  print(math.gcd(a, b))
  print(math.lcm(a,b))
  ```
