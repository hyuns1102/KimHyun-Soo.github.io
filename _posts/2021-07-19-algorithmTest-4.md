---
title: "[이코테 2021] 이진 탐색"
categories: codingtest
tags: python
published: true
# use_math: true
# comments: true
---

## [이코테 2021] 이진 탐색

> 이론, 예시 코드

---

## 이진 탐색

이진 탐색이란 반으로 쪼개면서 탐색하는 방법이다.  
이진 탐색은 배열 내부의 데이터가 정렬되어 있어야만 사용 가능한 방법이다.  
위치를 나타내는 변수 3개를 사용한다. 시작점, 중간점, 끝점  
찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는 과정이다.  
이진 탐색은 한 번 확인할 때마다 확인하는 원소의 개수가 절반씩 줄어든다는 점에서 시간 복잡도가 $$\log_2 N$$ 이다.
<br>
이진 탐색 구현 방법 2가지  
이 두 가지 방법은 가능한 외워두자. 간단할 수 있지만, 응용 문제 시에 시간을 단축시키는데 좋다.  

```python
# 이진 탐색 소스코드 구형(재귀 함수)
def binary_search(array, target, start, end):
  # start (시작점)가 end(끝점)을 넘어가면 None 
  if start > end:
    return None
  mid = (start + end) // 2
  if array[mid] == target:
    return mid
  # 중간값이 taget보다 클 경우, 끝점 수정
  elif array[mid] > target:
    return binary_search(array, target, start, mid - 1)
  # 중간값이 taget보다 작을 경우, 시작점 수정
  else:
    return binary_search(array, target, mid + 1, end)

n, target = list(map(int, input().split()))
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n-1)
if result == None:
  print("존재x")
else:
  print(result + 1) # 인덱스를 찾을 때
```

```python
# 이진 탐색 소스코드 구형(반복문)
def binary_search(array, target, start, end):
  # start (시작점)가 end(끝점)을 넘어가면 None 
  while start <= end:
      mid = (start + end) // 2
      if array[mid] == target:
          return mid
      elif array[mid] > target:
          end = mid-1
      else:
          start = mid+1
  return None

n, target = list(map(int, input().split()))
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n-1)
if result == None:
  print("존재x")
else:
  print(result + 1) # 인덱스를 찾을 때
```
