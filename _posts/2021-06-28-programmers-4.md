---
title: "[프로그래머스] 네트워크"
categories: programmers
tags: programmers python DFS BFS
published: true
---

## [프로그래머스] 네트워크

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/43162)

---

### 풀이

문제는 컴퓨터가 서로 연결되어 있을 때, 네트워크의 개수를 파악하는 문제이다.  
dfs() 이용해서 하나의 노드가 가지고 있는 모든 컴퓨터의 정보를 따라간다.  
모두 다 따라갔다가 나오면 개수 한 개를 셀 수 있게 만든다.  
<br>
나의 솔루션은 2차원 배열 그대로 visit을 만들었지만,  
다른 사람 솔루션은 노드 자체에 접근만 하면 visit이 되기 때문에 1차원 배열로 만들었다.
<br>
bfs() 방법도 deque를 이용해서 만들어 봤다.

```python
# 1. dfs - my solution
import copy
def dfs(visit, com, n):
   visit[com][com] = 0
   for i in range(0, n):
       if visit[com][i] == 1:
           visit[com][i] = 0
           if visit[i][i] == 1:
               dfs(visit, i, n)

def solution(n, computers):
   answer = 0
   visit = copy.deepcopy(computers)
   for com in range(n):
       if visit[com][com] == 1:
           dfs(visit, com, n)
           answer += 1
   return answer

test1, test2 = 5, [[1, 0, 1, 1, 0, 0], [0, 1, 0, 0, 1, 1], [1, 0, 1, 1, 1, 1], [1, 0, 1, 1, 1, 1], [0, 1, 1, 1, 1, 1], [0, 1, 1, 1, 1, 1]]
print(solution(test1, test2))

```

```python
# 2. dfs - 다른 사람 솔루션
def dfs(visit, com, n, computers):
    visit[com] = True
    for i in range(n):
        if i != com and visit[i] == False and computers[com][i] == 1:
            dfs(visit, i, n, computers)

def solution(n, computers):
    answer = 0
    visit = [False for _ in range(n)]
    for com in range(n):
        if visit[com] == False:
            dfs(visit, com, n, computers)
            answer += 1
    return answer
```

```python
# 3 bfs
from collections import deque

def bfs(visit, com, n, computers, deq):
    deq.append(com)
    while len(deq) > 0:
        start = deq.popleft()
        visit[start] = True
        for i in range(n):
            if computers[start][i] == 1 and visit[i] == False:
                deq.append(i)

def solution(n, computers):
    answer = 0
    deq = deque()
    visit = [False for _ in range(n)]
    for com in range(n):
        if visit[com] == False:
            bfs(visit, com, n, computers, deq)
            answer += 1
    return answer

test1, test2 = 3, [[1, 1, 0], [1, 1, 1], [0, 1, 1]]
print(solution(test1, test2))
```

---

### 실수 및 배운 점

처음 문제를 풀 때 visit을 2차원 배열로 만들어서 풀었고, 반쪽만 점검해서 완성시켰다.  
하지만 '반쪽'만 점검한다는 것이 문제였다. 왜냐하면 노드는 무조건 순서대로 있는 것이 아니었기 때문이다.  
<br>
bfs에서는 deque를 이용해서 문제를 풀었다. 각 정보를 '깊이'가 아닌 너비를 고려해야 했기에  
큐에 넣어서 순서가 되면 꺼내 쓰는 방식을 썼다.  
<br>
방식을 예전에 썼던 방식이기에 기억해서 썼지만, 실전에 다가오면 자꾸 틀릴 기분이 든다.  
순서도를 파악해서 완벽하게 내 것으로 만들어야 하는 게 필요하다는 것을 느꼈다.  
<br>

> deque 는 좌우가 뚫리면서 이어져있을 수도 있는 queue라고 생각하자. (양방향 큐이자 선입선출의 방식을 사용한다.)  
> method는 다음과 같다.  
> deque.append(item) : item을 오른쪽에 넣는다.  
> deque.appendleft(item) : item을 왼쪽에 넣는다.  
> deque.pop() : 맨 오른쪽 item을 리턴하는 동시에 삭제한다.  
> deque.popleft() : 맨 왼쪽 item을 리턴하는 동시에 삭제한다.  
> deque.extend(array) : 맨 오른쪽에 리스트의 요소들을 순회하면서 추가한다.  
> deque.extendleft(array) : 맨 왼쪽에 리스트의 요소들을 순회하면서 추가한다.  
> deque.remove(item) : deque안에 item 요소를 삭제한다.  
> deque.rotate(num) : deque안에서 num만큼 회전시킨다. (양수 : 오른쪽 / 음수 : 왼쪽)
