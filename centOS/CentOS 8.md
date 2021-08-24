# CentOS 8





## 1. 리눅스 입문

- GNU 프로젝트(Genetal Public License)
- 운영체제 3개 요소: 커널, 쉘, 사용자 프로그램



- date
- clear
- history
- who
- env



- 리눅스에서의 파일 개념 : 파일 이름, I-node, 데이터 블록
- 모든 데이터는 파일이라는 인터페이스를 가짐
- 모든 파일은 확장명이 없음



### I-node

- 인덱스 노드
- 하나의 파일을 생성하면 하나의 I node가 생성



### 링크 파일

- 여러 개의 이름이 하나의 I node에 연결되도록 함





## 리눅스 에디터

- mkdir: make directory
- rmdir: remove directory
- touch: 빈 파일 생성

```
alias c=clear 누르면
c만 쳐도 clear 됨
```

- cp: copycp
- cat: 파일 내용 연속출력
- pwd: 현재 위치를 절대 경로로 보여줌
- more: 한 페이지 단위로 파일 내용 출력
- ln: 링크파일 생성



### vi 에디터

```
vi bashrc
```

- 명령/입력/라인 모드



### 파일접근 권한설정



