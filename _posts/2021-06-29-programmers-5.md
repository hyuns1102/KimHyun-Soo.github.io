---
title: "[프로그래머스] 모의고사"
categories: programmers
tags: programmers python bf
published: true
---

## [프로그래머스] 모의고사

### 문제

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/42840)

---

### 풀이

**완전 탐색(Brute Force)**
1번 수포자, 2번 수포자, 3번 수포자가 찍는 방식이 정해져 있고,  
문제의 정답이 주어질 때, 답을 가장 많이 맞춘 사람을 출력한다.  
단, 여러 사람일 경우 오름차순 출력한다.  
<br>
이 경우는 푸는 사람의 패턴을 파악하고, count를 해준 후에  
사람의 번호와 개수를 동시에 갖고와서 가장 큰 수를 가진 사람만 출력할 수 있게 한다.  
오름차순을 고려해야 하기 때문에 번호 순서대로 비교하면서 출력한다.

```python
def solution(answers):
    answer = []
    one = [1,2,3,4,5]
    two = [2,1,2,3,2,4,2,5]
    three = [3,3,1,1,2,2,4,4,5,5]
    count = [0,0,0]

    for i in range(len(answers)):
        if answers[i] == one[i % len(one)]:
            count[0] += 1
        if answers[i] == two[i % len(two)]:
            count[1] += 1
        if answers[i] == three[i % len(three)]:
            count[2] += 1

    for idx, value in enumerate(count):
        if max(count) == value:
            answer.append(idx+1)

    #  for i in range(len(count)):
    #     if max(count) == count[i]:
    #         answer.append(i+1)

    return answer
```

---

### 실수 및 배운 점

- 먼저, 정답 패턴과 정답이 주어졌을 때 맞는 지 파악하는 것을 어렵게 생각했다.  
  단순히 배열의 길이와 인덱스를 생각하면 되는 부분이었다.

- [enumerate](https://docs.python.org/3/library/functions.html?highlight=enumerate#enumerate)
  에 대해서 알게 되었다. enumerate(list) 는 list 안에 있는 index, value  
  값을 같이 뽑아내어 for문 안에서 이용할 수 있다.

- 혼자서 다시 풀어보니, 굳이 enumerate를 안써도 쉽게 풀 수 있는 문제였다.
  너무 어려운 방법이나 새로운 방법을 구사하려고 애쓰는 기분이다. 천천히 생각하자.
