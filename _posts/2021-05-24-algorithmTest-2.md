---
title: "[이코테 2021] 알고리즘 경향 분석 및 파이썬 문법"
categories: codingtest
tags: python
published: true
---

## [이코테 2021] 알고리즘 경향 분석 및 파이썬 문법 - 2

> 모든 예시 코드는 Repl을 이용해서 확인해본다.

---

### 사전 자료형

- 사전 자료형은 키(Key)와 값(Value)의 쌍을 데이터로 가지는 자료형
- **변경 불가능한 자료형**을 키로 사용할 수 있습니다.
- hash table로 불린다.
- 데이터의 조회 시간 복잡도가 O(1)으로 list보다 효율적이다.
- **중괄호를 이용한다. {} (초기화 가능)**

```python
data = dict()
data['사과'] = 'Apple'
data['바나나'] = 'Banana'
data['코코넛'] = 'Coconut'

key_list = data.keys()
value_list = data.values()

print(key_list)
print(value_list)       # dict_list 형태로 출력

print(list(key_list))
print(list(value_list)) # 리스트 형식으로 출력

b = {
    '홍길동' : 97,
    '이순신' : 98
}                       # 중괄호로 만들어주는 것 가능

print(b)
print(b['이순신'])      # 특정 key 값 출력 가능

for key in key_list:
    print(data[key])    # key값을 출력
```

### 집합 자료형

- 중복 허용 x / 순서 x
- 집합은 리스트 혹은 문자열을 이용해서 초기화 가능합니다.
  - 이때 set() 함수를 이용합니다.
- 중괄호({})안에 각 원소를 콤마(,)를 기준으로 구분하여 삽입함으로써 초기화 할 수 있습니다.
- 데이터의 조회, 수정에 있어서 O(1)의 시간 복잡도를 가집니다.

```python
data = set([1, 1, 2, 3, 4, 4, 5]) # 중복 숫자들은 하나만 나오게 된다.
print(data)

data = {1, 1, 2, 3, 4, 4, 5} # 중괄호로 표현 가능
print(data)
```

- 집합 자료형의 연산
  - 합집합(|) , 교집합(&) , 차집합(-)

```python
data = set([1,2,3])
print(data)

data.add(4)         #새로운 원소 추가
data.update([5, 6]) #새로운 원소 여러개 추가
data.remove(3)      #특정 원소 삭제
```

### 사전 자료형 & 집합 자료형의 특징

- 리스트나 튜플은 순서가 있기 때문에 인덱싱을 통해 자료형의 값을 얻을 수 있습니다.
- 사전 자료형과 집합 자료형은 순서가 없기 때문에 인덱싱으로 값을 얻을 수 없습니다.
  - 사전의 키(Key) 혹은 집합의 원소(Element)를 이용해 O(1)의 시간 복잡도로 조회합니다.

### 기본 입출력

- input() 한 줄의 문자열을 입력 받는 함수
- map() 함수는 리스트의 모든 원소에 각각 특정한 함수를 적용할 때 사용

```python
n = input()
data = list(map(int, input().split()))

print(n)
print(data)
```

빠르게 입력을 받으려면?

```python
import sys

data=sys.stdin.readlin().rstrip()
print(data)
```

표준 출력 방법?

```python
a = 1
b = 2
print(a, b)       # 공백 두고 출력
print(7, end=" ")
print(8, end=" ") # 자동 줄바꿈 방지
```

f-string?

```python
answer = 8
print(f"정답은 {answer} 입니다.")
```

### 조건문 & 반복문

- 파이썬에서는 코드의 블록(Block)을 들여쓰기(Indent)로 지정합니다.

```python
score = 85
if score >= 70:
  print('hi')     #조건이 맞으면 실행된다.
  if score >= 90:
    print('bye')
else:
  print("힘내!")
print("bybey !!") # 무조건 실행된다.
```

- *공백 문자 4개를 이용해서 들여쓰기*를 하자!

- if ~ elif ~ else

```python
a = 5

if a >= 0:
    print("a>=0")
elif a >= -10:
    print("0> a >= -10")
else:
    print("-10 > a")
```

### 연산자

- 비교 연산자, 논리 연산자(and, or, not) 사용 가능
- in 연산자와 not in 연산자
  - 리스트, 튜플, 문자열, 딕셔너리 모두 사용 가능

### pass 키워드

- C++의 coninue랑 비슷하다. 조건 안에서 무시한다.

```python
a = -5

if a >= 0:
    print("a>=0")
elif a >= -10:
    pass
```

### 부등식

- 대수학의 부등식을 그대로 사용할 수 있습니다.

```python
a = -5

if -10 <= a < 20:
    print("hi")
elif 20<= a and a < 25:
    print("bye")
else:
    print("good")
```
