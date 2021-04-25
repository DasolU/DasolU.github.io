---
layout: post
title: Programmers 네트워크 문제
subititle: BFS 알고리즘 구현시 visited = [] vs. visted=[False for i in range(n)]
categories: CodingTest
tags: [CodingTest, Efficiency]
---
프로그래머스 깊이/너비 우선 탐색(DFS/BFS) 카테고리의 [네트워크][1] 문제의 솔루션 3 가지를 비교하고 시간 단축 방법을 정리했습니다.

[BFS 알고리즘][2]을 공부했기에 문제에 적용해보려 시도했지만 쉽지 않았습니다.

그래서 이번 문제를 풀 때 필요했던 생각의 방향을 줄글로 기록합니다.

## 아이디어

* 첫 번째 노드 (임의의 노드) 시작해서 연결된 모든 노드를 방문하며 연결된 모든 노드를 탐색한다. 그리고 visited에 기록한다.
* 이러한 방법을 사용하면 두 번째 노드에서 탐색을 시작할 때, 두 번째 노드와 연결이 되어있지만 이미 방문했던 (= 첫 번째 노드와 연결되어 있는) 노드는 탐색할 필요가 없게 된다.
따라서 이미 연결된 노드들과 그에 연결되지 않은 노드를 찾을 수 있게 된다.

알고리즘 작동 순서>
1. 첫 번째 컴퓨터부터 마지막 컴퓨터까지 조사한다.
2. 첫 번째 컴퓨터 조사를 시작한다. 첫 번째 컴퓨터를 방문하지 않았었다면 방문한다.
3. 방문해서 첫 번째 컴퓨터와 연결된 모든 자식 컴퓨터들을 탐색 목록에 저장하고, 방문한 목록에 저장한다.
4. 첫 번째 컴퓨터에 대한 조사가 끝나면 찾아낸 네트워크 개수에 하나를 추가한다.
6. 두 번째 컴퓨터를 조사하기 전에, 방문한 목록에 있는지 확인한다.
7. 두 번째 컴퓨터가 방문한 목록에 있기 때문에 조사를 하지 않는다.

## visted = [False for i in range(n)] 사용

### 선택한 답 ⭕️

* 먼저 시간 단축을 위해서 [지난번 테스트에서 배운점][3]을 적용했습니다.

  즉, queue 구현시 로 list말고 deque를 사용했습니다.

* solution 2에서 예상된 문제> if node not in visited 방식의 시간 복잡도는 O(n)으로 클 것으로 예상.
  따라서, visited를 미리 만들고 해당 노드와 관련된 값만 조사하여 시간을 단축했습니다.

```python
from collections import deque

def BFS(n, computers, node, visited):
    q = deque([node])
    while q:
        node = q.popleft()
        visited[node]=True
        for com in range(n):
            if com !=node and computers[node][com] == 1:
                if visited[com] == False:
                    q.append(com)

def solution2_1(n, computers):
    answer = 0
    visited = [False for i in range(n)]
    for node in range(n):
        if visited[node] == False:
        # if node not in visited:# O(n) 모든 원소들을 확인해야해서 시간 복잡도가 늘었던 것이 문제인 것으로 추측
            BFS(n, computers, node, visited)
            answer +=1
    return answer
```

#### 성능

* 비교: solution 2-1의 테스트 11 케이스의 경우 아래 solution 2에서 걸린 시간을 반정도로 크게 단축되었다.

```python
테스트 1 〉	통과 (0.02ms, 10.2MB)
테스트 2 〉	통과 (0.02ms, 10.2MB)
테스트 3 〉	통과 (0.10ms, 10.2MB)
테스트 4 〉	통과 (0.12ms, 10.2MB)
테스트 5 〉	통과 (0.01ms, 10.2MB)
테스트 6 〉	통과 (1.41ms, 10.3MB)
테스트 7 〉	통과 (0.03ms, 10.2MB)
테스트 8 〉	통과 (0.65ms, 10.4MB)
테스트 9 〉	통과 (0.28ms, 10.1MB)
테스트 10 〉	통과 (0.40ms, 10.3MB)
테스트 11 〉	통과 (3.68ms, 10.3MB)
테스트 12 〉	통과 (1.92ms, 10.3MB)
테스트 13 〉	통과 (1.07ms, 10.2MB)
```

