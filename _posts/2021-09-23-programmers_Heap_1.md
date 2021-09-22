---
layout: post
author: mrbang
title: 프로그래머스_힙_더맵게_Programmers
date: 2021-09-23T00:30:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Programmers
summary: 프로그래머스 Heap 1차 문제 
keywords: 프로그래머스 programmers Heap 1차 
permalink: /blog/2021-09-23-programmers_Heap_1/
---
# 더 맵게

**문제 설명** 문제 [주소](https://programmers.co.kr/learn/courses/30/lessons/42626).

> “매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.”

> “섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)”

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

**제한 사항** 

* scoville의 길이는 2 이상 1,000,000 이하입니다.
* K는 0 이상 1,000,000,000 이하입니다.
* scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
* 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

**입출력 예** 

> “scoville       	    K	return
[1, 2, 3, 9, 10, 12]	7	2”

**입출력 예 설명** 

1. 스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]

2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
가진 음식의 스코빌 지수 = [13, 9, 10, 12]

* 모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.

# 문제풀이 

**JAVA** 
```java
// 스코빌 지수가 표시된 음식이 명시된 스코빌 지수보다 클때까지 명시된 공식을 통해서 실행을 하였을때 
// 최소 진행 되어야 하는 작업 수를 리턴하여야 하는 문제 
import java.util.PriorityQueue; //import
//1. 높은 우선순위의 요소를 먼저 꺼내서 처리하는 구조 (큐에 들어가는 원소는 비교가 가능한 기준이 있어야함) 
//2. 내부 요소는 힙으로 구성되어 이진트리 구조로 이루어져 있음   
//3. 내부구조가 힙으로 구성되어 있기에 시간 복잡도는 O(NLogN)
//4. 응급실과 같이 우선순위를 중요시해야 하는 상황에서 쓰임
//가.int형 priorityQueue 선언 (우선순위가 낮은 숫자 순)
//가.PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();
//나.int형 priorityQueue 선언 (우선순위가 높은 숫자 순)
//나.PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());
//다.String형 priorityQueue 선언 (우선순위가 낮은 숫자 순)
//다.PriorityQueue<String> priorityQueue = new PriorityQueue<>(); 
//라.String형 priorityQueue 선언 (우선순위가 높은 숫자 순)
//라.PriorityQueue<String> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());

class Solution {
    
    public int solution(int[] scoville, int K) {
        
        
        int result = 0;         // 리턴될 변수 선언
        
try{
    //가.int형 priorityQueue 선언 (우선순위가 낮은 숫자 순) 예제로 섞여 있다면 1,2,3 이런순으로 정렬을 한다고 생각하면 된다. 
    PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();
        
    // 우선순위가 낮은 순으로 priorityQueue에서 제공하는 offer라는 함수를 통해서 큐에 데이터를 넣어둔다. 
        for(int i = 0 ; i< scoville.length; i++) {            
            priorityQueue.offer(scoville[i]);            
        }
        //queue.offer(data); queue에 데이터를 집어 넣습니다.
        //queue.poll(); //queue에 있는 맨 앞에 있는 데이터를 뽑습니다.
        //queue.peek(); //queue의 맨 앞의 데이터를 확인합니다.

        //priorityQueue.poll();       // priorityQueue에 첫번째 값을 반환하고 제거 비어있다면 null
        //priorityQueue.remove();     // priorityQueue에 첫번째 값 제거
        //priorityQueue.clear();      // priorityQueue에 초기화
        //queue.offer(data); queue에 데이터를 집어 넣습니다.
        //queue.poll(); //queue에 가장 작은 데이터를 뽑습니다.
        //queue.peek(); //queue의 가장 작은 데이터를 확인합니다.

    // 큐에 들어가있는 데이터중 peek함수를 통해서 명시된 스코빌 지수가 작거나 같다면 실행을 한다. 
     while (priorityQueue.peek() <= K) {
         
         // 큐에서 제일 peek함수를 통해서 가장작은 데이터를 확인하게 되지만 1개가 남았다고 가정을 하면 
         // 제한사항에서 명시된 것처럼 -1을 리턴하도록 유효성을 진행 한다. 
            if (priorityQueue.size() == 1) {
                return -1;
            }
         
            // poll함수를 통해서 가장 작은 데이터를 뽑는다. 
            int a = priorityQueue.poll();
            int b = priorityQueue.poll();
            // while이 실행이 된거는 명시된 스코프 지수보다 낮다고 조회되었기때문에 
            // 조건식을 시행한다. 
            int shake_Scoville = a + (b * 2);
            
            //offer함수를 통해 우선순위 큐에 섞은 스코빌 지수 데이터를 넣는다. 
            priorityQueue.offer(shake_Scoville);
            // 명시된 공식을 사용하여 섞었기 때문에 리턴값을 +1해준다. 
            result ++;
        }
    
    System.out.println("[리턴되는 값 ]>>>>" + result);
    
} catch(Exception e){
    
    System.out.println("[Errors발생]>>>>");
    
}
        
    return result;   
    
    }
    
}

```

**해설** 

> “
priorityQueue 우선순위가 낮은 큐로 데이터를 담아서 
1번째 2번째를 가져와 스코빌 지수와 비교를 진행하고 낮다면 공식을 계속 호출하도록 구성하였다. 
그리고 길이가 1일때 스코빌 지수에 못 미친다면 -1을 리턴하도록 구성하였다. 
priorityQueue에 대한 우선순위별 선언을 하는것에 대한 여러가지로 써먹을 수있을것 같다. 
”
