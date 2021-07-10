---
title: "[프로그래머스] K번째 수"
categories: programmers
tags: programmers python sort
published: true
---

## [프로그래머스] K번째 수

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42748)

---

### 풀이

풀이는 조건 순서에 맞춰서 코드를 작성하면 된다.  
여기서 주의할 점은 리스트 인덱스와 매개 변수로 주어진 인덱스와 1씩 차이가 난다는 점이다.

```python
def solution(array, commands):
    answer = []
    for info in commands:
        s, e = info[0], info[1]
        answer.append(list(sorted(array[s-1:e]))[info[2]-1])
    return answer
```

---

### 실수 및 배운 점

- 너무 쉬운 문제였는 데, 파이써닉한 방법을 찾으려 해서 풀이가 늦었다.  
  파이써닉 하지 않더라도 다 만들어보고 줄여보는 방법을 찾아보자.
