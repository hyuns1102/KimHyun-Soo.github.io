---
title: "[프로그래머스] 가장 큰 수"
categories: programmers
tags: programmers python sort
published: true
---

## [프로그래머스] 가장 큰 수

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42746)

---

### 풀이

가장 먼저 생각했던 풀이는 numbers 안에 값을 '문자열'로 취급해서 sort하는 방법을 생각했다.  
가장 앞자리가 높은 순으로 정렬 후 join으로 맞춰 만들려 했다.  
하지만 그 방법은 3, 30일 때, 30이 먼저 나오기 때문에 틀렸다. (코드 생략)
<br>
다음 방법은 permutations을 이용한 방법이었다.  
이 방법은 시간 초과가 떴다. 아무래도 numbers의 길이가 100,000이하 이기에  
모든 것을 순열로 리스트로 바꾸는 것 자체가 오래 걸릴 것이기 때문이다.
<br>
다음 방법은 lambda를 이용한 방법이다.(다른 사람 정답 봄)  
문자열로 취급한 값을 정렬할 때, key 값을 x\*3에서 비교하도록 만들었다.  
그 이유는 원소 하나당 1000이하의 수기 때문에 3000, 300을 비교할 때도 가능하기 때문이다.

```python
# 틀림
from itertools import permutations
def solution(numbers):
    res = []
    for i in range(len(numbers)):
        numbers[i] = str(numbers[i])
    res = list(permutations(numbers))
    for i in range(len(res)):
        res[i] = "".join(res[i])
    res  = sorted(res, reverse = True)
    return res[0]
```

```python
def solution(numbers):
    num = list(map(str, numbers))
    num = sorted(num, key= lambda x: x*3, reverse=True)
    return str(int("".join(num)))
```

---

### 실수 및 배운 점

- 실수했던 점은 key값을 제대로 이용하는 방법을 몰랐다는 것이다.  
  고민했는데 if문을 이용할 생각만 했다...  
  또 하나는 마지막 return 할 때, int, str을 안썼다.  
  그 예외는 0이 가장 앞에 나올 때가 생기기 때문인 것 같다.
