---
layout: post
title:  "Git rebase, merge, stash"
excerpt: "Git rebase, merge, stash"
category: git
tags: [git]
date: '2024-09-04 19:30:00 +09:00'
last_modified_at: '2024-09-04'
---

# Git rebase, merge, stash 설명

## merge VS rebase

두 명령어 모두 브랜치 간의 변경사항을 통합하는 데 사용하나 사용 방식, 결과가 다름<br>

**💫 merge**<br>

- 두 브랜치를 합칠 때, 두 브랜치의 공통 조상과 각 브랜치의 최신 커밋을 사용하여 새로운 커밋을 생성<br>

```bash
$ git checkout main
$ git merge feature-branch
```
이렇게 하면 feature-branch의 모든 변경사항이 main 브랜치에 통합.<br>
장점 : 원래의 브랜치 히스토리 유지.<br>
단점 : 복잡한 브랜치 히스토리 생성가능.<br>
<br>

**💫 rebase**<br>

- rebase는 현재 브랜치의 커밋을 임시로 저장하고, 대상 브랜치의 커밋으로 현재 브랜치를 업데이트한 후, 임시로 저장한 커밋을 다시 적용<br>

```bash
$ git checkout feature-branch
$ git rebase main
```
장점 : 선형적인 커밋 히스토리를 생성.<br>
단점 : 과거의 커밋 히스토리를 변경, 협업 중인 경우 다른 사용자와 충돌이 발생가능<br>
<br>

## stash

**💫 stash : 변경사항 임시 저장 및 복구**<br>

- 현재의 작업을 임시로 저장하고, 나중에 다시 불러와 계속 진행할 수 있게 해주는 기능<br>
<br>

임시 저장<br>
```bash
$ git stash save "임시 저장 메시지"
```
<br>

임시 저장 목록 보기<br>
```bash
$ git stash list
```
<br>

임시 저장된 변경사항 복구하기<br>
```bash
$ git stash apply stash@{0}   # 가장 최근의 stash 적용
```
<br>

임시 저장된 변경사항 제거하기<br>
```bash
$ git stash drop stash@{0}
```
<br>

✔ git stash pop은 apply와 drop을 동시에 수행<br>