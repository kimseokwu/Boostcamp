# Sequential model

- 입력이 여러개 들어올때 다음 값을 예측

- fix the time span: 입력할 과거 데이터를 고정(이전 2개의 데이터만 본다 등등)
- Markov model: 나의 현재는 바로 전 과거에만 dependant 하다 하지만 현실에 잘 맞지 않음
- Latent autoregressive model: input과 output 사이에 hidden state가 있음. hidden state는 과거의 정보를 summarize 하고 있다. 다음번 타입스텝은 히든 스테이트 하나에만 dependant하다.



# Recurrent Neural Network

- 자기 자신으로 돌아오는 구조가 있어서 과거 데이터들을 모두 반영함
- 시간순으로 풀면 입력이 굉장히 많은 fully connected layer로 표현 가능

- 단점) short-term dependencies: RNN은 하나의 fixed rule로 과거 정보를 모두 취합하기 때문에 데이터가 가면 갈수록 희석됨
- 과거의 데이터를 계속 입력하면 계속 값이 활성화함수를 중첩해서 통과하기 때문에 vanishing이 일어남, ReLU의 경우 계속 weight를 곱하기 때문에 exploding이 일어남



# Long Short Term Memory 

- 이전의 출력값(previous cell state), previous cell state, input data가 입력된다.
- core idea: cell state, 타임스텝 t까지 들어오는 정보를 요약
- forget gate: 어떤 정보를 버릴지 결정 현재의 input, 이전의 output이 들어감
- input gate: 어떤 정보를 cell state에 저장할 지 결정
- update cell: cell state 업데이트
- output gate: cell state를 이용해 output을 결정



# Gated Recurrent Unit

- 게이트가 두개
- cell state가 없음, hidden state만 존재
- reset gate
- update gate
- LSTM보다 GRU의 성능이 올라가는 경우가 있음(패러미터가 적음)
- transformer가 나오면서 RNN구조가 transformer로 바뀌고 있음