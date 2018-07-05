---
published: true
category: deeplearningbook
---
## Page 59

### Notation for Expectation
$$
\qquad \mathbb{E}_{x \sim P}[f(x)] \rightarrow \mathbb{E}_{x}[f(x)] \rightarrow \mathbb{E}[f(x)] \rightarrow \mathbb{E}[\cdot] \rightarrow \mathbb{E}
$$

### Expectation의 선형성
$$
\qquad \mathbb{E}_{x}[\alpha f(x) + \beta g(x)] = \alpha \mathbb{E}_{x}[f(x)] + \beta \mathbb{E}_x[g(x)]
$$

### Variance
확률분포로부터 x의 값들을 샘플링할 때, 확률변수 x의 함수의 값이 변하는 정도에 대한 척도이다.  
$$
\qquad Var(f(x)) = \mathbb{E} [(f(x) - \mathbb{E}[f(x)])^2] = \sigma ^2 = \frac{1}{\beta}
$$

### Covariance
공분산의 절대값이 크다는 것은 값이 크게 변하며 각각의 평균으로부터 동시에 떨어져 있음을 뜻한다.  
$$
\qquad Cov(f(x), g(x)) = \mathbb{E}[(f(x)-\mathbb{E}[f(x)])(g(x)-\mathbb{E}[g(x)])]
$$

### Correlation
각 변수들의 스케일에 의한 영향 대신 변수들이 관련된 정도만 측정하기 위해 각 변수의 기여도를 normalize한다.

### Independence and Covariance
독립은 비선형관계도 제외하기 때문에 0 공분산보다 더 강력한 요건이다.

## Page 70
### [Measure theory](http://mathworld.wolfram.com/MeasureTheory.html)
모든 이산 값들에 대해서는 확률이론에서의 중요한 결과들이 유지되지만, 연속 값들에 대해서는 "almost everywhere"일 때에만 유지된다.

### Random Variable Transformation
두 연속확률변수 x와 y가 있고, $$\textbf{y} = g(\textbf{x})$$라고 하자. $$p_y(\textbf{y})=p_x(g^{-1}(\textbf{y}))$$일 것 같지만 사실은 그렇지 않다.

$$
\begin{align*}
\qquad &x \sim U(0, 1) \\
&y = \frac{x}{2} \\
&p_y(y) = \begin{Bmatrix}
1 \, &if \; 0\leq y \leq 1/2\\ 
0 \, &otherwise \\
\end{Bmatrix} \\
&p_y(y) = p_x(2y) \\
&\int p_y(y)dy = \frac{1}{2}
\end{align*}
$$  
이는 y에 대한 확률분포의 정의를 위반했다.

이를 바로잡기 위해서는 매핑함수 g의 변화율을 고려해야 한다. 먼저 스칼라 경우로 돌아가 보면,  
$$
\begin{align*}
\qquad &|p_y(g(x))dy| = |p_x(x)dx| \\
&p_y(y) = p_x(g^{-1}(y)) \left |\frac{\partial x}{\partial y}\right | = \frac{p_x(g^{-1}(y))}{\left |\frac{\partial y}{\partial x}\right |} \\
&p_x(x) = p_y(g(x)) \left |\frac{\partial g(x)}{\partial x}\right |
\end{align*}
$$

고차원에서는 도함수 부분이 **Jacobian matrix**의 행렬식으로 일반화된다.  
$$
\qquad p_x(x) = p_y(g(x)) \left |det(\frac{\partial g(x)}{\partial x})\right |
$$

매핑함수가 선형이면 Jacobbian matrix는 선형변환 A이고, det(A)는 n차원 볼륨에 대한 scaling factor다.  
$$
\qquad p_y(y) = \frac{p_x(x)}{\left|det(A)\right|}
$$

Probability measure 관점에서 표현하면,  
$$
\begin{align*}
\qquad &g: S \rightarrow S^\prime \\
&\int_{x \in S} p_x(x)dx = \int_{y \in S^\prime} p_x(g^{-1}(y)) \left | \partial x \over \partial y \right | dy \\
&\therefore p_y(y) = p_x(g^{-1}(y)) \left | \partial x \over \partial y \right |
\end{align*}
$$