### visited = [] 사용 ❌

```python
from collections import deque

def BFS(n, computers, node, visited):
    q = deque([node])
    while q:
        node = q.popleft()
        visited.append(node)
        for com in range(n):
            if com !=node and computers[node][com] == 1:
                if com not in visited:
                    q.append(com)

def solution2(n, computers):
    answer = 0
    visited = deque()
    for node in range(n):
        if node not in visited:
            BFS(n, computers, node, visited)
            answer +=1
    return answer
```

#### 성능

```python
테스트 1 〉	통과 (0.02ms, 10.2MB)
테스트 2 〉	통과 (0.02ms, 10.3MB)
테스트 3 〉	통과 (0.10ms, 10.3MB)
테스트 4 〉	통과 (0.18ms, 10.2MB)
테스트 5 〉	통과 (0.01ms, 10.1MB)
테스트 6 〉	통과 (2.27ms, 10.1MB)
테스트 7 〉	통과 (0.03ms, 10.2MB)
테스트 8 〉	통과 (1.00ms, 10.2MB)
테스트 9 〉	통과 (0.82ms, 10.2MB)
테스트 10 〉	통과 (0.47ms, 10.2MB)
테스트 11 〉	통과 (7.29ms, 10.3MB)
테스트 12 〉	통과 (3.57ms, 10.2MB)
테스트 13 〉	통과 (1.35ms, 10.1MB)
```

## Queue 사용

```python
from collections import deque
def solution3(prices):
    answer = []
    q = deque(prices)
    q_idx = deque(list(range(0,len(prices))))
    max_idx = len(prices)-1
    while q:
        time = 0
        node = q.popleft()
        node_idx = q_idx.popleft()
        for i in range(len(q)):
            if node>q[i]:
                time = (i+node_idx+1)-node_idx
                break
        if time == 0:
            time = max_idx-node_idx
        answer.append(time)
    return answer
```

### 성능

```python
정확성: 66.7
효율성: 26.7
합계: 93.3 / 100.0

정확성 테스트
테스트 1 〉    통과 (0.01ms, 10.2MB)
테스트 2 〉    통과 (0.08ms, 10.3MB)
테스트 3 〉    통과 (0.92ms, 10.2MB)
테스트 4 〉    통과 (1.07ms, 10.3MB)
테스트 5 〉    통과 (1.09ms, 10.2MB)
테스트 6 〉    통과 (0.04ms, 10.2MB)
테스트 7 〉    통과 (0.40ms, 10.2MB)
테스트 8 〉    통과 (0.70ms, 10.3MB)
테스트 9 〉    통과 (0.05ms, 10.2MB)
테스트 10 〉   통과 (1.79ms, 10.3MB)
효율성 테스트
테스트 1 〉    통과 (247.57ms, 21.2MB)
테스트 2 〉    통과 (149.96ms, 19MB)
테스트 3 〉    실패 (시간 초과)
테스트 4 〉    통과 (193.79ms, 19.7MB)
테스트 5 〉    통과 (97.84ms, 18.3MB)
```

## 배운점

* visited=[False for i in range(n)]처럼
  visited 리스트를 노드 개수만큼 False로 미리 만들어놓고
  node를 방문했는지 조사할 때, if visited[node] == False:을 사용하자! 
  
  visted=[]
  visited.append(node)
  if new_node not in visited:
  위의 예시처럼 visited를 빈 list로 만들고 원소들을 append하는 방식을 사용하면, 
  새로 방문하는 노드가 visited 목록에 있는지 조사할 때 시간 복잡도가 O(n)으로, 
  이미 방문한 node가 많을수록 더 많은 시간을 소모하게 된다.
  
  따라서 visited=[False for i in range(n)]처럼
  visited 리스트를 노드 개수만큼 False로 미리 만들어놓고
  if visited[node] == False: 처럼 
  해당 node의 값이 False인 경우 조사하면 시간 복잡도가 O(1)이므로
  시간이 단축된다.

[1]: https://programmers.co.kr/learn/courses/30/parts/12421

[2]: https://dasolu.github.io/algorithm/2021/04/20/BFS.html
[3]: https://dasolu.github.io/codingtest/2021/04/21/list-pop-vs-collections-deque.html

