# TensorFlow 





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

