---
layout: post
author: mrbang
title: 프로그래머스_해시_완주하지_못한선수_Programmers
date: 2021-09-02T11:30:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Programmers
summary: 프로그래머스 해시 1차 문제 
keywords: 프로그래머스 programmers hash 1차 
permalink: /blog/2021-08-31-programmers_hash_1/
---
# 완주하지 못한 선수

**문제 설명** 문제 [주소](https://programmers.co.kr/learn/courses/30/lessons/42576).

> “수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.”
  

**제한사항** 

* 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
* completion의 길이는 participant의 길이보다 1 작습니다.
* 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
* 참가자 중에는 동명이인이 있을 수 있습니다.

**입출력 예** 

> “participant	completion	return
["leo", "kiki", "eden"]	["eden", "kiki"]	"leo"
["marina", "josipa", "nikola", "vinko", "filipa"]	["josipa", "filipa", "marina", "nikola"]	"vinko"
["mislav", "stanko", "mislav", "ana"]	["stanko", "ana", "mislav"]	"mislav"”

**입출력 예 설명** 

예제 #1
"leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #2
"vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #3
"mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

# 문제풀이 

**javascript** 

```javascript
function solution(participant, completion) {
    
    var answer = "";
    
    participant.sort();
    completion.sort();
    
    for(var i = 0; participant.length; i++) {        
        if(participant[i] != completion[i]) {
            
            return participant[i];        
            
        }      
    }      
    
}
```

**해설** 

> “ 문제를 확인해보면 전체인원그룹에서 완주인원그룹에 대한 내역을 제외하여 완주하지 못한 선수의 이름을 return하는 구조이다.
    그러면 일단 전체인원그룹과, 완주인원그룹에 대한 정렬을 진행을 하여 for문을 통해 전체인원갯수만큼 완주한 인원과 비교를 진행한다. 
    진행시 완주한 인원명단에 조회가 되지 않는다면 그인원에 대해서 반환을 하는 구조록 진행 하였습니다. 
    일단 해시 맵으로 진행을 해야하나 비교방식으로 1차 진행을 하였으며 이내역에 대해서는 해쉬 방법으로 변경 진행이 필요할것같다. 

    예) [absc, eds, bdes] 전체그룹을 정렬 [absc, bdes, eds] 이후 완주인원 [absc, bdes]도 정렬 후 비교를 진행 ”

**JAVA** 
```java
import java.util.Arrays;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        String result = null;               
        Arrays.sort(participant);
        Arrays.sort(completion);        
        for(int i = 0; i < completion.length; i++) {            
            if( !participant[i].equals(completion[i]) ){              
                return participant[i];                
            }             
        }                
          return participant[participant.length-1];
    }   
}
```

**해설** 

> “ 문제를 확인해보면 전체인원그룹에서 완주인원그룹에 대한 내역을 제외하여 완주하지 못한 선수의 이름을 return하는 구조이다.
    그러면 일단 전체인원그룹과, 완주인원그룹에 대한 정렬을 진행을 하여 for문을 통해 전체인원갯수만큼 완주한 인원과 비교를 진행한다. 
    진행시 완주한 인원명단에 조회가 되지 않는다면 그인원에 대해서 반환을 하는 구조록 진행 하였습니다. 
    일단 해시 맵으로 진행을 해야하나 비교방식으로 1차 진행을 하였으며 이내역에 대해서는 해쉬 방법으로 변경 진행이 필요할것같다. 

    예) [absc, eds, bdes] 전체그룹을 정렬 [absc, bdes, eds] 이후 완주인원 [absc, bdes]도 정렬 후 비교를 진행 ”
