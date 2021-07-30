---
title: "[네이버 부스트 캠프] AI-Tech - week5(5)"
categories: AI
tags: python
published: true
use_math: true
---

## Softmax classfication & Cross Entropy

이전 포스팅에서는 확률 분포가 '이항 분포'일 때 (y=0 or 1), logistic regression 방법을 이용하기 위해 sigmoid function을 활용해서 예측했다.  
이번에는 이산 확률 분포로 주어질 때, (y = 0, 1, 2, 3, 4, .. ) 예측 함수를 학습하는 방법에 대해 알아본다.  
여기서는 Softmax classification을 통해 가설함수를 세우고, Cross Entropy를 이용해서 Cost Function을 최소화 시켜서 예측 가능한 함수로 학습할 수 있게 한다.  

### 1. SoftMax
  
  SoftMax는 밑의 식처럼 이산확률 분포일 때, 함수 값들을 확률 값들로 변경시켜주는 역할을 한다. 
  $ P(class=i) = \frac{e^i}{\sum e^i} $
  
  ```python
  z = torch.FloatTensor([1, 2, 3])
  hypothesis = F.softmax(z, dim=0)

  # tensor([0.0900, 0.2447, 0.6652])
  ```


### 2. Cross Entropy Loss (Low-level)
  
  Multi-classification 의 경우, Cross Entropy loss를 쓸 수 있다.  
  2개의 확률 분포가 주어졌을 때, 2개가 얼마나 비슷한지 나타낼 수 있는 확률 분포 수치를 나타내는 것이다.  
  여기서 2개의 확률 분포는 예측 분포와 실제 분포를 의미한다.  
  즉, 목표는 이 2개의 확률 분포의 Cross Entropy를 최소화 시키는 것이다.  
  
  아래의 식에서 $ hat{y} $ 은 예측된 확률을 말하고 $ y $ 는 실제 값을 뜻한다.  

  $ L = \frac{1}{N} \sum - y \log(\hat{y}) $

  아래의 식은 강의에서 이론적으로 말한 것인데.. 이해가 안간다.  
  $ H(P, Q) = -\mathbb{E}{_{x\sim P(x)}}[log{Q(x)}] = - \sum{_{x\in \chi }}P(x)logQ(x) $
  
  예시)  
  문제를 만들자면,  
  3행 5열의 행렬을 만들고 이 때의 정답 값 ( 1행 3열 )을 randint로 뽑았을 때,  
  이 때의 cross entropy를 구하는 문제이다.  
  
  1) 3 x 5의 랜덤 행렬을 만들어준다. (gardient 가능한 )  
    그리고 softamx를 했을 때 가설 함수를 만든다.  

  ```python
    z = torch.rand(3, 5, requires_grad=True)
    hypothesis = F.softmax(z, dim=1)
    print(z)
    print(hypothesis)

    #tensor([[0.7576, 0.2793, 0.4031, 0.7347, 0.0293],
    #      [0.7999, 0.3971, 0.7544, 0.5695, 0.4388],
    #      [0.6387, 0.5247, 0.6826, 0.3051, 0.4635]], requires_grad=True)
    #tensor([[0.2645, 0.1639, 0.1855, 0.2585, 0.1277],
    #      [0.2430, 0.1624, 0.2322, 0.1930, 0.1694],
    #      [0.2226, 0.1986, 0.2326, 0.1594, 0.1868]], grad_fn=<SoftmaxBackward>)
  ```

  2) 0~5 사의 값을 가지는 3열의 행렬 생성 (실제값)

  ```python
  y = torch.randint(5, (3,)).long()
  #tensor([0, 2, 1])
  ```
  
  3) hypothesis 크기의 y_one_hot vector를 만들어준다.  

  ```python
  y_one_hot = torch.zeros_like(hypothesis)
  print(y_one_hot)
  y_one_hot.scatter_(1, y.unsqueeze(1), 1)
  print(y_one_hot)
  ``` 

  4) 이 때의 cost function은 위의 이론에 따라 cross entropy에 의해, 다음과 같이 나타낼 수 있다.  

  ```python
  cost = (y_one_hot * -torch.log(hypothesis)).sum(dim=1).mean()
  ```


### 3. Computing the Cost Function & Binary cross entropy

 
### 4. Full Code
  
### 5. Checking the Accuracy

### 6. nn & nn.functional
