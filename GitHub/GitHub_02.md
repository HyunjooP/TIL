# Git 특강



## 협업 Flow



- 작업 전 상태확인 필수

```
$ git status
```



### branch

master - 웬만하면 작업 브랜치로 사용하지 말 것.

feature - 기능별 개발 브랜치





브랜치 생성

```
(master) $ git branch {branch name}
```



브랜치 이동

```
(master) $ git branch {branch name
```



브랜치 생성 및 이동

```
(master) $ git checkout -b {branch name
```



브랜치 목록

```
(master) $ git branc
```



브랜치 삭제

```
(master) $ git branch -d {branch name}
```



브랜치 병합

```
(master) $ git merge feature-a

# feature-a branch로 이동 후 commit
# master branch commit
# master branch로 병합
```



Fork & Pull Model

```
# 레파지토리 포크한 후 클론 (이 때 브랜치는 메인이 되면 안됨)
$ git clone {project repository url
# 그 다음엔 Pull Request
```









## Commit 



Commit 을 통해 작업의 이력을 남기는게 중요



vs code를 이용해 commit 메시지를 쉽게 수정

```
$ git config --global core.editor "code --wait" 
$ git config --global -l
```









