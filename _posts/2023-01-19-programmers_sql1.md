---
layout: post
author: mrbang
title: Programmers Mysql 
date: 2023-01-19T11:00:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Develope_Tip
summary: Programmers 조건에 맞는 도서 리스트 출력하기
keywords: Mysql DB Programmers 조건에 맞는 도서 리스트 출력하기
permalink: /blog/2023-01-19-programmers_sql1/
---
# [SQL 고득점 Kit]조건에 맞는 도서 리스트 출력하기

**문제 설명** 문제 [주소](https://school.programmers.co.kr/learn/courses/30/lessons/144853?language=mysql).

> “다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(BOOK) 테이블입니다.
BOOK 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.


Column name    / Type        / Nullable / Description
BOOK_ID        / INTEGER     / 도서     / ID
CATEGORY	   / VARCHAR(N)  / FALSE    / 카테고리 (경제, 인문, 소설, 생활, 기술)
AUTHOR_ID      / INTEGER     / FALSE    / 저자 ID
PRICE          / INTEGER     / FALSE    / 판매가 (원)
PUBLISHED_DATE / DATE        / FALSE    / 출판일

”


**문제** 

> “BOOK 테이블에서 2021년에 출판된 '인문' 카테고리에 속하는 도서 리스트를 찾아서 도서 ID(BOOK_ID), 출판일 (PUBLISHED_DATE)을 출력하는 SQL문을 작성해주세요.
결과는 출판일을 기준으로 오름차순 정렬해주세요.”


**예시** 

> “예를 들어 BOOK 테이블이 다음과 같다면”

BOOK_ID / CATEGORY / AUTHOR_ID / PRICE / PUBLISHED_DATE
1       / 인문      / 1        / 10000  / 2020-01-01
2       / 경제      / 2        / 9000   / 2021-02-05
3       / 인문      / 2        / 11000  / 2021-04-11
4       / 인문      / 3        / 10000  / 2021-03-15
5       / 생활      / 1        / 12000  / 2021-01-10

조건에 속하는 도서는 도서 ID 가 3, 4인 도서이므로 다음과 같습니다.

BOOK_ID / PUBLISHED_DATE
3       / 2021-04-11
4       / 2021-03-15

그리고 출판일 오름차순으로 정렬하여야 하므로 다음과 같은 결과가 나와야 합니다.

BOOK_ID / PUBLISHED_DATE
4       / 2021-03-15
3       / 2021-04-11

# 문제풀이 

**MYSQL** 
```java

SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE,'%Y-%m-%d')  as PUBLISHED_DATE 
from book 
where category = '인문' 
and PUBLISHED_DATE between '2021-01-01' and '2021-12-31'
order by PUBLISHED_DATE asc

* 풀이 : 인문으로 검색을 진행 후 출판일 기준으로 조회 된 값을 출판일 기준으로 오름차순 정렬을 
진행하고 출력되는 출판일 날짜 포맷을  yyyy-MM-dd 형식으로 변경하여 출력

* 참고 : sql 조건 검색 중 점조건과 선분 조건이 있다. 
점 조건 : IN, = 연산자를 이용한 조건이며 해당 연사자는 하나의 점만을 의미함 
선분 조건 : Like, Between, <, > 등과 같이 점 조건을 제외한 연산자를 사용한 조건을 의미한다. 
선분 조건은 하나의 점만을 의미하는 것이 아니라 해당 조건을 만족하는 모든 실수를 의미 

-> sql조건문은 점조건을 먼저 사용하고 선분 조건을 사용해야 기본적인 SQL문속도가 빠르다. 
꼭 참고하자!!! (INDEX걸기 전에 기본적으로 점조건, 선분조건 순서부터 확인하자!!!!)

* 결론 : 조건절이 명확하면 =을 이용하자 범위 검색을 할때는 <> 부등호 보다 Between이 속도가 더빠르기 때문에 between을 사용하길 권장한다. 

* 참고 2 :  아래 구문은 동일하다. between은 <= 이내역과 동일하니 검색조건 진행시 참고하자.!!!!
and PUBLISHED_DATE between '2021-01-01' and '2021-12-31'
and PUBLISHED_DATE < '2022-01-01' and PUBLISHED_DATE > '2020-12-31' 

```

**해설** 

> “SQL별 DataFormat에 대한 숙지가 필요할것 같다.”
