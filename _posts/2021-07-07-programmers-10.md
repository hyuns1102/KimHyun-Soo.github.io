---
title: "[프로그래머스] 정수 삼각형"
categories: programmers
tags: programmers python dp
published: true
---

## [프로그래머스] 정수 삼각형

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/43105)

---

### 풀이

이 문제는 현재 위치에서 좌 우 아래로 내려가면서 수를 더할 때, 최대 값을 구하는 문제이다.

먼저, 이 문제를 탐색을 활용해서 풀수 있으나 높이가 500까지 가고, 정수 값 또한 9999 이하의 정수이기 때문에  
연산 과정이 많아질 것 같았다.  
그래서 메모이제이션을 이용한 dp 방법을 이용했다.  
현재 층에서 첫째 번과 가장 끝 번은 자신의 바로 위에 결과값과 현재 자신의 값으로 이루어져 있다.  
그 이 외의 값들은 각 위 층의 좌, 우 번째 값들의 최대 값을 더해준다.  
<br>

점화식으로 나타내면, 다음과 같다.

```python

if k == 0 or k == len(dp[i])
dp[i][0] = dp[i-1][0] + a[i][0]
dp[i][n-1] = dp[i-1][n-2] + a[i][n-2]

else
dp[i][j] = max(dp[i-1][j-1], dp[i-1][j]) + a[i][j]

```

위의 점화식을 코드로 옮기면 다음과 같다.

```python
def solution(triangle):
    answer = 0
    dp = []
    for i in range(len(triangle)):
        dp.append([0] * (i+1))


    dp[0][0] = triangle[0][0]

    for i in range(1, len(dp)):
        for j in range(len(dp[i])):
            if j == 0:
                dp[i][j] = dp[i-1][j] + triangle[i][j]
            elif j == len(dp[i]) - 1:
                dp[i][j] = dp[i-1][j-1] + triangle[i][j]
            else:
                dp[i][j] = max(dp[i-1][j-1], dp[i-1][j]) + triangle[i][j]


    return max(dp[len(dp) - 1])
```

---

### 실수 및 배운 점

- 맞혔지만, 실수했던 것을 못봤던 점은  
  첫째, 마지막째 값들에 대해 현재 값을 잘 더해줬지만 나머지 값들에 대한 현재 값을 더해주지 못해 살짝 헤맸다.
