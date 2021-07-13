---
title: "[프로그래머스] 도둑질"
categories: programmers
tags: programmers python dp
published: true
---

## [프로그래머스] 도둑질

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42897)

---

### 풀이

이 문제는 이전에 풀었던 [개미전사](https://hyuns1102.github.io/boj/BOJ-18/) 문제를 참고하면 좋을 것 같다.  
개미전사 문제와 같이 일직선 상에서 인접한 경우를 제외해서 최대 값을 나타낼 수 있는 점화식을 세우면 다음과 같다.  
`d[n] = max(d[n-1], d[n-2]+a[n])`  
이 문제에서 또한, 점화식을 그대로 이용하면 된다. 하지만 여기서 개미전사 문제와 다른 점은 리스트가 **'순환'**된다는 것이다.  
순환이 될 때 인접한 두 가지가 붙지 않기 위해서 고려해야할 점이 있다.

1. 첫번째 시작 점이 반드시 결과 값에 들어갈 때 (`dp[0], dp[1] = money[0]`)
2. 두번째 시작 점이 반드시 결과 값에 들어갈 때 (`dp[1] = money[1]`)

두가지 경우를 고려해주는 이유는  
첫번째 경우는 마지막 번째를 비교해서 결과를 넣지 않는다.  
두번째 경우는 마지막 번째를 비교해서 결과를 넣게 된다.

따라서 이 조건을 만족해서 코드를 짜면 다음과 같다.

```python

def solution(money):
    answer = 0
    dp = [0] * len(money)

    # i == 0 에서 무조건 턴다면? 마지막은 결과 값 x
    dp[0] = money[0]
    dp[1] = dp[0]
    for i in range(2, len(money)-1):
        dp[i] = max(dp[i-1], money[i] + dp[i-2])
    answer = max(dp)

    # i == 1 에서 무조건 턴다면? 마지막은 결과 값 o
    dp = [0] * len(money)
    dp[1] = money[1]
    for i in range(2, len(money)):
        dp[i] = max(dp[i-1], money[i] + dp[i-2])
    answer = max(answer, max(dp))
    return answer

```

---

### 실수 및 배운 점

- 순환했을 때 먼저 생각해야할 점은 '일직선' 상에 놓고 생각해야 한다는 것을 알게 되었다.  
  순환점은 시작과 마지막을 반드시 고려해야하기 때문이다.  
  아쉬웠던 점은 이전에 풀었던 개미전사와 비슷한 문제라는 것을 인지했지만, 이전처럼 제대로 유도하지 못했다.  
  순환이라는 점이 계속 헷갈리게 만들었던 것 같다.  
  조금 더 간단하게 생각하고 만들어 나가야겠다는 생각을 했다.
