---
title: "[프로그래머스] 카펫"
categories: programmers
tags: programmers python bf
published: true
---

## [프로그래머스] 카펫

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42842)

---

### 풀이

카펫의 가로, 세로 길이를 알기 위해서, 적당한 수학식을 이용하여 탐색하는 방법을 썼다.  
소수찾기에서 했던, 방법을 이용해서 약수를 모두 구한 후, 그 값을 이용해 brown의 값과 일치하는 지  
파악한 후에 일치한다면 answer에 넣게 했다.

```python
import math

def solution(brown, yellow):
    answer = []
    res = []
    for i in range(1, int(math.sqrt(yellow) + 1)):
        if yellow % i == 0:
            garo, sero = yellow//i, i
            res.append([garo, sero])

    for i in range(len(res)):
        if ((res[i][0] + 2) * (res[i][1] + 2) - yellow) == brown:
            answer.append(res[i][0] + 2)
            answer.append(res[i][1] + 2)
            break
    return answer
```

---

### 실수 및 배운 점

- 맞추긴 했지만, 많은 고민을 했다. 어렵지 않은 문제였는데 어렵게 생각하다보니 그렇게 된 것 같다.
