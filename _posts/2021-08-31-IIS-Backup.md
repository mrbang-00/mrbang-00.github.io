---
layout: post
author: mrbang
title: IIS 백업 정책 설정하기 ( Bat파일을 통한 소스압축 )
date: 2021-08-28T16:00:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/hello.jpg"
category: gitblog
summary: IIS에서 백업정책 만들기   
keywords: IIS BACKUP 백업정책 
permalink: /blog/2021-08-31-IIS-Backup/
---
# IIS기준 스케줄러 실행 후에 bat파일 호출을 통해서 스케줄러 작업을 위한 내역 

소스백업시 고려해야할 사항 

 `서버의 용량을 체크한다. `
 `백업 기준을 잡는다. 로컬에서 몇일, 배업할 대상의 서버에서는 몇일 동안진행할지 `

Bat파일을 통한 기존 소스내역을 다른내역으로 이관후 압축하는 BAT실행파일

**00. BAT 실행시 다른 bat 파일 호출 진행** 

> “call 1_eng_SeverCopy.bat
timeout /t 10
call 2_eng_doZip.bat
timeout /t 10
call 3_eng_delFolder.bat
timeout /t 10
call 4_eng_delZipFile.bat”

**01. 기존소스 백업 진행 ( 일자별 파일 생성을 진행 해서 진행 )** 

> “mkdir D:\BACKUP_SCHEDULE\TEST\01_bacfile_day\%DATE%
robocopy D:\WebHosting\TEST D:\BACKUP_SCHEDULE\TEST\01_bacfile_day\%DATE% /S >D:\BACKUP_SCHEDULE\TEST\03_log\1_copy-%DATE%.txt ”


**02. 파일 복사 진행 후 파일 압축 진행** 

> “zip -9vr D:\BACKUP_SCHEDULE\TEST\01_bacfile_day\%DATE%.zip D:\BACKUP_SCHEDULE\TEST\01_bacfile_day\%DATE% > D:\BACKUP_SCHEDULE\TEST\03_log\2_zip-%DATE%.txt”


**03. 압축 이후 복사 된 파일 삭제 진행** 

> “rmdir /s /q D:\BACKUP_SCHEDULE\TEST\01_bacfile_day\%DATE%\ > D:\BACKUP_SCHEDULE\TEST\03_log\3_rmdir-%DATE%.txt”


**04. 복사 된 파일에 대한 특정일자 이후 삭제 로직 진행** 

> “forfiles /p "D:\BACKUP_SCHEDULE\TEST\01_bacfile_day" /s /m *.zip /d -7 /c "cmd /c del @path" > D:\BACKUP_SCHEDULE\TEST\03_log\4_delZipFile-%DATE%.txt”

