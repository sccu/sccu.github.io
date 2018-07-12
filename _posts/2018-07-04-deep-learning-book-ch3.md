---
published: true
title: Chapter 3. Probability and Information Theory
category: deeplearningbook
---
확률이론은 불확실한 진술을 나타내기 위한 수학적 체계이다. 불확실성을 정량화하는 방법과 새로운 불확실한 진술을 유도하기 위한 공리들을 제공한다.  
확률이론은 불확실한 진술을 만들고 불확실성에 직면하여 추론할 수 있게 해 주는 반면, 정보이론은 어떤 확률분포 안에서 불확실성의 양을 측정할 수 있게 한다.

### 3.1 Why Probability?
세 가지 불확실성의 원천이 있다.  
1. 모델링된 시스템 내부에 본연의 확률적 성질. 예를 들어 원자보다 작은 입자들의 역학은 확률적이다.
1. 불완전한 관측.
1. 불완전한 모델링. 예를 들어 어떤 로봇이 사물의 위치를 관측할 때 공간을 이산화한다면 로봇에게 사물의 위치는 불확실한 정보가 된다.

확률이론은 원래 사건의 빈도를 분석하기 위해 개발되었다. 하지만 환자 진단과 같이 반복할 수 없는 명제의 경우에 확률은 **믿음의 정도**를 표현한다. 이렇게 사건의 비율에 관련된 확률을 **빈도주의자의 확륩**이라고 하고, 확실한 정도에 관계된 경우를 **베이지안 확률**이라고 한다.

확률은 불확실성을 다루는 논리의 확장으로 볼 수 있다. 논리는 다른 명제들의 집합이 참이거나 거짓이라는 가정이 주어졌을 때 어떤 명제가 참인지 거짓인지 결정하기 위한 형식화된 규칙의 집합을 제공한다. 확률이론은 다른 명제들의 가능도가 주어졌을 때 어떤 명제의 가능도를 결정하기 위한 형식화된 규칙의 집합을 제공한다.

### 3.2 Random Varialbes
**확률변수**는 무작위로 다른 값들을 취할 수 있는 변수이다. 확률변수는 일반적으로 보통 활자체의 소문자 글자($$\mathrm x$$)로, 확률변수가 가질 수 있는 값은 소문자 필기체 글자($$x$$)로 나타낸다. 벡터 변수에 대해서는 확률변수는 $$\mathbf x$$로, 그 값은 $$\boldsymbol x$$로 쓴다. 확률변수 자체만으로는 가능한 상태들의 설명일 뿐이므로, 그 상태들이 얼마나 잘 생기는지 설명하는 확률분포와 함께 결합되어야 한다.

확률변수는 이산적일수도 있고 연속적일수도 있다. 이산확률변수는 유한하거나 셀 수 있게 무한한 상태를 가지는 변수다. 여기서 상태란 정수 뿐만 아니라 수치적인 값을 가지지 않는 명명된 상태일 수도 있다. 연속확률변수는 실수와 연관된다.

### 3.3 Probability Distributions
**확률분포**는 하나 혹은 일련의 확률변수가 가능한 상태들 각각을 가질 가능성이 얼마나 되는지에 대한 설명이다. 우리가 확률분포를 기술하는 방법은 확률변수가 이산적인지 연속적인지에 달려 있다.

#### 3.3.1 Discrete Variables and Probability Mass Functions
이산변수에 대한 확률분포는 **확률질랑함수(probability mass function, PMF)**를 사용해서 기술할 수 있다. 확률질량함수는 보통 대문자 $$P$$로 표기한다. 종종 우리는 각각의 확률변수를 다른 확률질량함수와 결합하므로, 독자들은 어떤 확률질량함수를 사용할지를 함수의 이름이 아니라 확률변수의 동일성을 기반으로 추론해야 한다. $$P(\mathrm x)$$는 일반적으로 $$P(\mathrm y)$$와 다른 확률질량함수다.

