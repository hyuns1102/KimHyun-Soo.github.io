---
title: "[프로그래머스] 입국심사"
categories: programmers
tags: programmers python binarysearch
published: true
---

## [프로그래머스] 입국심사

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/43238)

---

### 풀이

이 문제는 문제에서부터 값의 범위가 10억이 넘어가기에 시간복잡도를 최소로 할 수 있는  
이진탐색을 이용해야한다는 것을 알아야한다.  
이진탐색을 이용하자면, 시간을 이용해서 중간값을 찾고, 최소 시간들을 쓰는 사무국들을 최대로 가져가며  
사람 수를 최대로 하는 시간을 가져온다.  
<br>
가장 애먹는 부분은 정확히 어떤 부분이 최소인가 인데  
몫만을 가져가면서 비교하기 때문에, 목표 사람 수와 같을 때 end값을 mid-1로 지정해줘서  
또 한번 비교할 수 있게 하고 최소 답을 가져오면 된다.

```python

def solution(n, times):
    answer = []
    start, end =0, min(times) * n
    times = sorted(times)
    while start <= end:
        total = 0
        mid = (start + end) // 2

        for x in times:
            if mid >= x:
                total += mid // x

        if n > total:
            start = mid + 1
        if n <= total:
            end = mid - 1
            answer.append(mid)

    return min(answer)

```

---

### 실수 및 배운 점

-
