---
title: "Data Structure, Dijkstra"
date: 2019-11-21 13:40:28 -0400
categories: DataStructure
tags : [DataStructure, dijkstra]
---
### Dijkstra 최단 경로 알고리즘?
- 네트워크에서 <b>하나의 시작 정점</b>으로부터 <b>모든 다른 정점까지의 최단 경로를 찾는 알고리즘</b>

---
### 알고리즘 설명
- 배열 s : 시작 정점에서 배열s에 있는 정점만을 거쳐서 다른 정점으로 가는 최단 거리를 기록하는 배열
- weight[v][w] : v에서 w로 가는 가중치 인접 행렬
- distnace[w] : 시작 정점에서 w까지의 거리 , 시작정점에서 w까지 직접 간선이 없을 경우 무한대의 값
- <b>distnace[w] = Math.min (distnace[w], distance[u] + weight[u][w])</b>
- 이때 distnace[u]는 시작정점에서 u까지의 거리이다

#### 1.
![dijkstra1](https://user-images.githubusercontent.com/55946791/69313410-ca6b7100-0c74-11ea-9078-57982329ebc1.png)

- 시작 정점은 0 이고, 직접갈수 없는 경로는 무한대, 가장 짧은 거리는 정점4 까지의 거리인 3이므로 정점4를 배열 S에 추가해준다

#### 2.
![dijkstra2](https://user-images.githubusercontent.com/55946791/69313475-fd156980-0c74-11ea-9f45-9e7bb1486a50.png)

- distnace[1] = Math.min (distance[1] , distance[4] + weight[4][1]) 이므로 distance[1]은 7에서 5로 변경된다.

#### 3.
![dijkstra4](https://user-images.githubusercontent.com/55946791/69313587-54b3d500-0c75-11ea-9bb3-506430f5bb66.png)
- 완료된 모습이다


---
### 구현

```java
package org.study;

import java.util.Scanner;

public class DijkstraTest02 {
	static int[][] ad;
    static int[] dist;
    static boolean[] visit;
    static int nE, nV;
    static final int inf = 1000000;

    public static void ssp(int start, int end){
        dist[start] = 0;    // 최초 시작 값 distance 초기화
        String s = "";
        for( int j = 0; j < nV; j++) // dist 값을 한번 초기화 했으므로 n-1번만 진행
        {
            int min = inf+1;    // dist 최소값 찾기 위한 임시 값 초기화
            int index = -1;
            for(int k = 1; k <= nV; k++){
                if(visit[k] == false && min > dist[k]){
                    min = dist[k];
                    index = k;
                }
            }
            visit[index] = true;
            s += index + " ";  // 경로를 체크하는 방법

            for(int l = 1; l <= nV; l++){
                if(ad[index][l] != 0 && dist[l] > dist[index] + ad[index][l]){ //인접 행렬을 검사하여 최적의 값을 찾아
                        dist[l] = dist[index] + ad[index][l];
                }

            }
        }

        for(int i = 1; i <= nV; i++){
            System.out.print(dist[i]);
        }
        System.out.println();
        System.out.println(s);

    }

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        nV = scan.nextInt();
        nE = scan.nextInt();

        ad = new int[nV+1][nV+1];
        dist = new int[nV+1];
        visit = new boolean[nV+1];

        for(int i = 1; i <= nV; i++){
            dist[i] = inf;   //임의의 무한한 값으로 거리값 초기화
        }

        for(int i = 0; i < nE; i++){
            int t1, t2, t3;
            t1 = scan.nextInt();
            t2 = scan.nextInt();
            t3 = scan.nextInt();

            ad[t1][t2] = t3;
        }

        ssp(1,5);
    }

}
```

---
## Reference
<https://mattlee.tistory.com/50>
