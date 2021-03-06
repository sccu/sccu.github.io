---
published: false
---
처리하기 어려운 연속 사후확률과 큰 데이터셋을 가진 잠재변수가 있을 때 통제된 확률모델의 효율적인 추론과 학습을 어떻게 수행할 수 있을까? 우리는 대규모 데이터셋으로 확장할 수 있고, 완화된 미분가능성 조건 하에서는, 처리하기 어려운 경우에서도 동작하는, 통계적인 변분 추론과 학습 알고리즘을 소개한다. Variational lower bound의 재파라미터화는 SGD를 사용해서 직접 최적화할 수 있는 하한의 추정을 낳는다. 또 datapoint마다 연속잠재변수를 가지는 i.i.d.인 데이터셋에 대해서, 근사추론모델을 적합화하여 계산하기 어려운 사후확률에 대해 제안된 하한 추정을 사용하여 특히 효율적으로 사후 추론을 할 수 있음을 보인다.

## 1. Introduction
변분 베이지안(variational Bayesian, VB) 접근은 계산하기 어려운 사후확률의 근사의 최적화를 포함한다. 불운하게도, mean-field 접근은 근사 사후확률에 대해 기대값의 해석적인 해를 요구하는데, 이는 일반적인 경우에 계산하기 어렵다. 우리는 variational lower bound의 재파라미터화가 어떻게 단순한 미분가능한 편항 없는 하한의 추정이 유도되는지 보인다. 이 SGVB(Stochastic Gradient Variational Bayes) 추정은 연속잠재변수를 가지는 거의 어떠한 모델에서나 효율적인 근사적 사후 추론을 위해 사용될 수 있고, 표준적인 경사상승기법을 사용해 직접적으로 최적화한다.

I.i.d.인 데이터셋과 데이터포인트 당 연속잠재확률변수를 위해 우리는 Auto-Encoding VB(AEVB) 알고리즘을 제안한다. AEVB 알고리즘에서 우리는 인지 모델을 최적화하기 위해 SGBV 추정을 사용해 매우 효율적으로 추론하고 학습한다. 이 모델은 단순한 원형 샘플링을 사용해 매우 효율적인 근사 사후 추론을 할 수 있도록 한다. 이는 다시 데이터포인트마다 (MCMC 같은) 값비싼 반복적 추론 계획 없이 모델 파라미터를 효율적으로 학습하게끔 한다. 학습된 근사 사후 추론 모델은 인지, 노이즈 제거, 표상화와 시각화 목적 같은 다수의 작업을 위한 사용될 수 있다. 인지 모델을 위해 신경망이 사용될 때 우리는 *variational auto-encoder*에 도달한다.

## 2. Method
이 섹션의 전략은 연속 잠재변수를 가진 방향 그래피컬 모델의 변형에 대해 하한 추정을 유도하기 위해 사용될 수 있다.
![Figure 1](/assets/AEVB-fig1.png){:height="30%" width="30%"}  
Figure 1: 고려 중인 방향 그래피컬 모델의 한 종류. 실선은 생성모델 $$p_\boldsymbol\theta (\mathrm z) p_\boldsymbol\theta (\mathrm x | \mathrm z)$$을 나타내고, 점선은 변분 근사 $$q_\boldsymbol\phi (\mathrm z | \mathrm x)$$를 나타낸다. 변분 매개변수 $$\boldsymbol \phi$$는 생성모델 파라미터 $$\boldsymbol \theta$$와 함께 결합해서 학습된다.

### 2.1 Problem scenario
연속 혹은 이산변수 $$\textbf x$$의 i.i.d.인 샘플로 이루어진 데이터셋 $$\boldsymbol X = \{\textbf x^{(i)}\}_{i=1}^N$$를 고려하자. 데이터는, 관찰되지 않은 연속확률변수 $$\textbf z$$를 포함하는, 어떤 랜덤 프로세스에 의해 생성되었다고 가정하자. 이 프로세스는 두 단계로 이루어진다. 

