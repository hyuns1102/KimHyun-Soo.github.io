---
title: "[네이버 부스트 캠프] AI-Tech - week5(4)"
categories: AI
tags: python
published: true
use_math: true
---

## logistic classification

로지스틱 회귀 함수를 이용해서 예측을 하는 방법을 알아본다.  
이전에 봤던 linear Regression과 logistic regression의 차이는 분류가 연속형인지, 범주형인지에 따라 달라진다.  
예를 들어, 1시간 2시간 공부한 학생이 pass or fail 하는 예측을 할 때, 연속형 x변수에 대한 범주형(category) 종속 변수 y에  
대응되는 경우가 있다.  
이 경우는 linear Regression을 이용해 나타낼 경우, 중간 0~1 사이에 대한 정보를 무시하게 된다. 따라서, logistic Regression의  
simoid function을 통해서 1에 가까운 경우와 0의 가까운 경우로 예측을 할 수 있게 한다.  
즉, 숫자의 의미가 없는 _분류_ 가 가능할 수 있도록 한다.  

### 1. Data set 내에서 여러 개의 Training Data와 Test Data를 명시

  Logistic regression의 경우 이항 분포를 나타내는 것을 볼 수 있다.  

  ```python
  x_data = [[1, 2], [2, 3], [3, 1], [4, 3], [5, 3], [6, 2]]
  y_data = [[0], [0], [0], [1], [1], [1]]
  ```

### 2. Hypothesis(가설) 함수를 찾기 위해 Weight, Bias 0으로 초기화
  
  $ H(X) = \frac{1}{1+e^{-W^T X}} $

  ```python
  W = torch.zeros((2, 1), requires_grad=True)
  b = torch.zeros(1, requires_grad=True)
  hypothesis = 1 / (1 + torch.exp(-(x_train.matmul(W) + b)))
  #hypothesis = 1 / (1 + torch.exp(-(torch.matmul(x_train, W) + b)))
  ```

  위와 같이 hypothesis 는 torch에 있는 exponential 함수를 이용해 나타낼 수 있다.  
  또는 아래와 같이 sigmoid function을 이용해서 simple하게 나타낼 수 있다.  

  ```python
  hypothesis = torch.sigmoid(x_train.matmul(W) + b)
  ```

