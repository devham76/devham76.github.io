---
title: "Data Structure, Dijkstra"
date: 2020-03-10 13:40:28 -0400
categories: DataStructure
tags : [DataStructure, dijkstra]
---

## Dijkstra 최단 경로 알고리즘

```
하나의 시작 정점으로부터 다른 모든 정점까지의 최단 경로를 찾는 알고리즘
```

> 참고) MST(최소 신장트리)

```
모든 정점들을 가장 적은 수의 간선과 비용으로 연결 한 것이며 종류는 Kruskal, Prim이 있다
```

## 알고리즘 설명
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



## 구현

```java
class Graph{
    private int n;           //노드들의 수
    private int maps[][];    //노드들간의 가중치 저장할 변수

    public Graph(int n){
        this.n = n;
        maps = new int[n+1][n+1];

    }
    public void input(int i,int j,int w){
        maps[i][j] = w;
        maps[j][i] = w;
    }

    public void dijkstra(int v){
        int distance[] = new int[n+1];          //최단 거리를 저장할 변수
        boolean[] check = new boolean[n+1];     //해당 노드를 방문했는지 체크할 변수

        //distance값 초기화.
        for(int i=1;i<n+1;i++){
            distance[i] = Integer.MAX_VALUE;
        }

        //시작노드값 초기화.
        distance[v] =0;
        check[v] =true;

        //연결노드 distance갱신
        for(int i=1;i<n+1;i++){
            if(!check[i] && maps[v][i] !=0){
                distance[i] = maps[v][i];
            }
        }


        for(int a=0;a<n-1;a++){
            //원래는 모든 노드가 true될때까지 인데
            //노드가 n개 있을 때 다익스트라를 위해서 반복수는 n-1번이면 된다.
            //원하지 않으면 각각의 노드가 모두 true인지 확인하는 식으로 구현해도 된다.
            int min=Integer.MAX_VALUE;
            int min_index=-1;

            //최소값 찾기
            for(int i=1;i<n+1;i++){
                if(!check[i] && distance[i]!=Integer.MAX_VALUE){
                    if(distance[i]<min ){
                        min=distance[i];
                        min_index = i;
                    }
                }
            }

            check[min_index] = true;
            for(int i=1;i<n+1;i++){
                if(!check[i] && maps[min_index][i]!=0){
                    if(distance[i]>distance[min_index]+maps[min_index][i]){
                        distance[i] = distance[min_index]+maps[min_index][i];
                    }
                }
            }

        }

        //결과값 출력
        for(int i=1;i<n+1;i++){
            System.out.print(distance[i]+" ");
        }
        System.out.println("");

    }
}
```

```java
public class Main {

    public static void main(String[] args) {
        Graph g = new Graph(8);
        g.input(1, 2, 3);
        g.input(1, 5, 4);
        g.input(1, 4, 4);
        g.input(2, 3, 2);
        g.input(3, 4, 1);
        g.input(4, 5, 2);
        g.input(5, 6, 4);
        g.input(4, 7, 6);
        g.input(7, 6, 3);
        g.input(3, 8, 3);
        g.input(6, 8, 2);
        g.dijkstra(1);
    }

}

```


## 알고리즘 문제
- [프로그래머스 배달](https://programmers.co.kr/learn/courses/30/lessons/12978)
- [알고리즘 문제 해설](https://devham76.github.io/assets/portfolio/algorithm/programmers-12978)

---
## Reference
- <https://bumbums.tistory.com/4>
- <https://mattlee.tistory.com/50>
