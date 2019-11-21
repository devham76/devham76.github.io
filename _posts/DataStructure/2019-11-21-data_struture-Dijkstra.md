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

- distnace[1] = Math.min (distance[1] , distance[4] + weight[2][1]) 이므로 distance[1]은 7에서 5로 변경된다.

#### 3.
![dijkstra4](https://user-images.githubusercontent.com/55946791/69313587-54b3d500-0c75-11ea-9bb3-506430f5bb66.png)
- 완료된 모습이다


---
## Reference
<https://mattlee.tistory.com/50>
