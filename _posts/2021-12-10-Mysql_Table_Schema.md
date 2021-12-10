---
layout: post
author: mrbang
title: 서버이중화
date: 2021-12-10T11:00:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/developer_tip.jpg"
category: Develope_Tip
summary: 명세서 쿼리    
keywords: Mysql DB 명세서 추출 쿼리 
permalink: /blog/2021-12-10-Mysql_Table_Schema/
---
# Mysql 명세서 쿼리 

개발을 진행 할때 DB명세서 작성진행시 사용할수 있는 쿼리 내역 

 `이렇게 호출하여 개발로 구성하여 엑셀다운로드로 구성하기 `
 


![Author Sidebar Widget](https://mrbang-00.github.io/assets/img/post/211110server_mirrorring.png)

**01. DB 쿼리** 

> “*DB TABLE 별 명세서 쿼리로 출력 하기”

```java

SELECT
   t1.table_name, t1.table_comment, column_name, data_type, column_type, column_key, is_nullable, column_default, extra, column_comment
FROM
   (SELECT
       table_name, table_comment
    FROM
       information_schema.TABLES WHERE table_schema='데이터베이스_이름') t1,
   (SELECT
       table_name, column_name, data_type, column_type, column_key, is_nullable, column_default, extra, column_comment, ordinal_position
    FROM
       information_schema.COLUMNS WHERE table_schema='데이터베이스_이름') t2
WHERE
    t1.table_name = t2.table_name
ORDER BY
    t1.table_name, ordinal_position;

```

**02. 엑셀 메크로만들기** 

> “*같은 값의 셀 병합하는 매크로
실행은 ALT + F8을 클릭하여 매크로를 생성 후 엑셀에서 해당매크로를 실행하여 진행”


```java

Sub SameCellMerge()
    Dim rngTarget As Range
    Dim rngCell As Range
    Dim strAddress As String
    Dim intNum As Long
    Dim intCount As Long
    Dim intTemp2 As Long
    Dim intTemp As Long
    Dim i As Integer
    Application.DisplayAlerts = False
    On Error GoTo ET
    Set rngTarget = Application.InputBox("대상 영역을 선택하세요", "영역 선택", Type:=8, Default:=strAddress)
    intNum = rngTarget.Cells.Count
  
    For Each rngCell In rngTarget
        intTemp = intTemp + 1
        intTemp2 = intNum - intTemp 
        If Len(rngCell) > 0 Then
            i = 0
            For intCount = 1 To intTemp2
                If rngCell.Offset(intCount, 0) = rngCell Then
                    i = i + 1
                Else
                    Exit For
                End If
            Next intCount
            If i > 0 Then Range(rngCell, rngCell.Offset(i, 0)).Merge
          
        End If
    Next rngCell
    rngTarget.VerticalAlignment = xlCenter
    Application.DisplayAlerts = True
    Exit Sub
ET:
    MsgBox "영역 선택이 잘못되었습니다. 영역을 다시 선택하세요!", , "에러 번호: " & Err.Number
End Sub

```