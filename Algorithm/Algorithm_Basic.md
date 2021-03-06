# 최적의 코딩을 결정하는 기본 알고리즘

빅데이터 기반 지능형 서비스 개발 수업

24차시

강사 나동빈





## 1. 가장 기본이 되는 자료구조: 스택과 큐



### 1.1 스택 자료구조

- 선입후출의 자료 구조

- 프링글스 과자통과 비슷한 출입구가 통일한 형태
- Python에서는 리스트, append와 pop으로 구현 가능



### 1.2 큐 자료구조

- 선입선출의 구조
- 입구와 출구와 모두 뚫려있는 터널과 같은 형태
- 먼저 들어온 자료가 먼저 나가는 형태
- Python에서는 deque 라이브러리 사용함, append와 popleft로 구현가능



## 2. 우선순위에 따라 데이터를 꺼내는 자료 구조



### 2.1 우선순위 큐(Priority Queue)

- 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료 구조
- 리스트 이용하거나 - 복잡도1, 삭제시간 N
- 힙(heap)을 이용하여 구현 - 복잡도 logN, 삭제시간 logN



#### 힙(heap)

- 완전 이진 트리
  - Complete Binary Tree
  - 루트 노드부터 시작하여 왼쪽 자식 노드, 오른쪽 자식 노드 순서대로 데이터 삽입
- 루트 노드를 제거하는 방식
  - 최소 힙(min heap): 루트 노드가 가장 작은 값을 가짐
  - 최대 힙(max heap): 루트 노드가 가장 큰 값을 가짐

##### 최소 힙 구성함수 Min-Heapify()

- 상향식: 부모 노드로 거슬러 올라가며, 부모보다 자신의 값이 더 작은 경우에 위치를 교체
- 힙에 새로운 원소가 삽입될 때, logN의 시간 복잡도로 힙 성질 유지
- 힙에서 원소가 제거될 때 마지막 노드가 루트 노드의 위치에 오도록 함
- Python에서는 heapq 라이브러리 이용, heappush로 구현
- max 쓰고 싶으면 -를 붙이면 됨



## 3. 활용도가 높은 자료구조: 트리 자료구조



### 3.1 트리(Tree)

- 가계도와 같은 계층적인 구조 
- root node: 부모가 없는 최상위 노드
- 단말 노드 leaf node: 자식이 없는 노드
- 트리의 크기가 n일 때, 전체 간선의 개수는 n-1개



### 3.2 이진 탐색 트리(Binary Search Tree)

- 이진 탐색이 동작할 수 있도록 고안된 자료 구조
- 왼쪽 자식 노드 < 부모 노드 < 오른쪽 자식 노드
- 루트 노드부터 방문해서 탐색 진행, 오른/왼 보고 찾고자 하는 자료와 가까운 곳으로 이동



### 3.3 트리의 순회(Tree Traversal)

- 노드에 한 번씩 방문하는 방법
  - 전위 순회(pre-order): 루트 먼저 방문
  - 중위 순회(in-order): 왼쪽 먼저 방문
  - 후회 순회(post-order): 오른쪽 먼저 방문
- Python에서는 노드 Class로 구현



## 4. 특수한 목적의 자료구조: 바이너리 인덱스 트리



### 4.1 바이너리 인덱스 트리(Binary Indexed Tree)

- 데이터의 변경이 가능한 상황에서에 합을 구해야 할 때
- 2진법 인덱스 구조를 활용해 문제 해결
- 펜윅 트리(fenwick tree)라고도 함
- 정수에 따른 2진수 표기: K & -K 로 계산
- 누적 합 구할때: Prefix Sum, 0이 아닌 마지막 비트만큼 빼면서 구간들의 값의 합 계산



### 4.2 트리 구조 만들기

- 0이 아닌 마지막 비트 = 내가 저장하고 있는 값들의 개수

- 특정 값을 변경할 때: 0이 아닌 마지막 비트만큼 더하면서 구간들의 값을 변경





## 5. 정렬 알고리즘(선택과 삽입)

- 정렬(Sorting)은 데이터를 특정한 기준에 따라 순서대로 나열하는 것



### 5.1 선택 정렬

- 처리되지 않은 데이터 중 가장 작은 데이터를 선택해서 맨 앞에 있는 것과 바꿈
- Python에서는 min_index로 선형 탐색을 시작하여 특정 원소와 스와프 연산으로 표현
- 복잡도는 O(N**2)