확률질량함수는 확률변수의 상태를 그 상태를 취한 확률변수의 확률로 매핑한다. $$\mathrm x = x$$인 확률은 $$P(x)$$로 표기한다. 확률 1은 $$\mathrm x = x$$이 확실함을, 확률 0은 $$\mathrm x = x$$이 불가능함을 나타낸다. 때로는 어떤 PMF를 사용했는지 애매하지 않기 위해, $$P(\mathrm x = x)$$와 같이 확률변수의 이름을 명확히 쓰기도 한다. 때로는 변수를 먼저 정의하고, 그 뒤에 어떤 분포인지 명세하기 위해 $$\sim$$ 표기를 써서 $$\mathrm x \sim P(\mathrm x)$$와 같이 표기하기도 한다.

확률질량함수는 많은 확률변수와 동시에 작용할 수도 있다. 그렇게 많은 확률변수에 대한 확률분포를 **결합확률분포(joint probability distribution)**이라고 한다. $$P(\mathrm x = x, \mathrm y = y)$$는 $$\mathrm x = x$$인 동시에 $$\mathrm y = y$$일 확률을 표시한다. 짧게 $$P(x, y)$$로 쓰기도 한다.

함수 $$P$$가 확률변수 $$\mathrm x$$에 대한 확률질량함수이기 위해서는 다음 속성들을 만족해야 한다.
* $$P$$의 정의역은 $$\mathrm x$$의 모든 가능한 상태의 집합이어야 한다.
* $$\forall x \in \mathrm x, 0 \leq P(x) \leq 1$$.
* $$\sum_{x \in \mathrm x} P(x) = 1$$. 이 속성을 정규화라고 부른다.

예를 들어, k 개의 다른 상태를 가지는 단일이산확률변수 $$\mathrm x$$를 고려해 보자. 우리는 모든 상태의 가능성이 동일하도록 모든 $$i$$에 대해 확률질량함수를 다음과 같이 설정해서 x에 **균등확률분포(uniform distribution)**를 지정할 수 있다.  
$$ P(\mathrm x = x_i) = \frac{1}{k} \tag{3.1} $$

확률질량함수의 첫 번째 속성을 만족하는지 알아보자. $$k$$가 양수이므로 값 $$1 \over k$$는 양수이다.
$$ \sum_i P(\mathrm x = x_i) = \sum_i {1 \over k} = {k \over k} = 1 \tag{3.2}$$  
이므로, 이 분포는 잘 정규화되어 있다.

#### 3.3.2 Continuous Variables and Probability Density Functions
연속확률변수를 다룰 때에는 확률질량함수 대신 확률밀도함수를 사용해 확률분포를 설명한다. 확률밀도함수가 되지 위해서는, 함수 $$p$$는 다음과 같은 속성을 만족해야 한다.
- $$p$$의 정의역은 x의 가능한 상태의 집합이어야 한다.
- $$\forall x \in \mathrm x, p(x) \geq 0$$. $$p(x) \leq 1$$을 요구하지 않는 점에 주목하라.
- $$\int p(x)dx = 1$$.

확률밀도함수 $$p(x)$$는 특정한 상태의 확률을 직접적으로 주지 않는다. 대신 체적 $$\delta x$$인 극소 영역내부에 안착될 확률이 $$p(x)\delta x$$로 주어진다.

### 3.4 Marginal Probability
우리는 확률변수 집합에 대한 확류분포를 알고 있고, 그 중 일부에 대한 확률분포를 알고 싶을 때가 있다. 부분집합에 대한 확률분포를 **주변확률**분포(**marginal probability** distribution)라고 한다.

예를 들어 이산확률변수 x와 y가 있고 $$P(\mathrm x, \mathrm y)$$를 알고 있다고 하자. 우리는 합 법칙에 따라 $$P(\mathrm x)를 구할 수 있다.

$$
\forall x \in \mathrm x, P(\mathrm x = x) = \sum_y P(\mathrm x = x, \mathrm y = y). \tag{3.3}
$$


"주변확률"이라는 이름은 종이에 주변확률을 계산할 때의 절차로부터 유래되었다. x 값들은 행으로, y 값들은 열로 된 그리드에 $$P(\rm x, y)$$ 값이 쓰여 있을 때, 격자의 행을 따라 합을 구하고, $$P(\rm x)$$를 종이의 오른쪽에 적는 것은 자연스럽다.

연속확률변수에 대해서는, 합 대신 적분이 필요하다.

$$
p(x) = \int p(x, y)dy. \tag{3.4}
$$

