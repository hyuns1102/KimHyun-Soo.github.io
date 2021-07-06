---
title: "[프로그래머스] 단어 변환"
categories: programmers
tags: programmers python dfs bfs
published: true
---

## [프로그래머스] 단어 변환

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/43163)

---

### 풀이

이 문제는 words 안에 있는 단어로 변환하면서 목표 단어까지 갈 수 있는 최단 길이를 찾는 문제이다.

탐색이 필요하기 때문에 dfs, bfs를 고려했고 먼저 bfs를 이용해서 문제를 풀었다.  
먼저 단어 변환 가능한 조건은 단어 중 문자 하나만 다를 때이다. 그래서 단어의 개수를 파악하는 Counter의 특성을 이용했다.  
현재 단어에서 다음 단어를 뺐을 때 길이는 1개만 남기 때문에, 1개였을 때 bfs에 들어갈 수 있도록 했다.  
그 후, list를 이용한 stack을 만들어서 bfs 방식을 따랐다. 만약, target과 now값이 같을 경우 최소 answer을 찾게 만들었다.

```python
from collections import Counter
def bfs(index, target, words):
    visit = [False] * len(words)
    visit[index] = True
    q = [[words[index], 1, visit]]
    answer = len(words)
    while q:
        now, ans, visit = q[0]
        q = q[1:]
        if now == target:
            answer = min(answer, ans)
        else:
            for i in range(len(words)):
                if visit[i] == True:
                    continue
                if len(Counter(words[i]) - Counter(now)) == 1:
                    visit[i] = True
                    q.append([words[i], ans+1, visit])

    return answer

def solution(begin, target, words):
    answer = len(words)
    if not target in words:
        return 0

    for index in range(len(words)):
        if len(Counter(words[index]) - Counter(begin)) == 1:
            answer = min(answer, bfs(index, target, words))

    return answer
```

---

### 실수 및 배운 점

- 단어가 한 개 차이일 때 bfs를 돌 수 있게 하는 방법을 찾느라 조금 생각했다. Counter를 이용해서 했지만, 다음엔 zip을 이용하는 방법도 고려해보자.
