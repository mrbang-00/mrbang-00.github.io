---
layout: post
author: mrbang
title: 서버이중화
date: 2021-11-10T11:00:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/developer_tip.jpg"
category: Develope_Tip
summary: 서버이중화   
keywords: IIS 서버이중화 망분리
permalink: /blog/2021-11-10-IIS-Server_Mirroring/
---
# 서버이중화를 진행 할때 기본 적인 구성 상태 및 참고 자료 

서버이중화시 참고사항

 `망분리 진행 `
 `방화벽 정책 설정 방안 `


![Author Sidebar Widget](https://mrbang-00.github.io/assets/img/post/211110server_mirrorring.png)

**00. 용어정리** 

* DMZ(Demilitarized Zone) 구간
> “외부영역에 서비스를 제공할때 내부 자원을 
보호하기 위해 내부망, 외부망 사이에서 접근 제어를 하는 방식이다. 
내부 자원에 대한 접근을 불가하기 위한 방법”


**00. 외부방화벽정책** 

> “*외부방화벽 정책
외부방화벽은 외부 솔루션 기준 포트 및 IP기준으로 설정을 진행 하도록 구성한다. ”

**01. 내부방화벽정책** 

> “*내부방화벽 정책
내부방화벽은 웹서버1,2번으로 접근하는 내역에 대해서만 허가한다.
(Ex. Oracle(1521, 1522), Mysql(3306), Ms-sql(1433,1434)
(Ex. 백업포트 21,20022 파일(139,3389,445,UDP137,138) SSH(10022) 등)
(Ex. 아이피는 웹서버1,2로 접근시에만 가능하도록 구성하기 
* 해당 내부망 서버 접근에 대해서도 방화벽 정책을 지정하여 관리하는 방식으로 진행 한다. ”

