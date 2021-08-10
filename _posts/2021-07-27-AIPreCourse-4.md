---
title: "[네이버 부스트 캠프] AI-Tech - week5(3)"
categories: AI precourse
tags: python
published: true
use_math: true
---

## 목차

[Multivariable Linear Regression](#multivariable-linear-regression)  
[Load Data](#load-data)  

## multivariable linear regression

Multivariable Linear Regression는 다항 선형 회귀 함수를 의미한다.  
이전에 포스팅 했던 Linear Regression과 다르게 _여러 개의_ x_train이 주어지고 하나의 y값이 주어졌을 때 Train 시키는 방법에 대해서 알아본다.  

### 1. Data set 내에서 여러 개의 Training Data와 Test Data를 명시

  ```python
  x1_train = torch.FloatTensor([[73], [93], [89], [96], [73]])
  x2_train = torch.FloatTensor([[80], [88], [91], [98], [66]])
  x3_train = torch.FloatTensor([[75], [93], [90], [100], [70]])
  y_train = torch.FloatTensor([[152], [185], [180], [196], [142]])
  ```

### 2. Hypothesis(가설) 함수를 찾기 위해 Weight, Bias 0으로 초기화
  
  $ H(x_1, x_2, x_3) = x_1w_1 + x_2w_2 + x_3w_3 + b $

  ```python
  w1 = torch.zeros(1, requires_grad=True)
  w2 = torch.zeros(1, requires_grad=True)
  w3 = torch.zeros(1, requires_grad=True)
  b = torch.zeros(1, requires_grad=True)
  hypothesis = x1_train * w1 + x2_train * w2 + x3_train * w3 + b
  ```

  위와 같이 hypothesis 는 w1,w2,w3, ... 으로 많은 나열이 필요하다.  
  이 경우를 간단하게 해주기 위해서 matmul()로 한번에 계산할 수 있도록 한다.  
  그리고 속도도 훨씬 더 빠르다!

  ```python
  x_train = torch.FloatTensor([[73, 80, 75],
                             [93, 88, 93],
                             [89, 91, 90],
                             [96, 98, 100],
                             [73, 66, 70]])
  y_train = torch.FloatTensor([[152], [185], [180], [196], [142]])

  W = torch.zeros((3, 1), requires_grad=True)
  b = torch.zeros(1, requires_grad=True)
  hypothesis = x_train.matmul(W) + b
  ```

### 3. Compute Loss(MSE) & gradient descent

  Cost Funtion, gradient descent는 이전 포스팅에서 했던 Simple Linear Regression 과 동일한 이론을 적용한다.  

  $Cost(W, b) = \frac{1}{m}\sum_{i = 1}^{m}(H(x^{i}) - y^{i})^{2}$
  $ \nabla W = \frac{\partial cost}{\partial W} = \frac{2}{m} \sum^m_{i=1} \left( Wx^{(i)} - y^{(i)} \right)x^{(i)} $
  $ W := W - \alpha \nabla W $

  ```python
  cost = torch.mean((hypothesis - y_train) ** 2)
  #optimizer 설정
  optimizer = optim.SGD([W, b], lr = 0.01)

  #optimizer 사용법
  optimizer.zero_grad() # gradient 초기화
  cost.backward() # gradient 계산
  optimizer.step() # step() 으로 개선
  ```

  이를 통해, 결과적으로 **최적의 W, b**를 결정한다.

### 4. Full Code
  
  위의 식을 토대로 Full Code를 작성하면 다음과 같다.  

```python
# 모델 초기화
W = torch.zeros((3, 1), requires_grad=True)
b = torch.zeros(1, requires_grad=True)
# optimizer 설정
optimizer = optim.SGD([W, b], lr=1e-5)

nb_epochs = 20
for epoch in range(nb_epochs + 1):
    
    # H(x) 계산
    hypothesis = x_train.matmul(W) + b # or .mm or @

    # cost 계산
    cost = torch.mean((hypothesis - y_train) ** 2)

    # cost로 H(x) 개선
    optimizer.zero_grad()
    cost.backward()
    optimizer.step()

    # 100번마다 로그 출력
    print('Epoch {:4d}/{} hypothesis: {} Cost: {:.6f}'.format(
        epoch, nb_epochs, hypothesis.squeeze().detach(), cost.item()
    ))
```

  여기서 새로운 방법인 nn.module을 활용한 모델을 생성한다.  

### 5. nn & nn.functional
  
  ```python
  import torch.nn as nn

  class MultivariateLinearRegressionModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.linear = nn.Linear(3, 1) # 입력 차원이 3일 때, 출력 차원은 1로 나타낸다. 

    def forward(self, x):  # 여기서 Hypothesis 계산을 한다.
        return self.linear(x)
  ```

  위의 식처럼 nn.module을 상속해서 모델을 생성한다.  
  nn.Linear(3,1)을 통해 입력 차원이 3일 때, 출력 차원은 1로 하는 Linear funcion을 만든다.  
  Hypothesis 계산은 forward() 에서 한다. forward를 통해 Linear를 할 수 있도록 한다  
  gradient 계산은 PyTorch 가 알아서 해준다. -> cost.backward()

  ```python
  import torch.nn.functional as F
  cost = F.mse_loss(prediction, y_train) #cost 계산
  ```

  위의 식은 torch.nn.functional에서 제공하는 loss function을 사용한다.  
  이는 이전 코드보다 에러가 덜 나고, 다른 loss와 교체할 수 있는 장점이 있다.  
  
### 6. Full Code

이렇게 조금 더 빠르게 만들 수 있다.  

```python

# 데이터
x_train = torch.FloatTensor([[73, 80, 75],
                             [93, 88, 93],
                             [89, 91, 90],
                             [96, 98, 100],
                             [73, 66, 70]])
y_train = torch.FloatTensor([[152], [185], [180], [196], [142]])
# 모델 초기화
model = MultivariateLinearRegressionModel()
# optimizer 설정
optimizer = optim.SGD(model.parameters(), lr=1e-5)

nb_epochs = 20
for epoch in range(nb_epochs+1):
    
    # H(x) 계산
    prediction = model(x_train)
    
    # cost 계산
    cost = F.mse_loss(prediction, y_train)
    
    # cost로 H(x) 개선
    optimizer.zero_grad()
    cost.backward()
    optimizer.step()
    
    # 20번마다 로그 출력
    print('Epoch {:4d}/{} Cost: {:.6f}'.format(
        epoch, nb_epochs, cost.item()
    ))
```

## load data

이전에 했던 linear regression의 이론과 공식 같은 경우, 데이터 양이 적을 때를 얘기했다.  
하지만 실제 러닝에서는 엄청난 양의 데이터를 이용해서 러닝을 한다. (적어도 수십만개의 데이터 제공)  
  
수십만개의 데이터를 이용할 경우, 연산량이 이전에 비해서 증가하게 되고 일반적으로 하드웨어가 받아주기가 힘들어진다.  
이를 효율적으로 활용하기 위해서는 데이터를 쪼개서 학습하는 방법을 이용하고자 한다. -> **mini-batch**  
전체 데이터 = mini-batch + mini-batch + mini-batch ...  

### 1. Effects

  업데이트를 좀 더 빠르게 할 수 있다.  
  전체 데이터를 쓰지 않아서 잘못된 방향으로 업데이트 할 수 있다.  
  cost가 매끄럽게 줄어들지 않을 수 있다.  

  Pytorch에서 사용하는 방법을 알아보면,  

### 2. Pytorch Dataset

torch.utils.data.Dataset을 상속받아 직접 커스텀 데이터셋(Custom Dataset)을 만든다.  
torch.utils.data.Dataset은 파이토치에서 데이터셋을 제공하는 추상 클래스입니다. 이 상속을 통해 메소드들을 오버라이드해서 커스텀 데이터 셋을 만든다.  
각 메소드는 주석을 보며 기능을 이해하자.  

```python
from torch.utils.data import Dataset

class CustomDataset(Dataset):
    def __init__(self): # 데이터셋의 전처리를 해주는 부분
        self.x_data = [[73, 80, 75],
                       [93, 88, 93],
                       [89, 91, 90],
                       [96, 98, 100],
                       [73, 66, 70]]
        self.y_data = [[152], [185], [180], [196], [142]]

    def __len__(self): # 데이터셋의 길이, 샘플의 개수
        return len(self.x_data)

    def __getitem__(self, idx): # 데이터 셋에서 특정 샘플을 가져오는 함수
        x = torch.FloatTensor(self.x_data[idx])
        y = torch.FloatTensor(self.y_data[idx])
        return x, y

dataset = CustomDataset()
```

### 3. Pytorch DataLoader

torch.utils.data.DataLoader을 사용해서 위에서 커스텀한 데이터 셋, batch size, shuffle 여부를 설정해준다.  
batch size는 주로 2의 제곱 수로 설정한다.  
shuffle을 하는 이유는 Epoch마다 연산을 외울 수 없도록 하기 위해서다.  

```python
from torch.utils.data import DataLoader

dataloader = DataLoader(
    dataset,
    batch_size=2,
    shuffle=True,
)
```

### 4. Full Code

위의 식을 토대로 전체 코드를 짜면 다음과 같다.  

```python

nb_epochs = 20
for epoch in range(nb_epochs + 1):
    for batch_idx, samples in enumerate(dataloader):
        x_train, y_train = samples
        # H(x) 계산
        prediction = model(x_train)
        # cost 계산
        cost = F.mse_loss(prediction, y_train)
        # cost로 H(x) 개선
        optimizer.zero_grad()
        cost.backward()
        optimizer.step()
        print('Epoch {:4d}/{} Batch {}/{} Cost: {:.6f}'.format(
        epoch, nb_epochs, batch_idx+1, len(dataloader),
        cost.item()
        ))

```
