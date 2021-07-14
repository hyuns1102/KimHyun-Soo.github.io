---
title: "[프로그래머스] H-index"
categories: programmers
tags: programmers python sort
published: true
---

## [프로그래머스] H-index

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42747)

---

### 풀이

h번 이상 인용된 논문이 h편 이상이고 나머지는 h번 이하일 때, h의 최댓값을 구하는 문제이다.

여기서 중요한 점은 h는 **논문의 갯수**라는 점을 주의해야 한다.  
예를 들어, input=[22, 24] 일 때, output=[ 2 ] 가 된다.  
작은 인용 횟수부터 list의 길이와 비교한 후에, 인용 횟수가 일치하거나 클 때, **길이**를 return 해준다.

(수정)  
즉, h의 최댓값을 가장 먼저 생각해보자.  
h의 최댓값을 m_h라 하면, m_h는 citations의 길이다.  
여기서 m_h보다 작은 인용횟수를 가진 논문이 있다면,  
m_h-1로 줄이고 citations에서 가장 적은 인용 횟수의 논문을 제외 시킨다.  
이렇게 하나씩 줄여가면서 인용 횟수와 논문의 최대 값이 같아질 때,  
논문의 최대값을 리턴하는 코드를 짠다면 아래와 같다.

```python
# 다른 사람 풀이
def solution(citations):
    citations.sort()
    for i, value in enumerate(citations):
        if value >= len(citations) - i:
            return len(citations) - i
    return 0
```

```python
def solution(citations):
    citations.sort(reverse = True)
    for index, value in enumerate(citations):
        if value < (index + 1):
            return index
    return len(citations)
```

```python
# 틀림
def solution(citations):
    citations.sort(reverse = True)
    for index, value in enumerate(citations):
        if index + 1 >= value:
            return value
    return answer
```

---

### 실수 및 배운 점

- 완전히 문제를 단순하게 봤다.  
  다시 보니, h의 가장 최대값을 고려하지 않고, value 값에만 집착해서  
  답을 찾지 못했다. 문제 해설도 보면서 제대로 이해되지 않았지만,  
  <br>
  h의 최대값을 고정시켜놓고, 이를 기준으로 줄여나가면서 로직을  
  봤더니 파악할 수 있었다.  
  <br>
  아직도 부족한게 많다...