### 3.5 Conditional Probability
많은 경우에, 우리는 다른 이벤트가 발생한 사실이 주어졌을 때, 어떤 이벤트의 확률에 관심이 있다. 이를 **조건부 확률(conditional probability)**이라고 부른다. $\mathrm x = x$가 주어졌을 때 $\mathrm y = y$인 조건부 확률을 $P(\mathrm y = y | \mathrm x = x)$으로 표기한다. 이 조건부 확률은 다음 식으로 계산할 수 있다.

$$
P(\mathrm y = y | \mathrm x = x) = {P(\mathrm y = y, \mathrm x = x) \over P(\mathrm x = x)}. \tag{3.5}
$$

### 3.6 The Chain Rule of Conditional Probabilities
많은 확률변수들에 대한 결합확률분포도 오직 하나의 확률변수에 대한 조건부 확률분포로 분해할 수 있다.

$$
P(\mathrm x^{(1)},..., \mathrm x^{(n)}) = P(\mathrm x^{(1)}) \prod_{i=2}^n P(\mathrm x^{(i)} | \mathrm x^{(1)},..., \mathrm x^{(i-1)}) \tag{3.6}
$$

이러한 관찰은 확률의 chain rule 혹은 product rule로 알려져 있다. 이것은 식 3.5의 조건부 확률의 정의로부터 도출된다.

예를 들어, 그 정의를 두 번 적용하면 우리는 다음 결과를 얻을 수 있다.

$$
\begin{align*}
P(a, b, c) &= P(a|b, c) P(b, c) \\
P(b, c) &= P(b|c) P(c) \\
P(a, b, c) &= P(a|b, c) P(b|c) P(c).
\end{align*}
$$

### 3.7 Independence and Conditional Independence
만약 확률분포가 하나는 x만 포함하고 다른 하나는 y만 포함하는 인수의 곱으로 나타낼 수 있다면 두 확률변수 x와 y는 **독립(independent)**이다.

$$
\forall x \in \mathrm x, y \in \mathrm y, p(\mathrm x = x, \mathrm y = y) = p(\mathrm x = x)p(\mathrm y = y) \tag{3.7}
$$

만약 x와 y에 대한 조건부 확률분포가 모든 z값에 대해 이런 식으로 인수분해된다면, 두 확률변수 x와 y는 확률변수 z가 주어졌을 때 **조건부 독립(conditionally independent)**이다.

$$
\forall x \in \mathrm x, y \in \mathrm y, z \in \mathrm z, p(\mathrm x = x, \mathrm y = y | \mathrm z = z) = p(\mathrm x = x | \mathrm z = z)p(\mathrm y = y | \mathrm z = z) \tag{3.8}
$$

독립과 조건부 독립은 압축된 표기법으로 표시하기도 한다. $\rm x \bot y$는 독립을 의미하고, $\rm x \bot y \| z$는 조건부 독립을 의미한다.

### 3.8 Expectation, Variance and Covariance
확률분포 $P(\rm x)$에 따른 어떤 함수 $f(x)$의 **기대(expectation)** 혹은 **기대값(expected value)**은 $x$가 $P$로부터 나올 때 $f$가 가질 수 있는 값의 평균이다. 이산변수에 대해서는 합으로 계산할 수 있고,

$$
\mathbb E_{x \sim P} = \sum_x P(x)f(x) \tag{3.9}
$$

연속변수에 대해서는 적분으로 계산된다.

$$
\mathbb E_{x \sim P} = \int_x p(x)f(x) \tag{3.10}
$$

### Notation for Expectation
확률분포의 식별이 문맥으로부터 분명할 때에는 $\mathbb{E}_{x \sim P}[f(x)]$처럼 기대값을 계산하는 확률변수의 이름만 쓸 수도 있다. 기대값을 계산하는 확률변수가 명확하다면 $\mathbb{E}[f(x)]$처럼 아랫첨자를 완전히 생략할 수도 있다. 기본값으로 $\mathbb{E}[\cdot]$는 각괄호 내 모든 확률변수들에 대한 평균이다. 마찬가지로, 모호성이 없다면 각괄호를 생략할 수도 있다.

기대값은 선형적이다. 예를 들어, $\alpha$와 $\beta$가 $x$에 대해 종속이 아니라면,

