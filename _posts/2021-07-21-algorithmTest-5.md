---
title: "[이코테 2021] 이진 탐색-부품 찾기"
categories: codingtest
tags: python binarysearch
published: true
# use_math: true
# comments: true
---

## [이코테 2021] 이진 탐색-부품 찾기

---

### 문제

책 : 이것이 코딩 테스트다. (197p)

동빈이네 전자 매장에는 부품이 N개 있다. 각 부품은 정수 형태의 고유한 번호가 있다. 어느 날 손님이 M개의 종류의 부품을 대량으로 구매하겠다며 당일 날 견적서를 요청했다.  
동빈이는 때를 놓치지 않고 손님이 문의한 부품 M개 종류를 모두 확인해서 견적서를 작성해야 한다. 이때 가게 안에 부품이 모두 있는지 확인하는 프로그램을 작성해보자.  
예를 들어 가게의 부품이 총 5개일 때 부품 번호가 다음과 같다고 하자.

```
N=5
[8, 3, 7, 9, 2]
```

손님은 총 3개의 부품이 있는지 확인 요청했는데 부품 번호는 다음과 같다.

```
M=3
[5, 7, 9]
```

이때 손님이 요청한 부품 번호의 순서대로 부품을 확인해 부품이 있으면 yes를, 없으면 no를 출력한다. 구분은 공백으로 한다.

### 풀이

풀이는 이진 탐색, 계수 정렬, 집합 자료형 이용 이렇게 3가지 방법을 이용할 수 있다.  
이 중 두가지만 얘기를 해보면,  
<br>
먼저 이진 탐색의 경우, 전자매장에 있는 부품을 정렬한 후에, 이전에 이론에서 봤던 이진 탐색 방법을 이용하면 된다.  
이렇게 문제를 풀게 된다면, _부품을 찾는 과정에서는_ 최악의 경우 시간 복잡도는 O(M X logN) 의 연산이 필요하므로 이론상 최대 약 200만 번의 연산이 이루어진다.  
그리고 N개의 _부품을 정렬하는 과정에서는_ 최악의 경우 시간 복잡도는 O(N X logN) 의 연산이 필요하므로 최대 약 2000만으로 많은 연산이 필요해진다.  
결과적으로, 시간 복잡도는 O((M+N) X logN)이 된다.  
<br>
set 집합 자료형의 경우, 탐색하는 과정에서 유용하게 쓰일 수 있다. set집합 자료형 자체에서 정렬을 해주고,  
특정 값을 찾는데 효과적인 방법을 보여줄 수 있다.

```python
# 이진 탐색
N = int(input())
array = list(map(int, input().split()))
M = int(input())
array_re = list(map(int, input().split()))
array = sorted(array)

def find_num(start, end, num, array):
  if start > end:
    return "no"
  mid = (start + end) // 2
  if array[mid] == num:
    return "yes"
  elif array[mid] > num:
    return find_num(start, mid-1, num, array)
  else:
    return find_num(mid+1, end, num, array)


def solution(N):
  for num in array_re:
    print(find_num(0, N-1, num, array), end = " ")
solution(N)
```

```python
# set 활용
N = int(input())
array = set(map(int, input().split()))  # 탐색 시에 유용
M = int(input())
array_re = list(map(int, input().split()))

for i in array_re:
  if i in array:
    print("yes", end=" ")
  else:
    print("no", end=" ")
```
