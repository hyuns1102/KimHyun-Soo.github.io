---
title: "[프로그래머스] 타겟 넘버"
categories: programmers
tags: programmers python DFS BFS
published: true
---

## [프로그래머스] 타겟 넘버

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/43165)

---

<br/><br/>

---

### 풀이

문제 생략,  
이 문제는 dfs를 활용하여 조합을 target number에 맞는 수를 찾는 문제이다.  
+, -를 이용해서 target number에 도달하는 경우의 수를 구하는 것이므로  
+, - 각각의 경우의 재귀함수를 이용해서 마지막까지 도달했을 때, target number와 일치하면  
answer에 1을 더 해준다.  
다음과 같은 로직을 생각해서 코드를 짜주면 다음과 같다.

```python
answer = 0
def dfs(numbers, target, index, res):
    if len(numbers)-1 == index:
        if res == target:
            global answer
            answer += 1
        return
    index += 1
    dfs(numbers, target, index, res + numbers[index])
    dfs(numbers, target, index, res - numbers[index])
    return

def solution(numbers, target):
    dfs(numbers, target, 0, numbers[0])
    dfs(numbers, target, 0, -numbers[0])
    return answer

```

```python
# 다른 사람 정답

def solution(numbers, target):

    if not numbers and target == 0:
        return 1
    elif not numbers:
        return 0
    return solution(numbers[1:], target + numbers[0]) + solution(numbers[1: ], target - numbers[0])
```

---

### 실수했던 점

조합을 찾아야 한다는 생각에 combinations에 매달려 있었다.  
그런데 combinations에서 안되었던 점은 tuple이라는 특성 때문에 변경이 불가했다.  
여기서 계속 빠져있었기에 탐색을 써야한다는 생각을 아예 하지 못했던 것 같다.  
다른 사람의 풀이를 보면서 논리만 제대로 이해한다면 효율적으로 코드를 짤 수 있다고 생각했다.  
실천해야겠다.  
다양하게 많이 생각해야겠다.