$$
\qquad \mathbb{E}_{x}[\alpha f(x) + \beta g(x)] = \alpha \mathbb{E}_{x}[f(x)] + \beta \mathbb{E}_x[g(x)] \tag{3.11}
$$

**분산(variance)**은 확률분포로부터 $x$의 값들이 나올 때, 확률변수 x의 함수의 값이 변하는 정도에 대한 척도이다.  

$$
Var(f(x)) = \mathbb{E} [(f(x) - \mathbb{E}[f(x)])^2] \tag{3.12}
$$

분산이 작을 때, $f(x)$의 값이 기대값 근처에 뭉쳐진다. 분산의 제곱근은 **표준편차(standard deviation)**로 알려져 있다.

### Covariance
공분산은 두 값이 서로 선형적으로 관련된 정도와 이 변수들의 규모에 대한 판별기준을 제공한다.

$$
Cov(f(x), g(x)) = \mathbb{E}[(f(x)-\mathbb{E}[f(x)])(g(x)-\mathbb{E}[g(x)])] \tag{3.13}
$$

공분산의 절대값이 크다는 것은 값이 크게 변하며 각각의 평균으로부터 동시에 떨어져 있음을 뜻한다. 공분산의 부호가 양이면, 두 변수는 동시에 상대적으로 높은 값을 가지는 경향이 있다. 부호가 음이면, 한 변수는 상대적으로 높은 값을 가질 때 다른 변수는 낮은 값을 가지거나 그 반대인 경향이 있다. **상관관계(correlation)** 같은 다른 척도들은 개별 변수들의 비율에 의한 영향 대신 변수들이 연관된 정도만 측정하기 위해 각 변수의 기여도를 normalize한다.

공분산과 종속성의 개념은 관계가 있지만, 사실은 구분되는 개념이다. 독립인 두 변수들은 공분산이 0이고, 공분산이 0이 아닌 두 변수는 의존적이기 때문에 관련이 있다. 하지만, 독립성은 공분산과 구분되는 속성이다. 공분산이 0인 두 변수에 대해 두 변수 사이에 선형적 종속성이 없어야 한다. 독립성은 비선형 관계까지도 배제하기 때문에, 공분산이 0인 것보다 더 강력한 요구조건이다. 예를 들어 구간 [-1, 1]에 대한 균등분포로부터 실수 $x$를 뽑는다고 가정하자. 그 다음으로 확률변수 $s$를 뽑는다. $1 \over 2$ 확률로 $s$를 1로 선택한다. 그렇지 않은 경우 $s$는 -1이 된다. 그러면 $y = sx$로 확률변수 $y$를 생성한다. $x$는 $y$의 크기를 완전히 결정하기 때문에, $x$와 $y$는 분명히 독립이 아니다. 하지만 $Cov(x, v)= 0$이다.

확률변수 벡터 $\boldsymbol x \in \mathbb R^n$의 **공분산 행렬(covariance matrix)**은 다음과 같은 $n \times n$ 행렬이다. 

$$
\mathrm{Cov}(\mathbf x)_{i,j} = \mathrm{Cov}(\mathbf x_i, \mathbf y_j) \tag{3.14}
$$

공분산의 대각 원소는 분산이다.

$$
\mathrm{Cov}(\mathbf x_i, \mathbf x_i) = \mathrm{Var}(\mathbf x_i) \tag{3.15}
$$

### 3.9 Common Probability Distributions
몇 가지 간단한 확률분포들은 머신러닝에서의 많은 맥략에서 유용하다.

#### 3.9.1 Bernoulli Distribution
**베르누이** 분포는 단일 이진 확률변수에 대한 분포다. 이 분포는 단일 파라미터 $\phi \in [0, 1]$에 의해 제어되는데, 이것은 확률변수가 1이 될 확률을 제공한다. 베르누이 분포는 다음과 같은 속성을 가진다.

$$P(\mathrm x = 1) = \phi \tag{3.16}$$  
$$P(\mathrm x = 0) = 1 - \phi \tag{3.17}$$  
$$P(\mathrm x = x) = \phi^x (1- \phi)^{1-x} \tag{3.18}$$  
$$\mathbb E_{\mathbf x}[\mathbf x] = \phi\tag{3.19}$$
$$\rm Var_{x}(x) = \phi(1-\phi) \tag{3.20}$$  

#### 3.9.2 Multinoulli Distribution