### 5.2 삽입 정렬

- 처리되지 않은 데이터를 골라서 적절한 위치에 삽입
- 구현 난이도가 높고, 효율적으로 작용
- 두번째 데이터부터 첫번째 데이터의 오른/왼 비교하여 적절한 위치에 삽입
- Python에서는 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
- 시간 복잡도 0(N**2)



## 6. 퀵 정렬과 계수 정렬



### 6.1 퀵 정렬

- 기준 데이터보다 큰 데이터와 작은 데이터의 위치를 바꿈
- 대부분의 정렬 라이브러리에서 사용됨
- 첫번째 데이터를 Pivot으로 설정
- 피벗을 기준으로 왼쪽에서는 큰 데이터, 오른쪽에서는 작은 데이터를 골라서 위치 변경
- 데이터가 왼/오른이 분할(Divide) 됨
- 이상적인 경우, 분할이 절반씩 일어난다면 NlogN = 너비 X 높이



- Python에서는 피벗보다 큰/작은 데이터를 찾을 때까지 반복, 엇갈렸다면 작은 데이터를 교체
- 리스트 슬라이싱, 표현식으로 사용



### 6.2 계수 정렬

- 특정한 조건이 부합할 때만 사용, 매우 빠르게 동작
- 정수로 표현할 수 있을 때만 사용 가능
- 각각의 데이터를 count하는 방법 (상수 시간에 접근 가능,,,?)
- Python에서는 각 데이터에 해당하는 인덱스의 값을 1씩 증가, 리스트에 기록된 정렬 정보 확인
- 동일한 데이터가 여러 개 등장할 때 효과적으로 사용 





## 7. 정렬 알고리즘 비교



- 선택 정렬: 아이디어가 간단
- 삽입 정렬: 데이터가 거의 정렬되어 있을 때는 가장 빠름
- 퀵 정렬: 가장 많이 쓰이는 정렬, 충분히 빠름
- 계수 정렬: 데이터의 크기가 한정된 경우만 가능, 빠르게 동작





## 8. DFS(Depth-First Search)와 BFS(Breadth-First Search)



### 8.1  DFS(Depth-First Search)

- 깊이 우선 탐색, 깊은 부분을 우선적으로 탐색
- 탐색 노드를 스택에 삽입하고 -> 최상단 노드에 방문하지 않은 노드를 스택에 넣고 -> 인접 노드가 없으면 스택에서 최상단 노드를 꺼냄 (뭔소리야..)
- Python에서는 2차원 그래프로 구현



### 8.2 BFS(Breadth-First Search)

- 너비 우선 탐색, 그래프에서 가까운 노드부터 우선 탐색
- 큐 자료구조 이용
- 큐에서 노드를 꺼내고 -> 인접 노드를 모두 큐에 삽입



## 9. 그래프 탐색 실습

- 음료수 얼려먹기 문제
- 미로 탈출



## 10. 다익스트라 알고리즘

- 최단 경로 알고리즘: 가장 짧은 경로를 찾는 알고리즘
- 음의 간선이 없을 떄만 가능
- 그리디 알고리즘으로 분류



### 10.1 동작과정

1. 출발 노드 설정 (0으로 시작)
2. 최단 거리 테이블 초기화
3. 방문하지 않은 노드 중에서 최단거리 노드 선택
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블 갱신
5. 3~4 반복



- 처리 과정에서 더 짧은 경로 발견하면 최단 경로 갱신함
- 그리디 알고리즘: 방문하지 않은 가장 비용이 적은 노드 선택
- 한 번 처리된 최단 거리는 고정
- 완전한 형태로 구하려면 추가 코드가 필요
- O(V)번에 걸쳐서 최단 거리가 가장 짧은 노드를 매번 선형 탐색



### 10.2 우선순위 큐

- 우선 순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료 구조
- 리스트, 힙(heap)으로 구현함





## 11. 플로이드 워셜 알고리즘

- 모든 출발지에서 다른 모든 출발지까지 최단 경로 계산
- 단계별로 거쳐가는 노드를 기준으로 알고리즘 수행
- 매 단계마다 방문하지 않은 노드 중에 최단 거리를 찾는 노드를 찾는 과정이 발생하지 않음
- 다이나믹 프로그래밍 유형
- 각 단계마다 특정한 노드를 거쳐가는 경우를 확인
- 노드의 개수가 N개일 때 N번의 단계 수행



