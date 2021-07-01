---
title: "[프로그래머스] 등굣길"
categories: programmers
tags: programmers python dp
published: true
---

## [프로그래머스] 등굣길

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42898)

---

### 풀이

이 문제는 일정한 일반적인 dp문제와 마찬가지로 작은 해들의 합이 곧 최단 경로가 되는 문제이다.  
<br>
결국 2차원 dp를 만들어서 (1,1) 에서 1로 시작해서
좌측, 상측의 dp값을 더해 최단거리를 만들어주면 된다.  
<br>
어릴 때 했던 최단거리 문제와 같다.  
<br>
여기서 주의할 점은,, 좌표값이다 ! 문제에 나오는 좌표값이 코드에서 작성할 때와는 반대이기 때문이다!  
그림 그리면서 잘 생각해야 한다.

```python
def solution(m, n, puddles):
    answer = 0
    dp = [[0] * (m+1) for _ in range(n+1)] # for문 빼먹지 말자.

    for i in range(1, n+1):
        for j in range(1, m+1):
            # 좌표 값 잘보자. n은 y축(코드에선 x), m은 x축 (코드에선 y)
            if i == 1 and j == 1:
                dp[i][j] = 1
                continue
            if [j, i] in puddles: # 좌표값 위치, 물웅덩이 갯수 (문제파악)
                continue
            else:
                dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[n][m] % 1000000007
# 좌표값 위치, 1000000007 로 나눈 나머지는 효율성 검사 의심
```

---

### 실수 및 배운 점

- 실수했던 점이 너무 많아서 정말 내 자신이 미울 정도이다. 점화식도 다 구했고 모든 걸 다 해결했다고 생각했는데  
  결국 문제를 제대로 파악하지 않아서 생겼던 문제가 나왔다.

  1. **좌표값**  
     좌표값이 문제와 반대로 나와있다. 그래서 결과값을 구하는 데 자꾸 반대로 써서 index error 가 났다.  
     <br>
     puddles의 좌표도 마찬가지로 반대로 검사했다.

  2. **puddles 개수**  
     puddles가 한 개만 있는 줄 알고 좌표 값을 그대로 대입 시켰다.  
     파이썬의 특징을 이용하자..  
     `if [j,i] in puddles:`

  3. **1000000007 로 나눈 나머지**  
     dp에서 자주 있는 문제이다. 루프 안에 나머지를 찾지 말고 답에서 찾아서 효율성을 얻자.

  4. **for문**  
     가장 기본적인 문제이다. 2차원 배열을 만들 때! list comprehension 제대로 쓰자.

     `n = [[0] * m for _ in range(n)]`
