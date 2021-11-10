---
layout: post
author: mrbang
title: 프로그래머스_정렬_K번째수_Programmers
date: 2021-09-23T00:30:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Programmers
summary: 프로그래머스 정렬 1차 문제 
keywords: 프로그래머스 programmers 정렬 1차 
permalink: /blog/2021-11-10-programmers_array_1/
---
# 더 맵게

**문제 설명** 문제 [주소](https://programmers.co.kr/learn/courses/30/lessons/42748?language=java).

> “배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.
예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면
1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.”

> “배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.”

**제한 사항** 

* array의 길이는 1 이상 100 이하입니다.
* array의 각 원소는 1 이상 100 이하입니다.
* commands의 길이는 1 이상 50 이하입니다.
* commands의 각 원소는 길이가 3입니다.

**입출력 예** 

> “array	            commands	                        return
[1, 5, 2, 6, 3, 7, 4]	[[2, 5, 3], [4, 4, 1], [1, 7, 3]]	[5, 6, 3]”

**입출력 예 설명** 

[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

# 문제풀이 

**JAVA** 
```java

// 문제 설명 
// 특정 값이 담겨있는 배열A가 있고 
// A값을 가공할수 있는 조건이 있는 배열B가 있을때 그 규칙에 맞게 리턴되는 값을 배열에 담아서 리턴하는 문제이다. 
// B배열의 규칙은 [가,나,다] 이렇게 존재 할때 A배열에서 '가'에서 '나'까지의 값을 구한뒤 '다'번째 값을 배열에 담아서 리턴하는 문제이다. 
import java.util.*;                 // 자바 형변환을 위해서 인위적으로 * 으로 선언
import java.util.Arrays;            // 배열을 사용하기 위해서 arrays를 추가하였으나 형변환을 위해서 *을 선언하였는데 형변환만 진행되는 IMPORT내역 찾아보기 

class Solution {                    // Solution이라는 클래스를 만듭니다. 

    public int[] solution(int[] array, int[][] commands) {      // 정수형 solution은 2개의 매개변수를 받는데 정수형배열 array, 정수형2차원 배열 commands를 받는다. 
        
        int[] answer = {};                                      // 정수형 배열 answer을 선언한다. 
        answer = new int[commands.length];                      // 정수형 배열에 대한 크기 선언을 한다.   (크기를 지정하지 않으면 배열에 값을 못넣는다.)
        
     try {

         for(int i =0; i < commands.length; i++ ){              // for 문을 시작하는데 B배열에 대한 길이만큼 진행한다. 문제예시는 3개가 있으므로 3개까지 진행 된다. 
        
             int[] arr_answer = Arrays.copyOfRange(array, (commands[i][0])-1 , commands[i][1] );        // Arrays.copyOfRange 함수를 이용하여 B조건에 해당되는 값을 구한다. 
                                                                                                        // Arrays.copyOfRange는 (배열, 시작, 종료) 이렇게 하면 배열에서 시작열에서 종료열에 대한 값을 선택하여 값을 리턴하게 된다.  B배열 2,5,3 이렇게 있으면 배열에서 2번째에서 5번째 까지 값을 리턴하게 되는데 배열은 0부터 시작하게 되니 [1, 5, 2, 6, 3, 7, 4]에서 2,6,3이 리턴이 된다. 2,5로 해당 함수를 실행하면 2,6,3으로 리턴이 된다. 그러므로 시작값에서 -1을 진행하며 2번째부터 시작한다는것을 명시해 주었다. 
             
             Arrays.sort(arr_answer);                                                                   // Arrays.sort를 통해서 오름차순 정렬을 진행
             System.out.println("[i]>>>>" + i);
             
             int last_val = (commands[i][2]);                                                           // B배열의 3번째 값을 담아둔다.                
             
             System.out.println("[arr_answer[last_val-1]]>>>>" + arr_answer[last_val-1]);
             answer[i] = arr_answer[last_val-1];                                                        // 구한 값을 담을 answer배열에 i번째에 해당값을 추가해둔다. 
                
         }


         
         System.out.println("[answer.length]" + answer.length);
         
    } catch(Exception e){
    
    
    }          
        
        return answer;

    }

}

```

**해설** 

> “array함수에 대한 공부가 필요한 부분이였다. 문제는 따로 힘는건 없었는데 Arrays.copyOfRange에 대한 습관화가 필요할 것같다.”
