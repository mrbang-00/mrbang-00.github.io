---
layout: post
author: mrbang
title: Programmers Mysql AVG PAY 
date: 2023-01-19T11:00:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Develope_Tip
summary: Programmers 평균 일일 대여 요금 구하기    
keywords: Mysql DB Programmers 평균 일일 대여 요금 구하기 
permalink: /blog/2023-01-19-programmers_mysql/
---
# [SQL 고득점 Kit]평균 일일 대여 요금 구하기

**문제 설명** 문제 [주소](https://school.programmers.co.kr/learn/courses/30/lessons/151136?language=mysql).

> “다음은 어느 자동차 대여 회사에서 대여중인 자동차들의 정보를 담은 CAR_RENTAL_COMPANY_CAR 테이블입니다. CAR_RENTAL_COMPANY_CAR 테이블은 아래와 같은 구조로 되어있으며, CAR_ID, CAR_TYPE, DAILY_FEE, OPTIONS 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.


Column name / Type         / Nullable
CAR_ID      / INTEGER      / FALSE
CAR_TYPE    / VARCHAR(255) / FALSE
DAILY_FEE   / INTEGER      / FALSE
OPTIONS     / VARCHAR(255) / FALSE


자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.
”


**문제** 

> “*CAR_RENTAL_COMPANY_CAR 테이블에서 자동차 종류가 'SUV'인 자동차들의 평균 일일 대여 요금을 출력하는 SQL문을 작성해주세요. 이때 평균 일일 대여 요금은 소수 첫 번째 자리에서 반올림하고, 컬럼명은 AVERAGE_FEE 로 지정해주세요.”


**예시** 

> “*CAR_RENTAL_COMPANY_CAR 테이블에서 자동차 종류가 'SUV'인 자동차들의 평균 일일 대여 요금을 출력하는 SQL문을 작성해주세요. 이때 평균 일일 대여 요금은 소수 첫 번째 자리에서 반올림하고, 컬럼명은 AVERAGE_FEE 로 지정해주세요.”

CAR_ID / CAR_TYPE  / DAILY_FEE  / OPTIONS
1      / 세단      / 16000      / 가죽시트,열선시트,후방카메라
2      / SUV       / 14000      / 스마트키,네비게이션,열선시트
3      / SUV       / 22000      / 주차감지센서,후방카메라,가죽시트

'SUV' 에 해당하는 자동차들의 평균 일일 대여 요금은 18,000 원 이므로, 다음과 같은 결과가 나와야 합니다.


AVERAGE_FEE
18000




# 문제풀이 

**MYSQL** 
```java

* 첫번째 풀이 
SELECT round(sum(daily_fee)/count(daily_fee))  as AVERAGE_FEE from CAR_RENTAL_COMPANY_CAR WHERE CAR_TYPE = 'suv'  group by car_type 

-> 일단 조건절에 SUV로 검색을 진행 하고 하루 이용료를 전체 합산을 하고 전체 갯수를 구해 그값으로 나누고 나서 round함수를 통해 반올림 처리를 진행하고 alias를 줘서 값을 추출하였다. 

* 함수를 찾아서 만든 풀이 

SELECT ROUND(AVG(DAILY_FEE), 0) AS AVERAGE_FEE FROM CAR_RENTAL_COMPANY_CAR 
 WHERE CAR_TYPE LIKE '%SUV%';

일단 LIKE를 통해 suv로 조건을 주고 그 이후 하루 이용료에 대한 AVG함수를 통해 평균값을 구한뒤 
round함수를 통해서 소수점 자리를 미출력 하였다. 

* 참고 : 일단 AVG함수를 통해서 값을 구하면 반올림이 되어서 구해진다. 

```

**해설** 

> “
기본적인 사칙연산을 통해서 쿼리를 작성할수 있으나 각 sql들이 제공하는 함수를 사용하는것도 
속도면이나 가독성 측면에서 권장되기 때문에 함수에 대한 숙지가 필요할것 같다. 
”
