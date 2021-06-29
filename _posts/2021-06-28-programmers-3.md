---
title: "[프로그래머스] 완주하지 못한 선수"
categories: programmers
tags: programmers python hash
published: true
---

## [프로그래머스] 완주하지 못한 선수

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42576)

---

### 풀이

문제 생략,  
이 문제는 공통 사람을 빼고 나머지 사람을 찾는 문제이다.  
그런데 문제는 set으로 받아서 푼다면, 중복은 1개로 치기 때문에 모두 뺐을 때 0이 나올 수 있다.  
따라서 set이 아닌 두 가지 방법으로 풀 수 있다.

```python
# 1. Counter()
from collections import Counter
def solution(participant, completion):
    part = Counter(participant)
    com = Counter(completion)
    part.subtract(com)
    return list(part)[0]
print(solution(["mislav", "stanko", "mislav", "ana"], ["stanko", "ana", "mislav"]))
```

```python
# 2. hash()
def solution(participant, completion):
    dic = {}
    temp = 0
    for part in participant:
        dic[hash(part)] = part
        temp += hash(part)
    for part in completion:
        temp -= hash(part)
    return dic[temp]
print(solution(["mislav", "stanko", "mislav", "ana"], ["stanko", "ana", "mislav"]))
```

---

### 실수 및 배운 점

set을 활용하려 했더니 중복은 적용이 안된다는 것을 다시 배우게 되었다.  
dict를 이용할 때,  
선언 : dic = {} / dic = dict()  
키값 : dic / dic.keys()  
값 : dic.values()  
이렇게 생각하자.

<br>

1. Counter()

   - Counter는 배열 (리스트, 튜플, 세트) 값들의 개수를 세어서 {'자료이름' : '개수'} 형태로 리턴한다.

   - Counter 객체끼리는 뺄셈이 가능하다. (C.substract(A)) -> C = C-A  
     '-'를 이용한 뺄셈을 하게 되면 음수 값이 표현이 안된다 !

   - Counter 는 value값에 0와 음수(minus)가 표현이 가능하다.

   - Counter에서 검색을 할 때, key값이 없을 경우 '0'으로 리턴한다.

   - Counter('key').most_common(n) 은 가장 많은 value를 가지고 있는 key값의 { key : value } 를 n개만큼 가져온다.

```python
from collections import Counter
array = [11,11,22,22,3,4,5]
c = Counter.array
print(c)
# Counter({11: 2, 22: 2, 3: 1, 4: 1, 5: 1})
```

2. hash()

   - hash()는 해당 값의 주소 값을 가져온다. dictionary에서 빠르게 비교할 때 쓰인다.

   - 같은 값이라면 자료형이 다르더라도 같은 주소 값을 가진다. (hash(1) = hash(1.0))

   - 값이 숫자라면 주소값 = 숫자로 표현된다.

   - 여기서는 중복을 고려해서 주소 값들을 모두 더하고 빼주는 것으로 나머지를 찾았다.

```python
array_3 = ["hi", "my", 2, 3]
D = {}
for i in range(len(array_3)):
    D[hash(array_3[i])] = array_3[i]
print(D)
# {864452902972903991: 'hi', -9128108481256874222: 'my', 2: 2, 3: 3}
```
