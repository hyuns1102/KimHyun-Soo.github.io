---
title: "[프로그래머스] 여행경로"
categories: programmers
tags: programmers python dfs
published: true
---

## [프로그래머스] 여행경로

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/43164)

---

### 풀이

여행을 갈 수 있는 티켓이 `[출발지, 도착지]` 형태로 주어졌을 때, 방문한 공항 경로를 배열에 담아 리턴한다.  
가능한 도착 경로가 2개 이상일 때, 알파벳 순으로 경로를 return 한다.

먼저 배열을 dict형식으로 출발지, 도착지 형태로 받는다. 그리고 이 dict 내에서 알파벳 순으로 정렬한다.  
그 후, dfs를 이용해서 도착지에 왔을 때, 그 다음 출발 티켓이 없거나 출발 티켓의 도착지가 없을 경우,  
path에 쌓는다. 그렇지 않다면, stack에 도착지를 쌓아준다.

stack의 맨 윗부분(top)에 대해서 계속 확인해주면서 스택을 관리한다.

```python
def graph_init(tickets):
        routes = dict()
        # 출발지 : 도착지1, 도착지2 ... 순으로 그래프를 만들어준다.
        for key, value in tickets:
            routes[key] = routes.get(key, []) + [value]
        return routes

def dfs(routes, start):
        stack = [start]
        path = []
        while stack:
            top = stack[-1] # 스택의 맨 윗부분 (마지막 도착지) 에 대해 가져온다.
            if top not in routes or len(routes[top]) == 0: # 도착지를 출발로 하는 티켓이 없거나, 출발로 하는 티켓의 도착지가 없을 때
                path.append(stack.pop()) # 경로에 추가
            else:
                stack.append(routes[top].pop(0)) # 도착지를 출발로 하는 티켓이 있다면, 티켓에서 제거(pop) 후 stack에 쌓아 마지막 도착지(출발지)로 둔다.
        return path[::-1] # 쌓은 path를 역순으로 return 한다.

def solution(tickets):
    routes = graph_init(tickets)
    for r in routes:
        routes[r] = sorted(routes[r])

    return dfs(routes, "ICN")
```

---

### 실수 및 배운 점

- 생각보다 어려웠던 문제였다. stack을 이용한 dfs가 가장 직관적이면서 보기 편했던 것 같다.  
  처음엔 bfs를 이용해서 풀 수 있지 않을까 했지만, 예외가 생겼다.  
  ticket  
  "ICN" -> "AAA"  
  "ICN" -> "BBB"  
  "BBB" -> "ICN"  
  이와 같은 경우일 때, bfs로 짠 코드는 AAA에서 멈추고, BBB를 가지 않았다.  
  이 경우를 어떻게 해결할까 했지만, 결국 stack을 이용해서 path에 저장해야 했다.  
  구글링을 통해 답을 보았고, dict, stack, path를 통해 자신이 최소로 지나올 수 있는 곳은 모두 path에 담아 역으로 출력하는 방법을 알았다.  
  이해하는 데 오래 걸렸지만, 새로운 방법을 배울 수 있었다.

- 배웠던 부분

  1. dict : 출발지 : 도착지1 도착지2 ... 배열로 만들어준다.  
     `routes[key] = routes.get(key, []) + [value]` 여기서 get(key, []) 는 key가 없을 때, default 값은 [] 이것으로 나타낸다는 뜻이다.  
     이를 설정해주지 않는다면 None이 뜬다. 즉, key Error는 존재하지 않는다.
  2. stack : 들렸던 곳을 모두 쌓아놓는다. 들렸던 곳에서 가장 top에 있는 도착지를 탐색한다.
  3. path : top이 티켓에 없을 때, 최종 도착지로 쌓는다.

- 못가는 티켓이 없기 때문에 모든 여행지의 최단 경로를 먼저 path에 쌓는 방법으로 최적의 경로를 찾는 것 같다.
