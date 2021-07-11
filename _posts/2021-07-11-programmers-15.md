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

여기서 중요한 점은 h는 논문의 갯수라는 점을 주의해야 한다.  
예를 들어, input=[22, 24] 일 때, output=[ 2 ] 가 된다.  
작은 인용 횟수부터 list의 길이와 비교한 후에, 인용 횟수가 일치하거나 클 때, 길이를 return 해준다.

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

- 음.. 문제 파악이 제대로 되지 않았다..  
  아직도 헷갈리는 느낌이다.
