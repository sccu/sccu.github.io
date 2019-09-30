# Parameters Tuning

(원본: https://lightgbm.readthedocs.io/en/latest/Parameters-Tuning.html)  

이 페이지는 서로 다른 시나리오들을 위한 파라미터 튜닝 가이드를 포함한다.

**List of other helpful links**
- [Parameters](https://lightgbm.readthedocs.io/en/latest/Parameters.html)
- [Python API](https://lightgbm.readthedocs.io/en/latest/Python-API.html)

## Leaf-wise (Best-first) 트리를 위한 파라미터 튜닝

LightGBM은 [leaf-wise](https://lightgbm.readthedocs.io/en/latest/Features.html#leaf-wise-best-first-tree-growth) 트리 성장 알고리즘을 사용하는 반면, 다른 많은 인기있는 도구들은 depth-wise 트리 성장을 사용한다. Depth-wise 성장과 비교하면, leaf-wise 알고리즘은 훨씬 빨리 수렴한다. 하지만, leaf-wise 성장은 적절한 파라미터와 함께 사용되지 않는다면 overfitting될 수 있다.

Leaf-wise 트리를좋은 결과를 얻기 위해 중요한 파라미터들이 있다.

1. `num_leaves`. 이것은 트리 모델의 복잡도를 통제하는 주요 파라미터다. 이론적으로, 우리는 depth-wise 트리와 동일한 leaf 수를 얻기 위해  `num_leaves = 2^(max_depth)`로 설정할 수 있다. 이런 간단한 변환은 실전에서는 좋지 않다. 이유는 leaf-wise 트리는 전형적으로 고정된 leaf 수에 대해 depth-wise 트리보다 훨씬 깊기 때문이다. 제약이 없는 깊이는 overfitting을 유발할 수 있다. 그리하여, `num_leaves`를 튜닝할 때에는, `2^(max_depth)`보다 작도록 해야 한다. 예를 들어, `max_depth=7`일 때 depth-wise 트리가 좋은 정확도를 보이지만, `num_leaves`를 127로 설정해서 overfitting이 생긴다면, 70이나 80으로 설정하면 depth-wise 트리보다 성능이 나을 수도 있다.
2. `min_data_in_leaf`. 이것은 leaf-wise 트리에서 overfitting을 막기 위해 매우 중요한 파라미터이다. 이 파라미터의 최적값은 훈련 샘플 수와 `num_leaves`에 달려 있다. 이 파라미터를 큰 값으로 설정하면 트리가 너무 깊어지는 것을 막을 수 있지만, underfitting을 유발할 수 있다. 실전에서는 큰 데이터셋에 대해 수백에서 수천 정도로 설정하면 충분하다.
3. `max_depth`. 트리 깊이를 명시적으로 제한하기 위해 설정할 수 있다.

## For Faster Speed
- `bagging_fraction`과 `bagging_freq`를 설정해서 배깅 사용하기
- `feature_fraction`을 설정해 feature sub-sampling 사용하기
- 작은 `max_bin` 사용하기
- `save_binary`을 사용해 향후 학습에서 데이터 로딩 속도 올리기
- 병렬 학습 사용하기

## For Better Accuracy
- 큰 `max_bin` 사용하기 (속도가 저하될 수 있음).
- 작은 `learning_rate`를 큰 `num_iterations`와 함께 사용
- 큰 `num_leaves` 사용 (overfitting을 유발할 수 있음)
- 더 큰 훈련데이터 사용
- `dart` 시도하기

## Deal with Over-fitting
- 작은 `max_bin` 사용
- 작은 `num_leaves` 사용
- `min_data_in_leaf`와 `min_sum_hessian_in_leaf` 사용 
- `bagging_fraction`과 `bagging_freq`를 설정해 배깅 사용 
- `feature_fraction`을 설정해 feature sub-sampling 사용 
- 더 큰 훈련데이터 사용
- Regularization을 위해 `lambda_l1`, `lambda_l2`와 `min_gain_to_split` 시도 
- 깊은 트리 성장을 피하기 위해 `max_depth` 시도
