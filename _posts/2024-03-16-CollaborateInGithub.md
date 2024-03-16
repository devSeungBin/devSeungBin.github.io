---
title: Github로 협업하기
date: 2024-03-16 10:32:33 +0900
categories: [Git, github]
tags: [devops] # TAG names should always be lowercase
comments: true
author: seungbin
img_path: /assets/img/posts/Git/github/2024-03-16-CollaborateInGithub/
image:
  path: preview.jpg
  alt: 이미지 미리보기
---

# Github로 협업하기

다음은 깃허브로 프로젝트 협업을 할 때 세팅하는 방법이다. 여기서 원격 저장소는 github 레포지토리를 의미하며, 로컬 저장소는 github 레포지토리를 clone해 컴퓨터 내부에 저장된 레포지토리를 의미한다. 또 팀장의 원격 저장소는 실제 배포에 사용될 원본 저장소이다.

<br>

## 로컬 저장소 세팅 (팀원만)

1. 원본 저장소를 fork

   팀장의 원격 저장소에 접속한다.  
   fork 버튼을 눌러 자신의 원격 저장소로 fork한다.

   ```
   # fork 전
   https://github.com/kankinku/web4.0
   (팀장의 원격 저장소)

   # fork 후
   https://github.com/devSeungBin/web4.0
   (fork한 팀원 개인의 원격 저장소)
   ```

   ![fork.jpg](/fork.jpg)

2. fork한 저장소를 로컬로 clone

   fork한 원격 저장소를 자신의 로컬 저장소로 clone한다.

   ```
   # clone할 로컬 저장소로 이동
   > $ cd [path]

   # 원격 저장소를 로컬 저장소로 clone
   > $ git clone [url]
   ```

   ![clone.jpg](/clone.jpg)

3. 원격 저장소 remote 설정

   clone 후, origin이라는 이름으로 remote url이 자신의 원격 저장소로 기본으로 설정된다.  
   추후에 원본 저장소 내용과 동기화를 위해 fork를 했던 원본 저장소도 remote로 등록한다.

   ```
   # 원본 저장소 remote 등록
   > $ git remote add [별명] [원본 저장소 url]

   # 원격 저장소 확인
   > $ git remote -v
   ```

   ![remote.jpg](/remote.jpg)

<br>

## 로컬 저장소 사용법

1. branch 생성 (github flow)

   새로운 기능 개발, 버그 수정 등 프로젝트 작업 시 사용할 topic branch를 만든다.  
   topic branch의 이름은 기능을 설명하는 명확한 이름으로 네이밍한다.

   ```
   # 브랜치 생성
   > $ git branch [branch 이름]

   # 브랜치 이동
   > $ git checkout [branch 이름]

   # 브랜치 생성 후 이동 (-b 옵션)
   > $ git checkout -b [branch 이름]

   # 브랜치 리스트
   > $ git branch
   ```

   ![branch.jpg](/branch.jpg)

   > github flow 방식은 main(master) branch와 topic branch만 관리하면 되는 간단한 구조이다. 이름 그대로 github 환경에서 사용하기 적합한 branch 전략이며 웹 애플리케이션 개발 환경에서도 사용하기 적합하다.
   > {: .prompt-info }

2. 코드 작업 후 add / commit / push

   각자 코드 추가 및 수정 작업(기능 추가 혹은 버그 수정 등)이 완료되면, 개인 깃허브 원격 저장소의 topic branch에 add, commit, push하여 반영한다.

   ```
   # 추가, 수정된 파일 추적
   > $ git add .

   # 커밋 메세지 추가 후 git에 저장
   > $ git commit -m [commit 메세지]

   # github 저장소에 업로드
   > $ git push origin [branch 이름]


   /* 알아두면 좋은 명령어 */

   # 로컬 저장소 상태 확인 (커밋 상황, 추적 상황)
   > $ git status

   # 지난 commit 내용 확인
   > $ git log

   # git add 되돌리기
   > $ git rm --cached [file 이름]
   ```

   ![add_commit_push.jpg](/add_commit_push.jpg)  
   ![add_commit_push2.jpg](/add_commit_push2.jpg)

3. pull request 생성

   자신의 깃허브 원격 저장소에 접속해보면 상단에 `Compare & pull request` 버튼이 활성화된다.  
   해당 버튼을 클릭하고, PR 메세지를 작성한 뒤 `Create pull request` 버튼을 누르면 풀 리퀘스트를 생성한다.

   ![pullrequest.jpg](/pullrequest.jpg)  
   ![pullrequest2.jpg](/pullrequest2.jpg)  
   ![pullrequest3.jpg](/pullrequest3.jpg)

   > PR 내역은 원본 저장소의 pull request 메뉴에서 확인 가능하다. Conversation에서는 PR 메세지를, Commits에서는 해당 branch의 커밋 내역을, File changed에서는 파일, 코드의 수정 내역을 바로 볼 수 있다.
   > {: .prompt-info }

4. merge pull request **(팀장만)**

   pull request를 받은 팀장은 코드 변경내용을 확인하고 merge 여부를 결정한다.  
   승인을 하면 merge confirm으로 원본 저장소에 변경된 사항이 반영이 되고, pull request의 상태는 closed로 변경된다. 만일 맘에 들지 않는다 하면 Reject 된다.

   ![merge.jpg](/merge.jpg)

5. merge 이후 동기화 및 branch 삭제

   원본 저장소에 merge가 완료되면 원본 저장소의 내용이 변경된다. 따라서 자신의 원격 저장소와 로컬 저장소를 동기화하고, 더이상 작업이 필요없어진 자신의 원격 저장소의 branch를 삭제한다.

<br>

## Reference

|                                                                                                     Page                                                                                                      |  Author   |
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------: |
| [[GIT] ⚡️ 깃헙 Pull Request 보내는 방법 - 알기 쉽게 정리](https://inpa.tistory.com/entry/GIT-%E2%9A%A1%EF%B8%8F-%EA%B9%83%ED%97%99-PRPull-Request-%EB%B3%B4%EB%82%B4%EB%8A%94-%EB%B0%A9%EB%B2%95-folk-issue) |  `Inpa`   |
|                          [Github 협업하기 : PR부터 merge까지](https://velog.io/@dongvelop/Github-%ED%98%91%EC%97%85%ED%95%98%EA%B8%B0-PR%EB%B6%80%ED%84%B0-merge%EA%B9%8C%EC%A7%80)                           | `이동엽`  |
|                                                            [Git 브랜치 전략 (feat. Git Flow, Github Flow)](https://hudi.blog/git-branch-strategy/)                                                            |  `Hudi`   |
|                                                                 [git git add, git commit이란? 쓰는이유/사용법](https://hihiha2.tistory.com/4)                                                                 | `hihiha2` |
