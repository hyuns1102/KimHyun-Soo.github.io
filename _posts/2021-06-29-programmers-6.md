---
title: "[프로그래머스] 소수찾기"
categories: programmers
tags: programmers python
published: true
---

## [프로그래머스] 소수찾기

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42839)

---

### 풀이

숫자가 적혀있는 종이가 주어졌을 때, 모든 조합을 고려하여 소수의 개수를 찾는 문제이다.  
(11과 011은 같은 숫자로 취급)  
생각해야할 점은

1. 순서를 고려하고 조합을 찾아야 한다.
2. 그 숫자가 소수인지 파악해야한다.
3. 중복이 있을 경우 제외한다.

첫번째 순서를 고려하여 조합을 찾는 방법은 permutation을 이용.  
두번째 소수인지 파악하는 방법은 0, 1을 제외한 수의 제곱근까지 모든 수를 나눈다.  
세번째 중복 제외는 set을 이용한다.

```python
from itertools import permutations
import math

def find_prime(n):      # 소수 찾는 방법
    if n==0 or n ==1:
        return False
    else:
        for i in range(2, int(math.sqrt(n) + 1)):
            if n % i == 0:
                return False
        return True
def solution(numbers):
    answer = []
    for idx in range(1, len(numbers)+1):
        arr = list(permutations(numbers, idx))  # permutations : 순서를 고려하고 만드는 순열 (튜플)
        for j in range(len(arr)):
            num = int("".join(arr[j]))   # join : 문자열이 나뉘어졌을 때 하나로 붙여줌
            if find_prime(num) == True:
                answer.append(num)

    answer = list(set(answer))
    return len(answer)

print(solution("17"))       # result : 3
print(solution("011"))      # result : 2
```

---

### 실수 및 배운 점

- 조합을 만들 때, dfs()를 이용해서 모든 수를 검사하려고 했다. 근데 왜 안되지?  
  하나씩 도달할 때 문자열이 소수인지 판별한 다음에 그 다음 수를 조합해서 검사한다.. 다시 해봐야겠다.

- 순열 조합을 만드는 것은 permutation(items, number) 을 이용해서 만들자. 순서를 고려해서 만드는 조합이다.  
  (1,2) 와 (2, 1) 은 다르다.

- 새로 배웠던 것은 **join** 이다. [str.join](https://docs.python.org/3/library/stdtypes.html?highlight=str%20join#str.join) 은  
  iterable한 객체의 문자열을 str의 구분자와 함께 결합시켜주는 것이다.  
  iterable : list, set, dict, str, tuple, bytes, range 처럼 반복해서 접근 가능한 객체를 뜻한다.

- set은 중복된 문자열을 하나의 문자열로 바꿔준다.
