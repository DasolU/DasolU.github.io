---
layout: post
title: Summary for BFS Algorithm
subtitle: BFS 알고리즘 풀이를 위한 필수 함수 총정리
categories: CodingTest
tags: [CodingTest, Summary]
---
🌟코딩테스트에서 **BFS** 문제를 풀기 위해 꼭 필요한 함수 총 정리!!!!!🌟

코테 전에 **BFS 알고리즘 필수 요약** 보고 들어가세요!

계속 업데이트 합니다. 



## Queue 만드는 방법

queue에 2D node를 추가할 때 시공간 복잡도가 가장 낮은 방법.

(현재까지 진행한 여러가지 테스트롤 통해 내린 결론이며, 향후 변경될 수 있다.)

1. q = deque()
2. q.append((sy, sx))
3. (y, x) = q.popleft()
4. q.append((ny, nx))

## Graph 만드는 방법

### node와 edge가 주어질 때

[13023번 - ABCDE](https://www.acmicpc.net/problem/13023)

[1260번 - DFS와 BFS](https://www.acmicpc.net/problem/1260)

[11724번 - 연결 요소의 개수](https://www.acmicpc.net/problem/11724)

[1707번 - 이분 그래프](https://www.acmicpc.net/problem/1707)

```python
# Make Graph
graph=[[]for i in range(node+1)]
for _ in range(edge):
    node1, node2 = map(int,sys.stdin.readline().split())
    graph[node1].append(node2)
    graph[node2].append(node1)
```

### N X M 인접 행렬(adjacency matrix)이 주어질 때

[2667번 - 단지번호붙이기](https://www.acmicpc.net/problem/2667)

[2178번 - 미로 탐색](https://www.acmicpc.net/problem/2178)

[7576번 - 토마토](https://www.acmicpc.net/problem/7576)

[7562번 - 나이트의 이동](https://www.acmicpc.net/problem/7562)

```python
input = sys.stdin.readline
n = int(input())

graph=[]
for i in range(row):
    line = input().split() # returns list ex>['0110100']
    graph.append([])
    for j in line[0]:
        graph[i].append(int(j))

visited = [[0]*column for _ in range(row)]
```



## 문제 유형

### 모든 노드 방문할 때

* 노드 n개가 연결된 경로가 존재하는지 구하기

[13023번 - ABCDE](https://www.acmicpc.net/problem/13023)

 	1. for문 사용하여 모든 노드 방문
      	1. DFS: level == n-1일 때 return



* 모든 노드 방문하며 그 순서 출력하기

[1260번 - DFS와 BFS](https://www.acmicpc.net/problem/1260)

1. visited = []에 pop한 node를 추가한다
2. visited를 return한다



* 연결 요소(connected component)의 개수 구하기

[11724번 - 연결 요소의 개수](https://www.acmicpc.net/problem/11724)

1. for문 사용하여 모든 노드 방문
   1. 방문하지 않은 노드만 방문한다
      1. BFS

### 일부 노드만 선택적으로 방문할 때: 2D

📌 1. 먼저 자식 노드의 위치가 2D array index 범위 안에 위치하는지 조사하기 

​	✔️ 가능한 < 또는 >을 사용하자‼️ <= 또는 >= 사용을 피하자‼️

​		 예를들어 0<=ny <= n - 1 을 사용하지 말고, 예를들어 0<=ny < n 을 사용하자.

​		 이유)  <=을 사용하는 경우 -1 연산을 추가로 하게 되므로 ~ 효율성이 낮아진다.	

​	✔️이 과정이 선행되어야 방문 여부를 확인할 때 2D array index 범위를 벗어나는 error가 발생하지 않는다.



📌 2. 이후 자식 노드의 방문 여부를 조사하고, 동시에 방문 여부 리스트에 탐색 비용을 저장하자‼️



#### 자식 노드의 탐색 비용이 동일할 때

📌 목표 node까지 도달하는데 필요한 최소한의 edge개수/시간/이동/거리를 구하는 방법은?

즉, 탐색 깊이를 count할 때

➡️ 동일한 부모 노드와 연결된 자식 노드라면 같은 level을 가지도록 한다.

즉, 모든 자식 노드의 visited 값에 부모 노드의 visited 값에 1을 추가한다.

이 방법을 사용하면 목표 node에 도달했을 때 visitied에 저장된 level이 자연스럽게 최소 edge개수/시간/이동/거리가 된다.



##### 1D: 다양한 방향

* 최단 경로로 이동할 때 지나가는 노드를 print 하기

[13913번 - 숨바꼭질 4](https://www.acmicpc.net/problem/13913)

BFS 방법을 사용하면 같은 level의 자식 노드를 node를 방문한다.

따라서 node를 pop하여 모두 저장하는 방법으로는 최단 경로를 print 할 수 없다.

➡️ parent list를 만들어서, 자식 노드 방문시 부모 노드를 저장한다. 

BFS를 마치고 도착한 노드의 parent list 값을 확인하여 이전에 방문한 노드를 알아내는 것을 반복한다.



 

##### 2D: 좌 우 상 하

목적지에 도달하기 위한 최소의 칸 수 구하기

* 목적지에 도달하는 최소 이동 거리 구하기

[2178번 - 미로 탐색](https://www.acmicpc.net/problem/2178)

1. visited = [[0]*node for _ in range(node)]
2. for 문으로 가능한 모든 자식 노드 조사 (if 문으로 각 경우를 조사하는 것이 더 빠르지만 코드가 길어져서 작성 시간이 더 오래 걸린다.)
   1. 자식 노드의 row와 column이 2D array의 Index 범위를 벗어나지 않는지 조사
      1. 방문하지 않은 자식 노드만 방문
         1. visited\[child_y][child_x] = visited\[parent_y][parent_x] + 1
         2. 

* 연결 요소(connected component)의 개수 구하기

[2667번 - 단지번호붙이기](https://www.acmicpc.net/problem/2667)



* 시작 노드가 여러 개인 경우, 가능한 모든 시작 노드에서 동시에 BFS 탐색하기

➡️ Queue안에 모든 시작 노드를 추가한다. 이 방법으로 차례로 BFS를 진행하게 된다.

[7576번 - 토마토](https://www.acmicpc.net/problem/7576)

예를 들어 이 문제에선 [0,0]과 [3,5]에 토마토가 존재하므로, 탐색 시작 노드가 2개가 된다.

따라서 두 노드를 queue에 올려서 BFS를 진행하면서, 자식 토마토가 익는데 걸리는 시간을 채워준다.

그 결과는 다음과 같다.

[[ 1 -1  7  6  5  4]
 [ 2 -1  6  5  4  3]
 [ 3  4  5  6 -1  2]
 [ 4  5  6  7 -1  1]]

##### 2D: 다양한 방향

* 목적지에 도달하는 최소 이동 거리 구하기

[7562번 - 나이트의 이동](https://www.acmicpc.net/problem/7562)

```python
dx = [-1,-2,-2,-1,1,2,2,1]
dy = [2,1,-1,-2,-2,-1,1,2]

for i in range(8):
    ny, nx = y + dy[i], x + dx[i]
    if 0 <= nx < l and 0 <= ny < l and visited[ny][nx] == -1:
        q.append((ny, nx))
        visited[ny][nx] = visited[y][x] + 1
```

#### 자식 노드의 탐색 비용이 서로 다를 때

* 최단 경로이면서 탐색 비용이 최소인 경로 구하기

[1261 알고스팟][1], [13549 숨바꼭질 3][2]

➡️ 탐색 비용이 작은 자식 노드를 queue의 앞에 추가하고, 탐색 비용이 큰 자식 노드는 뒤에 추가한다.

​	✔️ q.appendleft(), q.append() 를 사용한다.

이 방법은 비용이 적은 경로부터 우선적으로 탐색하고, 가장 적은 비용에 대한 탐색이 끝나고 나서야 비로소 더 큰 비용의 경로를 탐색하기 시작한다.

따라서 이 방법을 통해 탐색 비용과 길이가 이 최소인 경로를 찾을 수 있다.



* 이분 그래프 (Bipartite Graph) 판별하기

이분 그래프란? 그래프의 정점의 집합을 둘로 분할하여, 각 집합에 속한 정점끼리는 서로 인접하지 않는 그래프이다.

[1707번 - 이분 그래프](https://www.acmicpc.net/problem/1707)

➡️ 방문하지 않은 자식 노드의 탐색 비용 저장시, 부모 노드의 값에 -1을 곱하여 서로 다른 집합임을 표시한다.

만약 자식 노드를 이미 방문했으며, 부모 노드와 탐색 비용이 동일하다면 return false



[1]: https://www.acmicpc.net/problem/1261
[2]: https://www.acmicpc.net/problem/13549