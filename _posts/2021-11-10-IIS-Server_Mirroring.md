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


**02. 방화벽 진행 시** 
> “방화벽장비는 천차 만별이지만 통상적으로 FORTIGATE사에 있는 제품이 국가인증 및 성능이 높은 축에 속하는 편이라고 한다. 
방화벽진행시참고사항 
1. Services - 기본 방화벽 장비에서 대표적인 포트에 대한 서비스를 등록을 해둔다. 
              여기에다가 사용하고 있는 외부 솔루션에 대한 포트 및 해당 포트드를 그룹핑을 진행 할수 있다. 
2. Addresses - 아이피 대역대를 추가하거나 그룹핑을 진행 할수 있다. 
3. Policy & Object - 위 내역을 추가하고 방화벽 정책을 수립한다. 
                   - FortiGate 기준 NAME, FROM, TO, Source, Destination, Schedule, Service, Action을 설정할수 있다. 
* NAME : 그냥 명칭을 지정할수 있음
* FROM : 도착지 개념
* TO : 출발지를 말한다. 
* Source : 출발지 개념이라고 생각하면 된다. 
* Destination : 도착지 개념
* Schedule : 월,화,수.. 요일별로 방화벽 정책을 지정할수 있다.
* Service : 출발지, 도착지를 지정하고 포트를 설정할수 있다. 
* Action : ACCEPT/DENY 정보를 설정한다. 

”

**03. L4 진행 시** 
> “Layer2, Layer3, SLB 이렇게 통상적으로 참고하면 될것 같다. 
SLB에서는 Real Servers, Server Groups, Virtual Servers, Filters, Ports, Proxy IP, Layer 7 Resources, Health Checks, Global SLB, Advanced
이렇게 설정이 가능하다. 
Real Servers - 웹서버에 대한 정보를 등록한다. (IP, 이름, 상태, 최대 접속 내역등)
Server Groups - 서버에서 사용하는 포트 정보를 추가해둔다. ( 해당 포트에 대한 분기 처리 방식을 설정 할수 있다. )

L4  LOAD Balancing 방식을 ALteon에서는 SLB Metric이라고 표현하는것 같다. 
방식은 
* Least Connections - 서버의 오픈 세션수를 고려하여 가장적은 세션을 가진 서버로 분기 시키는 방식 
 - 장점 : 거의 5:5분산이 가능하다. 
 - 단점 : 경로 보장이 안된다. 

* Round Robin - 서버에 대해서 순차적으로 이동 시켜준다. 
 - 장점 : 거의 5:5분산이 가능하다. 
 - 단점 : 경로 보장이 안된다. 

* Min Misses(Minimum Missies) - Hash와 유사함 

* Respose Time - Alteon장비가 응답시간이 빠른쪽으로 많은 세션을 주고 느린쪽으로 적게 주는 방식

* Server Bandwidth

* Hash - IP기준으로 분기 하는 방식 IP를 기반으로 내부 로직으로 분기를 처리한다. 
 - 장점 : 경로가 보장된다, 메모리를 적게 사용하고 요구 절차가 간단.
 - 단점 : 세션이 5:5로 분산이 어렵다.


* Persistent Hash

* Least Connections per Service

이렇게 존재한다.


* 나머지 내역은 공부가 필요하다. 
Virtual Servers
Filters
Ports
Proxy IP
Layer 7 Resources
Health Checks
Global SLB
Advanced
”


**04. 네트워크 장비** 
> “네트워크 장비를 설치하고 아이피를 부여하면 
해당아이피로 접근시 관리하는 웹페이지 접근이 가능하다. 아이피타임 관리자 페이지 같은 개념
L4장비또한 관리 페이지가 있으나 putty로 접근시에는 telnet으로 진행하여 23 포트로접근해야 가능함 
이내역은 찾아봐야할것 같다.  ”