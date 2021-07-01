---
title: "[프로그래머스] N으로 표현"
categories: programmers
tags: programmers python dp
published: true
---

## [프로그래머스] N으로 표현

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42895)

---

### 풀이

이 문제는 일정한 규칙을 찾은 후, Dynamic Programming 을 이용해서 푸는 문제이다.  
먼저, 규칙을 찾기 위해서 예를 들어 만들어 봤다.  
a(i)는 N이 i개 사용되었을 때 생기는 결과 값이라 하자.

N = 5 일 때,

```python
a(1) = [5]
a(2) = [55, 5+5, 5x5, 5-5, 5/5]
a(3) = [555, 5+(5+5), 5x(5+5), 5-(5+5), 5/(5+5),
        5+(5x5), 5x(5x5), 5-(5x5), 5/(5x5), ...]
...
```

이런 식으로 나가게 될 것이다. 즉, 이것만 보면 규칙성이 눈에 보인다.  
사칙연산하는 과정은 X라 하자. 그렇다면,

```python
a(1) = [N]
a(2) = [NN, a(1) X a(1)]
a(3) = [NNN, a(1) X a(2), a(2) X a(1)]
a(4) = [NNNN, a(1) X a(3), a(2) X a(2), a(3) X a(1)]
...
a(i) = [N*i, a(1) X a(i-1), ... , a(i-1) X a(1)]
```

다음과 같이 나타낼 수 있다.  
<br>
즉, 이전 결과 값들을 이용해서 나타내는 것을 볼 수 있다.  
그리고 여기서 주의할 점은

1. 각 수열에는 번호만큼 자리를 가진 N이 존재한다.  
   (a(5) = [55555, ... ])
2. 나누기와 빼기가 있기 때문에, 위치를 바꿔서도 계산을 해야한다. 또한, 나누기의 경우 분모가 0일 경우를 제외해줘야 한다.

3. 가져가야할 수열들 a(i-n), a(n) 의 번호 합이 현재 번호와 같아야한다. (i = i - n + n)

이 경우들을 고려해서 코드를 만들면 다음과 같다.

```python
# list 이용
def solution(N, number):
    dp = [[] for _ in range(9)]

    for index in range(1, 9):
        dp[index].append(int(str(N) * index)) # 수열이 시작될 때 자리수 만큼의 수를 만들어 준다.
        for i in range(1, index//2 + 1):
            for x in dp[index - i]: # 가져가야할 수열의 번호 합이 현재 번호와 같도록 한다.
                for y in dp[i]: # 사칙 연산시 빼기와 나누기를 고려해서 만들어준다.
                    dp[index].append(x+y)
                    dp[index].append(x-y)
                    dp[index].append(y-x)
                    dp[index].append(x*y)
                    if y != 0:
                        dp[index].append(x//y)
                    if x != 0:
                        dp[index].append(y//x)
        if number in dp[index]: # dp가 만들어질 때 바로 확인할 수 있도록 한다.
            return index
    return -1
```

```python
# set 이용
def solution(N, number):
    dp = [{} for _ in range(9)]
    for index in range(1, 9):
        dp[index] = {int(str(N) * index)} # 첫째번 set 설정
        for i in range(1, index//2 + 1):
            for x in dp[index - i]:
                for y in dp[i]:
                    dp[index].add(x+y)
                    dp[index].add(x-y)
                    dp[index].add(y-x)
                    dp[index].add(x*y)
                    if y != 0:
                        dp[index].add(x//y)
                    if x != 0:
                        dp[index].add(y//x)
        if number in dp[index]:
            return index
    return -1

print(solution(2, 11))
```

---

### 실수 및 배운 점

- 실수했던 점은 점화식을 다 구했는 데 많은 루프를 돌려야하기 때문에 시간 초과가 날 수 있다는 걱정을 했다. 그래서 코드로 제대로 구현해보지 못한채 고민만 했다는 점이다.  
  풀이를 보고 아쉬운 생각이 너무 들었다. 이제는 아이디어가 떠오르면 구현부터 해봐야 겠다는 생각이 들었다.

- set는 안에 아무것도 없을 때 add 안된다는 것이다.  
  에러 메세지를 보면, dict로 인식해서 add가 되지 않는다.  
  하나의 수라도 있어야 add가 가능하다.

- 문자열을 수로 나타낼 때, join을 이용하려 했다.  
  하지만 굳이 그럴 필요가 없는게 이미 모아져 있는 수라면 문자열로 만들어서 int형으로 바꿔도 수로 나타내질 수 있다.

  Number = int(str(N) \* i)

  ```python
  N = 5
  Number = int(str(N) * 5)
  Number : 55555
  ```

  join : 문자열 리스트가 주어지고 합해질 때

  ```python
  s = ["hi", "hello"], s = "".join(s)
  s : "hihello"
  ```