### 3. Computing the Cost Function & Binary cross entropy

  Cost Function은 Cross Entropy에 의해서 다음과 같인 나타낼 수 있다.  
  실제 값(0 or 1) 과 예측 로그 값을 곱했을 때, 1일 때의 예측 로그값과 0일 때의 예측 로그값을 살려 모든 평균을 낸다.  
  이것을 cost function으로 0에 가깝게 만들도록 학습시키는 것이다.  
  왜냐하면, 예측 값이 정확히 1 또는 0이 나왔을 때 (정확히 예측 했을 때) 답은 0이 되기 때문이다.  
  이 cost function을 활용해서 최적의 W, b값을 구할 수 있도록 한다.  

  $ cost(W) = -\frac{1}{m} \sum y \log\left(H(x)\right) + (1-y) \left( \log(1-H(x) \right) $

  ```python
  losses = -(y_train * torch.log(hypothesis) + 
           (1 - y_train) * torch.log(1 - hypothesis))
  cost = losses.mean()
  ```
  
  위와 같은 방법은, BCE (Binary Cross Entropy) 를 통해 보다 쉽게 나타낼 수 있다.  

  ```python
  cost = F.binary_cross_entropy(hypothesis, y_train)
  ```

### 4. Full Code
  
  위의 식을 토대로 Full Code를 작성하면 다음과 같다.  

Data

```python
x_data = [[1, 2], [2, 3], [3, 1], [4, 3], [5, 3], [6, 2]]
y_data = [[0], [0], [0], [1], [1], [1]]
x_train = torch.FloatTensor(x_data)
y_train = torch.FloatTensor(y_data)
```

Low-level

```python
# 모델 초기화
W = torch.zeros((2, 1), requires_grad=True)
b = torch.zeros(1, requires_grad=True)
# optimizer 설정
optimizer = optim.SGD([W, b], lr=1)

nb_epochs = 1000
for epoch in range(nb_epochs + 1):

    # Cost 계산
    hypothesis = torch.sigmoid(x_train.matmul(W) + b) # or .mm or @
    cost = -(y_train * torch.log(hypothesis) + 
             (1 - y_train) * torch.log(1 - hypothesis)).mean()

    # cost로 H(x) 개선
    optimizer.zero_grad()
    cost.backward()
    optimizer.step()

    # 100번마다 로그 출력
    if epoch % 100 == 0:
        print('Epoch {:4d}/{} Cost: {:.6f}'.format(
            epoch, nb_epochs, cost.item()
        ))
```

F.binary_cross_entropy

```python 
# 모델 초기화
W = torch.zeros((2, 1), requires_grad=True)
b = torch.zeros(1, requires_grad=True)
# optimizer 설정
optimizer = optim.SGD([W, b], lr=1)

nb_epochs = 1000
for epoch in range(nb_epochs + 1):

    # Cost 계산
    hypothesis = torch.sigmoid(x_train.matmul(W) + b) # or .mm or @
    cost = F.binary_cross_entropy(hypothesis, y_train)

    # cost로 H(x) 개선
    optimizer.zero_grad()
    cost.backward()
    optimizer.step()

    # 100번마다 로그 출력
    if epoch % 100 == 0:
        print('Epoch {:4d}/{} Cost: {:.6f}'.format(
            epoch, nb_epochs, cost.item()
        ))
```

### 5. Checking the Accuracy

우리는 위의 학습을 통해 적절한 W와 b를 구한다. 그리고 이 parameter가 얼마나 정확한지 확인해봐야 한다.  
아래의 식처럼 만들어진 W, b를 이용해서 hypothesis 함수를 세운다.  
(본래 x_train이 아닌 실제 x_test를 이용해서 정확성을 체크해야 한다.)

```python
hypothesis = torch.sigmoid(x_train.matmul(W) + b)
```

함수 자체가 float 형식으로 0에 가까운지 1에 가까운지 판단하는 것이므로,  
0.5이상일 경우 1로 아니면 0으로 만든다.  
그리고 눈으로 실제 y값과 대조한다.  

```python
prediction = hypothesis >= torch.FloatTensor([0.5])
print(prediction[:5])

print(prediction[:5])
print(y_train[:5])
```

조건문을 이용해서 y값과 예측값이 같을 경우 1로 아닐 경우 0으로 만들어준다.  
그리고 확률로 나타내어 예측값의 정확성을 측정한다.  

```python
correct_prediction = prediction.float() == y_train
print(correct_prediction[:5])
accuracy = correct_prediction.sum().item() / len(correct_prediction)
print('The model has an accuracy of {:2.2f}% for the training set.'.format(accuracy * 100))
```

### 5. nn & nn.functional

지금까지 했던 이론을 torch.nn, nn.module을 이용하여 상속을 통한 customizing을 이용해서 model의 학습을 간단히 한다.  

```python
class BinaryClassifier(nn.Module):
    def __init__(self):
        super().__init__()
        self.linear = nn.Linear(8, 1)
        self.sigmoid = nn.Sigmoid()

    def forward(self, x):
        return self.sigmoid(self.linear(x))
```

```python
model = BinaryClassifier()
```

학습을 진행할 때마다 정확성을 체크해서 가장 최적의 해를 찾을 수 있게 Full Code를 짠다.  

```python
# optimizer 설정
optimizer = optim.SGD(model.parameters(), lr=1)

nb_epochs = 100
for epoch in range(nb_epochs + 1):

    # H(x) 계산
    hypothesis = model(x_train)

    # cost 계산
    cost = F.binary_cross_entropy(hypothesis, y_train)

    # cost로 H(x) 개선
    optimizer.zero_grad()
    cost.backward()
    optimizer.step()
    
    # 20번마다 로그 출력
    if epoch % 10 == 0:
        prediction = hypothesis >= torch.FloatTensor([0.5])
        correct_prediction = prediction.float() == y_train
        accuracy = correct_prediction.sum().item() / len(correct_prediction)
        print('Epoch {:4d}/{} Cost: {:.6f} Accuracy {:2.2f}%'.format(
            epoch, nb_epochs, cost.item(), accuracy * 100,
        ))

```
