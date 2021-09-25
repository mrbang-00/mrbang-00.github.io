---
layout: post
author: mrbang
title: MYSQL_Linux에서 Mysql설치
date: 2021-09-23T00:30:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Programmers
summary: Linux에서 Mysql설치
keywords: Linux, Mysql설치
permalink: /blog/2021-09-25-mysql_linux_install/
---
# Linux에서 Mysql설치

**진행 내역** 

`실시간 체크를 위한 DB신규 생성을 위한 여분 서버(Linux)에 Mysql 설치하기 `
`목적 : 웹서버에 대량의 접속이 발생시 1개의 DB에서 커넥션 수가 다수 발생하여 다수 호출되는 데이터는 여분의 서버에서 사용하기 위함`


**절차** 

1. 해당 명령어를 통해 리눅스 서버의 정보를 조회한다. 
> “
`grep . /etc/*-release`
/etc/lsb-release:DISTRIB_ID=Ubuntu
/etc/lsb-release:DISTRIB_RELEASE=14.04
/etc/lsb-release:DISTRIB_CODENAME=trusty
/etc/lsb-release:DISTRIB_DESCRIPTION="Ubuntu 14.04.3 LTS"
/etc/os-release:NAME="Ubuntu"
/etc/os-release:VERSION="14.04.3 LTS, Trusty Tahr"
/etc/os-release:ID=ubuntu
/etc/os-release:ID_LIKE=debian
/etc/os-release:PRETTY_NAME="Ubuntu 14.04.3 LTS"
/etc/os-release:VERSION_ID="14.04"
/etc/os-release:HOME_URL="http://www.ubuntu.com/"
/etc/os-release:SUPPORT_URL="http://help.ubuntu.com/"
/etc/os-release:BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
”
대략 이렇게 조회가 된다. 

> “
기존 서버 : /etc/centos-release:CentOS Linux release 7.1.1503 (Core)
신규 서버 : /etc/centos-release:CentOS Linux release 7.2.1511 (Core)
”

2. 기존 Mysql 버전 확인 

> “
SELECT VERSION();
5.7.13
”
해당 명령어를 통해 Mysql 버전을 확인한다. 

3. 설치 과정

> “
* wget 설치
$ yum install wget
”

> “
* MySQL 다운로드
$ wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
”

> “
* MySQL 설치
$ sudo rpm -ivh mysql57-community-release-el7-11.noarch.rpm
”

> “
* MySQL 서버 설치
$ sudo yum install mysql-server
”

> “
* 서비스 시작
$ sudo systemctl start mysqld
MySQL은 루트 로그인이나 샘플 유저와 같이 보안 수준이 낮은 기본 옵션을 변경해주는 보안 스크립트가 포함 되어있다.
”

> “
* 보안 스크립트 실행
$ sudo mysql_secure_installation

기본 루트 암호를 묻는 메시지에서는 새로운 비밀번호를 입력하라고 나온다. 

`The existing password for the user account root has expired. Please set a new password. New password:`

Mysql 5.7 버전이상에서는 비밀번호 설정 강도가 강화되어 규칙이 변경되었다. 
대문자, 숫자, 특수문자가 포함된 12자리를 지정하라고 한다. 
”

4. Mysql 관리 

> “

> “
* wget 설치
$ yum install wget
”

> “
* Mysql 정지
$ systemctl stop mysqld
”

> “
* Mysql 환경 옵션 설정
$ systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"
해당 명령어를 통해 mysql safe설정 변경 
이유 : 기존에는 mysql safe를 사용하지만 5.7이상부터는 systemd에서 관리를 한다고 한다. 
”

> “
* Mysql 시작
$ systemctl start mysqld
”

> “
* Mysql 로그인
$ mysql -u root
root로 접속이 가능하다. 
”

> “
* 루트 비밀번호 변경
mysql> UPDATE mysql.user SET authentication_string = PASSWORD('새로운 비밀번호') -> WHERE User = 'root' AND Host = 'localhost'; mysql> FLUSH PRIVILEGES; mysql> exit
”

> “
* Mysql 정지
$ systemctl stop mysqld
”

> “
* Mysql 환경 옵션 설정 해제 
$ systemctl unset-environment MYSQLD_OPTS
- 환경 옵션 설정 해제 명령어 
”

> “
* Mysql 시작
$ systemctl start mysqld
”

> “
* Mysql 로그인
$ mysql -u root -p
”

> “
* Mysql사용자 추가
mysql> create user '사용자'@'localhost' identified by '비밀번호';
”

> “
* 권한 부여
mysql> grant all privileges on *.* to '사용자'@'%';
”

> “
* 외부 접속 허용
$ vi /etc/my.cnf bind-address 0.0.0.0 # 
mysql 워크벤치나 외부접속 툴에서 접속이 가능하기 위해서는 위 명령어를 설정해주어야 한다.
”

”
