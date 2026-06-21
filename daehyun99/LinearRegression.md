- https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html#sklearn.linear_model.LinearRegression

# LinearRegression

> [class sklearn.linear_model.LinearRegression(*, fit_intercept=True, copy_X=True, tol=1e-06, n_jobs=None, positive=False)](https://github.com/scikit-learn/scikit-learn/blob/cc50648cc/sklearn/linear_model/_base.py#L519)

일반적인 최소제곱법 선형회귀 <br>

`LinearRegression`은 데이터셋의 관찰된 값과 선형 근사로 예측된 값 사이의 잔차의 제곱합(`residual sum of squares`, `RSS`)을 최소화하는 방향으로 선형 모델을 계수와 함께 학습한다. <br>

> Parameters:

- `fit_intercept`: `bool`, `default=True`
    - 이 모델의 절편(`intercept`)를 계산하는지. 만약 `False`로 설정되어 있다면, 계산에 절편을 사용하지 않는다. (즉, 데이터가 중심이 될 것이다.)
- `copy_X`: `bool`, `default=True`
    - 만약 `True`라면, X는 복사될 것이다; 아니면, 아마 오버라이드된다.
- `tol`: `float`, `default=1e-6`
    - `coef_`는 `tol`에 의해 결정된다. `tol`은 희소 학습 데이터에서 `scipy.spare.linalg.lsqr`의 `atol`과 `btol`로 설정된다. `tol`은 밀집 학습 데이터에서 `scipy.linalg.lstsq`의 `cond`로 설정된다.
- `n_jobs`: `int`, `default=None`
    - 계산을 위한 job의 갯수이다. 이것은 오직 충분히 큰 문제의 경우에만 속도 향상을 제공할 것이다.(첫 번째로 `n_targets > 1`이고, 두 번째로 `X`가 희소하거나 `positive` 설정이 `True`인 경우에 대해) <br>`None`은 1을 의미한다. (`joblib.parallel_backend` 맥락을 제외하고는) <br>`-1`은 모든 프로세스 사용을 의미한다. <br>`Glossary`에서 자세한 정보를 확인하라.
- `positive`: `bool`, `default=False`
    - `True`로 설정된 경우, 계수를 양수로 강제한다. 이 설정은 밀집 행렬의 경우에만 지원한다.
    - "회귀 계수에 양의 제한이 있는 선형 모델"과 "제한이 없는 선형 모델" 간의 비교를 위해, `Non-negative least squares`를 참고하라.

> Attributes:

- `coef_`: 배열의 형태 `(n_features, )` 또는 `(n_targets, n_features)`
    - 추정된 선형 회귀 문제의 계수. 만약 모델 학습 간에 여러 타겟 값이 주어진다면, 예를 들어`y`가 2D라면, `coef_`의 형태는 2D 배열 형태(`(n_targets, n_features)`)이다. 반면에, 오직 1개의 타겟 값이 통과된다면, 이것은 1D 배열의 길이(`n_features`)가 된다.
- `rank_`: `int`
    - 행렬 `X`의 랭크이다. 오직 `X`가 밀집 행렬일 때만 사용 가능하다.
- `singular_`: 배열의 형태 (`(min(X, y),)`)
    - `X`의 Singular 값이다. 오직 `X`가 밀집 행렬일 때만 사용 가능하다.
- `intercept_`: `float` 또는 배열의 형태 (`(n_targets, )`)
    - 선형 모델과 독립적인 항이다. 만약 `fit_intercept=False`라면, `0.0`으로 설정된다.
- `n_features_in_`: `int`
    - `fit()` 실행 중에 관측되는 `feature`의 갯수
- `feature_names_in_`:  배열의 형태 (`(n_features_in_, )`) 
    - `fit()` 실행 중에 관측되는 `feature`의 이름 갯수. 오직 `X`가 모든 문자열 feature 이름을 가질 때 정의된다.

> Notes:

개발의 관점에서, 이 모델은 단순히 일반 최소 제곱법 또는 비음수 최소 제곱법을 예측기 객체 형태로 감싼 것이다.

> Examples:
```py
import numpy as np
from sklearn.linear_model import LinearRegression
X = np.array([[1, 1], [1, 2], [2, 2], [2, 3]])
# y = 1 * x_0 + 2 * x_1 + 3
y = np.dot(X, np.array([1, 2])) + 3
reg = LinearRegression().fit(X, y)
reg.score(X, y) # 1.0
reg.coef_ # array([1., 2.])
reg.intercept_ # np.float64(3.0)
reg.predict(np.array([[3, 5]])) # array([16.])
```

---
### 단어장

- `coefficient`: 계수
- `residual`: 잔차
- `intercept`: 절편
- `sum of squares`: 제곱합(표준편차)
- `precision`: 정확
- `sparse`: 희소한
- `dense`: 밀집
- `unless in`: ~의 경우를 제외하고
- `term`: 항
