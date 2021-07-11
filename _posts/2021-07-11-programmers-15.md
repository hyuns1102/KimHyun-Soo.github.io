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

문제가 너무 헷갈린다.  
h번 이상 인용된 논문이 h편 이상이고 나머지는 h번 이하일 때, h의 최댓값을 구하는 문제이다.

일단 sort를 이용한 후에

```python
# 틀림
def solution(citations):
    answer = 0
    citations = sorted(citations)
    for index, value in enumerate(citations):
        if (len(citations)-(index)) >= value and value >= index:
            answer = max(answer, value)

    return answer
```

```python
# 다른 사람 풀이
def solution(citations):
    citations.sort()
    for i, value in enumerate(citations):
        if value >= len(citations) - i:
            return len(citations) - i
    return 0
```

---

### 실수 및 배운 점

- 실수했던 점은 key값을 제대로 이용하는 방법을 몰랐다는 것이다.  
  고민했는데 if문을 이용할 생각만 했다...  
  또 하나는 마지막 return 할 때, int, str을 안썼다.  
  그 예외는 0이 가장 앞에 나올 때가 생기기 때문인 것 같다.
