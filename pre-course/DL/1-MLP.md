# Neural Network

- 인간의 뇌를 모방하고자 한 시스템

- neural networks are function approximators that stack affine transformation followed by nonlinear transformation



# Linear Neural Networks

- model: yhat = wx + b
- loss: sum(y - yhat)^2 / N -> mse
- loss function을 파라미터로 편미분하고 이를 통해 gradient descent로 파라미터를 최적화한다.



# Beyond Linear Neural Networks

- 좀 더 레이어를 쌓는다면? -> 결국 행렬의 곱이기 때문에 쌓아봤자 의미 없다

- non-linear transform 필요!

- 활성화 함수: ReLU, Sigmoid, tanh

- 히든 레이어가 하나 있는 neural network는 대부분의 measurable function을 근사할 수 있다. 그러나 뉴럴 네트워크의 표현력만을 의미하는 것. 진짜 찾을 수 있을지는 모른다.

  

# Multi-Layer Perceptron

- 히든 레이어가 1개 이상 있는 perceptron
- loss function은?
  - Regression Task: MSE
  - Classification Task: cross-entrophy
  - probabilistic Task: MLE