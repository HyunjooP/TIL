# Deep Learning



## 1) TensorFlow 



Data flow graph를 기반으로 하는 numerical computation을 하는 오픈 소스 소프트웨어 라이브러리



- Directed Acyclic Graph(DAG)
- 수치 계산과 데이터의 흐름을 Node와 Edge를 사용한 양방향 그래프로 표현
  - 노드: 수치 연산
  - 엣지: 노드 사이를 이동하는 다차원 데이터 텐서



- 특징 및 장점
  - 코드 수정 없이 데스크탑, 서버 혹은 모바일 디바이스에서 CPU나 GPU, TPU(Tensor Processing Unit)를 사용하여 연산을 수행
  - 분산 실행환경이 가능
  - 아이디어 테스트에서 서비스 단계까지 모두 이용 가능
  - 계산 구조와 목표함수만 정의하면 자동으로 미분 계산 처리



- Install

```
conda install tensorflow

pip install tensorflow
```



- 모델 컴파일
  - 손실함수: 훈련하는 동안 모델의 오차를 측정. 모델의 학습이 올바른 방향으로 향하도록 이 함수 값을 최소화 해야 함
  - 옵티마이저(optimizer) - 데이터와 손실함수를 바탕으로 모델의 업데이트 방
    법을 결정
  - 지표(metrics) - 훈련 단계와 테스트 단계를 모니터링 하기 위해 사용
- 모델 훈련
  - 훈련 데이터를 모델에 주입
  - 모델이 이미지와 레이블을 맵핑
  - 테스트 세트에 대한 모델의 예측
- 



## 2) Neural Network



- 신경망 훈련 요소
  - 네트워크(또는 모델)를 구성하는 층(layer)
  - 입력 데이터와 그에 상응하는 타깃(target)
  - 학습에 사용할 피드백 신호를 정의하는 손실함수(loss function)
  - 학습 진행 방식을 결정하는 옵티마이저(optimizer)
- Layer
  - 딥러닝의 구성 단위
  -  하나 이상의 텐서를 입력으로 받아 하나 이상의 텐서를 출력하는 데이터 처리 모듈
  - 대부분의 경우 가중치라는 층의 상태를 가짐
  - 가중치는 확률적 경사 하강법(SGD)에 의해 학습되는 하나 이상의 텐서이며 여기에 네트워크가 학습한 지식이 담겨 있음
- 텐서 포맷과 데이터 처리 방식
  - (samples, features) 크기의 2D텐서가 저장된 간단한 벡터 데이터는 완전 연결층(fully connected layer)나 밀집층(dense layer)이라고도 불리는 밀집연결층(densely connected layer)에 의해 처리되는 경우가 많음
  - (samples, timesteps, features) 크기의 3D 텐서로 저장된 시퀀스 데이터는 보통 LSTM같은 순환층(recurrent layer)에 의해 처리
  - 4D 텐서로 저장되어 있는 이미지 데이터는 일반적으로 2D 합성곱 층(convolution layer)에 의해 처리
- 층 호환성(layer compatibility) - 각 층이 특정 크기의 입력 텐서만 받고 특정크기의 출력 텐서를 반환한다는 사실을 말함
- 호환 가능한 층들을 엮어 데이터 변환 파이프라인(pipeline)을 구성하여 딥러닝 모델을 만듦
- 딥러닝의 레고 블록처럼 생각할 수 있음



- Model
  - 층의 네트워크
  - 하나의 입력을 하나의 출력으로 매핑하는 층을 순서대로 쌓는 것



- 손실함수(loss function)
  - 훈련하는 도안 최소화 될 값 → 주어진 문제에 대한 성공지표
  - 분류, 회귀, 시퀀스 예측 같은 일반적인 문제에서는 올바른 손실 함수를 선택하는
    간단한 지침이 존재
  - 2개의 클래스 분류 - 이진 크로스엔트로피(binary crossentropy)
  - 여러개의 클래스 분류 - 범주형 크로스엔트로피(categorical crossentropy)
  - 회귀 - 평균 제곱 오차(mean square error, MSE
  - 시퀀스 학습 - CTC(Connected Temporal Classification)





- 옵티마이저(optimizer)
  - 손실함수를 기반으로 네트워크가 어떻게 업데이트될지 결정. 특정 종류의 확률적 경사 하강법(SGD)을 구현





## 3) CNN(Convolution Neural Network)



- 이미지의 공간정보를 유지한 상태로 학습 가능한 모델
- 각 레이어의 입출력 데이터의 형상 유지
- 이미지의 공간 정보를 유지하면서 인접 이미지와의 특징을 효과적으로 인식
- 복수의 필터로 이미지의 특징 추출 및 학습
- 추출한 이미지의 특징을 모으고 강화하는 Pooling layer
- 필터를 공유 파라미터로 사용하기 때문에, 일반 인공 신경망과 비교하여 학습 파라미터가 매우 적음



구조

- 이미지의 특징을 추출(feature extraction)하는 부분과 클래스를 분류(classification)하는 부분으로 나눌 수 있음
- 특징 추출 영역은 convolution layer와 pooling layer를 여러 겹 쌓는 형태로 구성
- 마지막 부분에는 이미지 분류를 위한 fully-connected layer가 추가
- 이미지의 특징을 추출하는 부분과 이미지를 분류하는 부분 사이에 이미지 형태의 데이터를 배열 형태로 만드는 flatten layer가 위치







## 4) Transfer Learning



### 4.1) Cat vs. Dog





