---
published: true
---

## Q-learning
Action value를 과대평가하는 경향이 있다. Q-learning의 예측 에러는 지나친 낙관으로 귀결된다.

## Deep Q Network
Target network와 Replay memory가 도입되어 성능이 현저히 증가했다(Mnih et al., 2015).

## Deep Reinforcement Learning with Double Q-learning
[Hado, 2010](https://papers.nips.cc/paper/3964-double-q-learning.pdf)

표준 Q-learning과 DQN에서의 _max_ 연산자는 action을 선택하고 평가하는 두 상황에서 모두 동일한 값을 사용한다. 이는 값을 과대평가하는 결과를 초래하여 지나치게 낙관적인 값 예측을 유발한다.

이를 예방하기 위해 선택과 평가를 분리한다. Single Q-learning은 여러 이유에 의해 upward bias가 생기지만, double Q-learning은 bias를 크게 감소시킨다.

Overestimation은 충분히 flexible한 function에서 일반적으로 생길 수 있다.

예측한 action value가 이미 지나치게 낙관적이라면, value 예측은 보다 더 악화될 수 있다. 값들을 균등하게 과대평가한다면 policy를 손상시키지 않겠지만, 실제 상황에서 서로 다른 상태과 액션에 대해서 과대평가 오차는 차이가 난다.

### Double DQN
[Hado, 2015](https://arxiv.org/abs/1509.06461 "Double DQN")

Double Q-learning의 아이디어는 _max_ 연산을 액션 선택과 평가로 분해하여 과대예측을 줄이는 것이다. 비록 완전히 분리하지는 못하지만, DQN의 target network도 두 번째 value function에 대한 후보이다. 

$$
\DeclareMathOperator*{\argmax}{argmax}
Y_t^{DoubleDQN} \equiv R_{t+1} + \gamma Q(S_{t+1}, \argmax_a Q(S_{t+1}, a; \theta_t); \theta_t^-)
$$

$$\theta_t^-$$: the weight of the target network in Double DQN

$$
Y_t^{DQN} \equiv R_{t+1} + \gamma \max\limits_{a} Q(S_{t+1}, a; \theta_t^\prime)
$$

1. Q-learning이 지나치게 낙관적인 이유
2. 이런 과대예측은 실제 상황에서는 알려진 것보다 일반적이고 심각하다.
3. 지나친 낙관을 줄이기 위해 Double Q-learning가 대규모로 사용될 수 있다.
4. Double DQN이라는 구현을 제안한다.
5. Double DQN이 더 나은 정책을 찾고 Atari 게임들에서 SOTA를 달성했다.

## Dueling Network Architectures for Deep Reinforcement Learning
[Ziyu, 2016](https://arxiv.org/abs/1511.06581 "Dueling Network Architectures for Deep Reinforcement Learning")

Prioritized experience replay(Schaul et al., 2016)는 uniform experience replay에 비해 학습속도도 빠르게 만들고 최종 정책의 품질도 더 좋게 만들었다. Dueling architecture와 함께 적용해서 SOTA를 달성했다.

### 실험방법
* van Hasselt et al. (2015)의 하이퍼파라미터를 기반으로 learning rate 약간 감소.
* Backward pass에서 combined gradient를 $$1 / \sqrt 2$$만큼 rescale하면 안정성이 $1 / \sqrt 2$ 증가.
* 10보가 작거나 같도록 gradient norm clipping. (Clip)

### 실험결과
* Single보다 Single Clip의 성능이 더 좋다.
* Duel

## Asynchronous Methods for Deep Reinforcement Learning
* policy와 value를 각각 계산한다.
  * policy loss는 $$ \log \pi (a_i \| s_i; \theta^\prime)(R - V(s_i;\theta_v^\prime)$$
  * 논문의 value loss는 $$(R - V(s_i; \theta_v^\prime))^2$$이지만, smooth L2 norm을 사용하는 구현도 있음.

## Trust Region Policy Optimization
[joschu et al., 2015](https://arxiv.org/abs/1502.05477, "Trust Region Policy Optimization)



## Proximal Policy Optimization Algorithms
[joschu et al., 2017]()
PPO는 trust region policy optimization(TRPO)의 이점을 가지면서도, 구현하기 쉽고, 일반적이며, 더 나은 샘플 복잡도를 가진다.
* Q-learning: 간단한 문제에서 실패하기도 한다.
* Vanilla policy gradient methods: 데이터를 비효율적으로 사용하고 강건하지 못하다. 
* TRPO: 상대적으로 복잡하고 노이즈나 파라미터 공유를 포함하는 아키텍쳐와 호환이 되지 않는다.




## SARSA
State-action-reward-state-action

## Stock Trading
Deuling architecture는 각 상태에서 선택한 행위가 환경에 영향을 끼치지 않는 경우(예: 주식)에 특히 유용하다.
