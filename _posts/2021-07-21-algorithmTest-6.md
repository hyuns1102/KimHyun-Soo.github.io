---
title: "[이코테 2021] 이진 탐색-떡볶이 떡"
categories: codingtest
tags: python binarysearch
published: true
# use_math: true
# comments: true
---

## [이코테 2021] 이진 탐색-떡볶이 떡

---

### 문제

책 : 이것이 코딩 테스트다. (201p)

동빈이네 떡볶이 떡은 길이가 일정하지 않다. 떡볶이 떡의 길이가 일정하지 않지만 한 봉지 안에 들어가는 떡의 총 길이는 절단기로 잘라 맞춘다.  
절단기에 높이(H)를 지정하면 줄지어진 떡을 한 번에 절단한다. 높이가 H보다 긴 떡은 H 위의 부분이 잘릴 것이고, 낮은 떡은 잘리지 않는다.  
예를 들어 높이가 19, 14, 10, 17cm인 떡이 나란히 있고 절단기 높이를 15cm로 지정하면 자른 뒤 떡의 높이는 15, 14, 10, 15cm가 될 것이다.  
잘린 떡의 길이는 차례대로 4, 0, 0, 2cm이다. 손님은 6cm만큼의 길이를 가져간다.  
손님이 왔을 때 요청한 총 길이가 M일 때 적어도 M만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램을 작성하시오.

- 입력
  첫째 줄에 떡의 개수 N과 요청한 떡의 길이 M이 주어진다. (1<= N <= 1,000,000 , 1 <= M <= 2,000,000,000)
  둘째 줄에는 떡의 개별 높이가 주어진다. 높이는 항상 M 이상, 높이는 10억보다 작거나 같은 양의 정수 또는 0 이다.

### 풀이

풀이는 이진 탐색으로만 풀 수 있는 문제이다. 중간값의 위치에 따라 길이를 계산해주고 목표 떡의 길이와 비교했을 때,  
작으면 잘랐을 때, 길이를 많이 먹을 수 있도록 end값을 조정하고 크다면 잘랐을 때 길이를 적게할 수 있도록 start값을 조정한다.

```python
# 이진 탐색
n, m = map(int, input().split())
array = list(map(int, input().split()))

def find_height(n, m, array):
  start, end = 0, max(array) # 시작점 끝점 생성
  answer = 0
  while True:
    if start > end:
      return answer
    res = 0
    mid = (start + end) // 2 # 중간값 생성
    for i in range(n):
      if array[i] > mid:
        res += array[i] - mid # 중간값에서 잘랐을 때 떡의 길이

    if res >= m:              # 현재 떡의 총 길이가 목표값보다 크거나 같을 때,
                              # 적어도 M만큼의 떡을 얻어야 하기 때문에 M보다 작으면 안된다.
      start = mid + 1
      answer = mid
      if res == m:            # 목표값에 맞다면 return
        return answer
    else:
      end = mid-1

print(find_height(n, m, array))
```
