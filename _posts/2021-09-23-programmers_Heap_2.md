---
layout: post
author: mrbang
title: 프로그래머스_힙_디스크_컨트롤러_Programmers
date: 2021-09-23T00:30:00.613Z
# thumbnail: /assets/img/posts/hello.jpg
thumbnail: /assets/img/posts/Programmers.jpg"
category: Programmers
summary: 프로그래머스 Heap 2차 문제 
keywords: 프로그래머스 programmers Heap 2차 
permalink: /blog/2021-09-23-programmers_Heap_2/
---
# 디스크 컨트롤러

**문제 설명** 문제 [주소](https://programmers.co.kr/learn/courses/30/lessons/42627?language=java).

> “하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.
”
**예를들어** 
> “
- 0ms 시점에 3ms가 소요되는 A작업 요청
- 1ms 시점에 9ms가 소요되는 B작업 요청
- 2ms 시점에 6ms가 소요되는 C작업 요청
”
와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다.
한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.
**이미지**
> “
- A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
- B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
- C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)
”

이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.
하지만 A → C → B 순서대로 처리하면
**이미지**

이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)

**제한 사항** 

* jobs의 길이는 1 이상 500 이하입니다.
* jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
* 각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
* 각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
* 하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.

**입출력 예** 

> “jobs	return
[[0, 3], [1, 9], [2, 6]]	9”

**입출력 예 설명** 

문제에 주어진 예와 같습니다.

* 0ms 시점에 3ms 걸리는 작업 요청이 들어옵니다.
* 1ms 시점에 9ms 걸리는 작업 요청이 들어옵니다.
* 2ms 시점에 6ms 걸리는 작업 요청이 들어옵니다.

# 문제풀이 

**JAVA** 
```java
// 문제 설명 
// 하드디스크는 한번에 하나의 작업 수행만 가능하다. 
// 각 작업별 소요시간에 대한 평균을 구하는 문제로서 요청시간에서 작업 완료시간의 총 소요시간에
// 대한 평균 값을 구하는 문제이다. 
// 설명 편의를 위해 3ms에서 ms를 초로 설명을 하겠습니다. 
// 예제를 보면 A라는 작업은 0초에 작업요청이 들어왔으며 3초의 작업소요시간이 걸리게 됩니다. 
// 총 소요시간은 3초에 소요시간이 발생을 하게되며 
// B라는 작업은 9초가 걸리고 1초에 요청이 들어왔지만 A라는 작업이 끝나고 나서 시작을 해야하므로 
// 3초이후 시작하여 소요시간 9초 이후에 완료가 되므로 12초에 종료가 됩니다. 
// 여기서 문제는 요청시간과 작업완료시간에 대한 소요시간을 구하는 내역이므로 
// B작업은 1초에요청이되어 12초에 완료가 되었으므로 11초가 걸렸습니다. 
// A는 3초 B는 11초 C는 17초 
// C작업은 2초에 요청이 들어왔으나 B작업이후 6초가 걸려 완료가되었으니 총 17초가 걸리게 됩니다. 
// 3개의 작업소요시간에 대한 평균을 구하는 내역이므로 (3초 + 11초 + 17초)나누기 3개의 작업을 
// 하게 되면 평균 10초가 걸리는 작업시간을 리턴을 해주면 됩니다. 

// 하지만 A작업 이후 C작업을 하고 B작업을 한다면 3초 7초 17초 /3 = 9초의 평균 소요시간이 
// 리턴됩니다. 

// 이처럼 작업의 평균 소요 시간이 제일 작은 시간을 구하게 되는 문제입니다. 

// 주어진 2차원 배열 [[0, 3], [1, 9], [2, 6]] 
// 2차원 배열의 
import java.util.*;

class Node implements Comparable<Node>{
    int start;
    int cost;
    public Node(int start, int cost) {
        
        this.start = start;
        this.cost = cost;
        
    }
   
    @Override
    public int compareTo(Node n) {
        
        if(n.cost != cost)
            if(n.cost < cost)
                return 1;
            else
                return -1;
        else
            if(n.start < start)
                return 1;
            else
                return -1;
    }
}


class Solution {   
    
    public int solution(int[][] jobs) {
        int answer = 0;
        ArrayList<Node> list = new ArrayList<>();
        for(int i = 0; i < jobs.length; i++)
        {
            list.add(new Node(jobs[i][0],jobs[i][1]));
        }
        
        Collections.sort(list);
        int time = 0;
        
       
        
        while(list.size() > 0)
        {
            for(int i = 0; i < list.size(); i++)
            {
                if(time >= list.get(i).start)
                {
                    time += list.get(i).cost;
                    answer += time - list.get(i).start;
                    list.remove(i);
                    break;
                }
                
                if(i == list.size() - 1)
                {
                    time++;
                }
            }
        }
        
        return answer/jobs.length;
     }
}

```

**해설** 

> “
아직 이해가 되지 않는다. .....
”
