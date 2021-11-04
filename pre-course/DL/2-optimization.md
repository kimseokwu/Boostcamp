# Introduction

- Gradient Descent: 1차 미분 값을 사용해 local minimum을 향해 반복적으로 최적화 시킨다.



# Important Concepts in Optimization

- generalization
- under-fitting vs over-fitting
- cross validation
- bias-variance tradeoff
- bootstrapping
- bagging and boosting



# Generalization

- 새로운 데이터에 모델이 얼마나 잘 적용될 것인가
- Underfitting vs. Overfitting



# cross-validation

- train data와 validation data를 나누는 경우가 많음. validation data로 모델의 성능을 검증
- train/validation 비율은?
- cross-validation: data를 k개로 나눠서 k-1개로 학습하고 1개로 validation
- cross-validation으로 최적의 parameter를 찾고 실제로 모델을 학습시킬땐 모든 데이터를 사용한다. test 데이터는 학습에 어떤 방식이던 사용되면 안됨



# Bais and Variance

- High Variance: 얼마나 출력이 일관적?
- High Bias: 평균적으로 출력이 true target에 접근하고 있는가?
- Bias and Variance Tradeoff: bias를 줄이면 variance가 늘어나고 variance가 줄어들면 bias가 늘어난다.



# Bootstrapping

- 랜덤 샘플링을 이용해서 만든 여러 모델들의 컨센서스를 보고 전체적인 uncertainty를 예측하려고 함
- Bagging vs Boosting
  - bagging: 여러 모델을 부트스트랩으로 만듦, 여러 모델의 결과값을 투표나 평균을 내서 최종 결과값을 냄(모델들이 독립적)
  - boosting: 간단한 모델을 만들고 다음 모델을 전 모델이 잘 예측하지 못하는 부분에 성능을 좋도록 만들어서 여러 모델을 sequential 하게 만듦으로써 strong learner를 만드는 것(모델들이 독립적이지 않음)



# Gradient Descent Methods

- sotchastic gradient descent: 하나의 샘플만을 이용
- min-batch gradient descent: batch size를 이용
- batch gradient descent: 한번에 모든 데이터를 사용
- momentum: 모멘텀과 현재 gradient vector를 합쳐 accumulation을 만들고 다음으로 최적화를 넘김
- nesterov accelerated gradient: lookahead gradient로 local minimum에 잘 들어감
- adagrad: 패러미터가 지금까지 얼마나 많이 변했는지 고려, 많이 변한 패러미터는 적게, 적게 변한 패러미터는 많이 변화시킴, 뒤로가면 갈수록 학습이 멈춰지는 부작용
- adadelta: adagrad 개선, learnig rate이 없음
- rmsprop: step size 추가
- adam: gradient square와 모멘텀을 같이 사용, adaptive + momentum



# Batch-size matter

- 배치사이즈가  크면 sharpe minimizer, 배치사이즈가 작으면 flat minimizer(새로운 데이터에 잘 작동)



# Regularization

- early stopping: validation error를 보고 학습을 먼저 멈춤
- parameter norm penalty: 패러미터가 너무 커지지 않게 함, 함수를 최대한 부드럽게 만듦
- data augmentation: 더 많은 데이터는 언제나 옳다. 주어진 데이터를 조작해서 새 데이터를 만들어서 데이터를 늘린다. 레이블이 변환되지 않는 조건 하에서
- nois robustness: 입력데이터에 랜덤 노이즈를 만든다.
- label smoothing: 학습데이터 두개를 뽑아서 섞는다.(cutmix)
- dropout: 일부 weight을 0으로 바꿔준다.
- batch normalization: 적용하고자 하는 layer의 statistic을 정교화 시킴
