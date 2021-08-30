# Linear_Regression
> Linear Regression 구현해보기

Machine Learning의 기초인 Linear Regression을 직접 구현하고 그래프로 확인하여 동작 원리를 올바르게 이해할 수 있도록 설계한 파이썬 코드입니다.

![](../header.png)

## 소개

  이 Repository에서는 경향성이 있는 임의의 2차원 데이터를 400개 만들고 학습하여 이를 대표하는 선형함수(Hypothesis)를 찾는 과정을 쉽게 볼 수 있도록 만들었습니다. Linear Regression은 scikit learn와 같은 라이브러리에서 쉽게 가져와 사용할 수 있습니다. 하지만 Linear Regression을 직접 구현해보고 동작원리를 제대로 파악하지 않는다면 복잡한 상황에서 제대로 활용하기 어렵습니다.  Linear Regression의 Hypothesis를 이루는 Weight, Bias, Cost의 값의 변화를 그래프로 확인하고 나아가 이 값들을 그래프로 표현하여 값의 변화를 확인합니다. 또한 학습이 진행되는 과정에서 H(x)함수가 어떻게 변화하는지 동영상으로 기록하여 확인합니다.

## 구현과정

먼저 임의의 2차원 데이터를 경향성이 있도록 설정합니다.  


```
mat_cov = [[1,0.9],[0.9,1]]
mu =  [4,3]
N = 400
X = np.random.multivariate_normal(mu, mat_cov, N)
```
![data_generation](https://user-images.githubusercontent.com/44831709/131356943-f9f18275-a9a9-4a50-b16b-2613febfda73.png)

Hypothesis를 다음과 같이 정의합니다.  


![hypothesis](https://user-images.githubusercontent.com/44831709/130807611-38f189db-a6fd-441d-8457-8109efc1715e.png)


데이터를 몇 번 학습할지, learning rate는 얼마로 할지 설정하고 임의의 베타값을 설정합니다.

```
N_iter = 1000
N = X.shape[0]
alpha = 0.05
beta_0 = np.random.random()
beta_1 = np.random.random()
x1 = X[:,0]
x2 = X[:,1]
rng = np.random.default_rng(2021)
```



Cost function은 아래와 같이 MSE(Mean Squared Error)로 설정합니다.   


![cost_function](https://user-images.githubusercontent.com/44831709/130806508-eae6ef66-e175-4f52-acbf-edba20e9aa6f.png)


데이터를 학습니다. history 에 베타값을 저장하고 나중에 그래프를 그릴 때 활용합니다.

```
history = []
history.append([beta_0,beta_1])
for i in range(N_iter):
    beta_1_next = beta_1 - alpha * (1/N) * np.sum(2*beta_1*np.square(x1) -2*x1*x2 + 2*x1*beta_0)
    beta_0_next = beta_0 - alpha* (1/N) * np.sum(2*beta_0 - 2*x2 + 2*x1*beta_1)
    beta_1, beta_0 = beta_1_next, beta_0_next
    history.append([beta_0,beta_1])

```

학습을 완료한 후 초기에 분포했던 데이터와 이를 대표하는 1차함수, Linear Graph를 함께 확인합니다.
```
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt

## draw a graph: x2 = beta_1*x1 + beta_0 
xt= np.arange(0,10,0.1)
plt.plot(xt, xt*beta_1+beta_0)


plt.plot(X[:,0],X[:,1],'.')
plt.xlabel('X1')
plt.ylabel('X2')
beta_1 = history[-1][1]
beta_0 = history[-1][0]


plt.grid(True)

```
![quick_plot](https://user-images.githubusercontent.com/44831709/131357530-83206b2e-b38b-4f74-803b-8134f507f1ea.png)

위의 데이터를 대표하는 그래프를 찾았기 때문에 앞으로 우리에게 값을 예측해야 하는 과제가 주어진다면, 우리는 입력값 (x1)이 주어질 때 그에 맞는 결과로 이 Linear 함수에서의 결과값을 반환해주면 됩니다.   
지금까지 주어진 데이터를 대표하는 함수를 찾는 방법으로 학습했습니다. 이 함수를 찾는 과정을 그래프로 확인해 보겠습니다. 
학습에 진행됨에 따라 beta_1의 변화를 확인합니다.

```
%matplotlib inline
np_history = np.array(history)
plt.rcParams["figure.figsize"] = (14,6)
plt.plot(np.arange(N_iter+1),np_history[:,1])
plt.xlabel('N')
plt.ylabel('beta_1')
plt.show()

```
![beta1_plot](https://user-images.githubusercontent.com/44831709/131358333-29d081dd-a5b4-43a6-bea8-9d2a025663c5.png)

beta_0의 변화를 확인합니다.

```
%matplotlib inline
np_history = np.array(history)
plt.rcParams["figure.figsize"] = (14,6)
plt.plot(np.arange(N_iter+1),np_history[:,0])
plt.xlabel('N')
plt.ylabel('beta_0')
plt.show()
```

![beta0_plot](https://user-images.githubusercontent.com/44831709/131358587-64e2d377-ea82-4637-9fe0-786dbf5b1db9.png)


Cost의 변화를 확인합니다.

```
cost_list = []
for b0,b1 in history:
    cost = (1/N)*np.sum(np.square(x2-x1*b1-b0))
    cost_list.append(cost)
    
np_cost = np.array(cost_list)

%matplotlib inline
np_history = np.array(history)
plt.rcParams["figure.figsize"] = (14,6)
plt.plot(np.arange(N_iter+1),np_cost)
plt.xlabel('N')
plt.ylabel('cost')
plt.show()
```

![cost_plot](https://user-images.githubusercontent.com/44831709/131359229-dc70a861-f0d3-454a-ac47-4168f2969543.png)

## 정보

https://wikidocs.net/21670
