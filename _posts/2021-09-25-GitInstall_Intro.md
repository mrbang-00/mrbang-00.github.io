---
layout: post
author: mrbang
title: 윈도우에서 git사용하기 
date: 2021-09-25T17:30:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/developer_tip.jpg"
category: Develope_Tip
summary: 윈도우에서 git사용하기 
keywords: Git설치 VisualStudioCode
permalink: /blog/2021-09-25-GitInstall_Intro/
---
# Linux에서 Mysql설치

**내역** 

`윈도우에서 Visual Studio Code를 통해서 Git Blog 사용하기`

**방법** 

* 1.Git설치하기 [주소](https://www.git-scm.com/).

>
1. `Git 설치하기`
Git공식홈페이지에서 Window 버전다운로드 
2. 설치 진행 후 설정 변경
-> Visual Studio Code에서 사용하기 위함 - Use Visual Studio code as Git's default editor선택 (Visual Studio code에서 사용하기 위함)

>
1. `Git Bash실행 및 설정 `
해당 컴퓨터에서 Git을 사용하기 위한 설정을 진행 한다. (Git Bash 실행)
2. 명령어 
- 사용자명 지정 : $ git conifg --global user .name "사용자명"
- 이메일 지정 : $ git conifg --global user .email "이메일주소@이메일주소"
- 설정내역 확인 : $ git conifg --list

>
1. `VSCode에서 설정 `
F1 -> git:Clone -> git 주소 가져와서 입력 후 해당 컴퓨터 저장위치선택 
2. 로그인 하라고 하면 브라우저가 실행이 되고 로그인 하면 자동 인증 된다. 



