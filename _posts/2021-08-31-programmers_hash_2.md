---
layout: post
author: mrbang
title: 프로그래머스_해시_전화번호_목록_Programmers
date: 2021-09-02T11:30:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Programmers
summary: 프로그래머스 해시 2차 문제 
keywords: 프로그래머스 programmers hash 2차 
permalink: /blog/2021-08-31-programmers_hash_2/
---
# 완주하지 못한 선수

**문제 설명** 문제 [주소](https://programmers.co.kr/learn/courses/30/lessons/42577).

> “전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

구조대 : 119
박준영 : 97 674 223
지영석 : 11 9552 4421
전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.”

**제한사항** 

* phone_book의 길이는 1 이상 1,000,000 이하입니다.
* 각 전화번호의 길이는 1 이상 20 이하입니다.
* 같은 전화번호가 중복해서 들어있지 않습니다.

**입출력 예** 

> “phone_book	return
["119", "97674223", "1195524421"]	false
["123","456","789"]	true
["12","123","1235","567","88"]	false”

**입출력 예 설명** 

입출력 예 #1
앞에서 설명한 예와 같습니다.

입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

입출력 예 #3
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.

# 문제풀이 

**JAVA** 
```java
import java.util.*;

class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        int check = 0;     
        String aaa = "";
        String bbb = "";
        
        try {
        
        for(int i = 0; i < phone_book.length; i++) {       
            
            for(int j = i+1; j < phone_book.length; j++) {   
                
                System.out.println( i + "|" + phone_book[i].toString() 
                                   + "|" + j + "|" + phone_book[j].toString() + "####" );
                
                if( (phone_book[i].toString().startsWith(phone_book[j].toString()) ) && (phone_book[i].toString() != phone_book[j].toString()) ) {
                    
                    check += 1;  
                    //return false;
                    
                } else {
                    
                    //break;
                    
                } 
                 
            }
      
        }
            
        } catch(IndexOutOfBoundsException e) {

			System.out.println(e);

		}
            
        if(check > 0) answer = false; 
        if(check == 0) answer = true; 
        
        return answer;
        
    }
}
```

**해설** 

> “”