### 11.1 동작과정

- 초기 상태: 최단 거리 테이블 초기화
  1. 1번 노드를 거쳐가는 경우를 고려하여 테이블 생성
  2. 2번 노드를 거쳐가는 경우를 고려하여 테이블 생성
  3. 3번 노드를 거쳐가는 경우를 고려하여 테이블 생성
  4. 4번 노드를 거쳐가는 경우를 고려하여 테이블 생성





## 12. 벨만 포드 알고리즘

- 음수 간선이 포함된 상황에서의 최단 거리 문제



### 12.1 동작과정

1. 출발노드 설정
2. 최단 거리 테이블 초기화
3. 간선 E개 확인 -> 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블 갱신



### 12.2 다익스트라와의 비교

- 다익스트라: 매번 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드 선택
- 매번 모든 간선 전부 확인



## 13. 서로소(Disjoint Sets) 집합 알고리즘

- 공통 원소가 없는 두 집합 
- 합집합(Union): 두 개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산
- 찾기(Find): 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산
- UnionFind 연산



### 13.1 자료 구조

- 합집합 연산을 확인하여 서로 연결된 두 노드 A,B를 확인

- A를 B의 부모 노드로 설정

- 루트 노드에 즉시 접근할 수 없음

- ex) 노드 3의 루트를 찾기 위해서는 노드 2를 거쳐 노드 1에 접근

- 문제점: Union 과정이 편향되게 이루어지면 Find 함수가 비효율적으로 동작

- 경로압축(Path Compression): 찾기 함수를 재귀적으로 호출하여 부모 테이블 값을 바로 갱신

  



### 13.2 동작 과정

- 초기: 노드의 개수 크기의 부모 테이블 초기화
- 큰 루트 노드의 부모를 작은 루트 노드로 설정
- 각 노드의 부모 노드를 찾아 집합의 형태를 확인



### 13.3 서로소 집합을 활용한 사이클 판별

- 무방향 그래프 내에서의 사이클 판별
- 간선을 하나싹 확인하여 루트 노드 확인
  - 루트 노드가 다르면 합집합 연산 수행
  - 루트 노드가 같다면 사이클 발생
- 초기단계: 모든 노드에 대하여 자기 자신을 부모로 설정하는 형태로 부모 테이블 초기화





## 14. 크루스칼 알고리즘

- 최소 신장 트리를 찾는 알고리즘
- 그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프



### 14.1 최소 신장 트리

- N개의 도시에 존재하는 상황에서 두 도시 사이에 도로를 놓아 전체 도시가 서로 연결될 수 있게 도로 설치
- 최소 신장 트리에 포함되어 있는 간선의 비용만 더하면, 그 값이 최종 비용



### 14.2 동작과정

1. 간선 데이터를 비용에 따라 오름차순 정렬
2. 간선을 하나씩 확인하며 현재의 간선이 사이클을 발생시키는지 확인
   - 사이클이 발생하지 않는 경우 최소 신장 트리에 포함

초기단계: 그래프의 모든 간선 정보에 대해 오름차순 정렬



## 15. 최소 공통 조상(Lowest Common Ancestor)

- 두 노드의 공통된 조상 중에서 가장 가까운 조상 찾는 문제
- DFS를 이용해 모든 노드에 대해 깊이 계산



### 15.1 동작과정

1. 모든 노드에 대한 깊이 계산하여 깊이를 맞춤

2. 최소 공통 조상을 찾을 두 노드 확인

3. 부모가 같아질 때까지 반복적으로 두 노드 방향으로 거슬러 올라감





## 16. 위상 정렬

- 방향성을 거스르지 않도록 전체 노드를 나열하기
- 진입차수(Indegree): 특정한 노드로 들어오는 간선의 개수
- 진출차수(Outdegree): 특정한 노드에서 나가는 간선의 개수
- DAG(Direct Acyclic Graph) 순환하지 않는 방향 그래프에 대해서만 수행
- 여러가지 답이 존재할 수 있음
- 모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재한다고 판단



### 16.1 동작과정

- 큐를 이용하여 구상
- 진입차수가 0인 모든 노드에 큐를 넣고
- 큐가 빌 때까지 다음의 과정을 반복
- 결과적으로 각 노드가 큐에 들어온 순서가 위상 정렬을 수행한 결과와 같음





## 17. 재귀함수

- Recursive Funtion: 자기 자신을 다시 호출하는 함수

  
