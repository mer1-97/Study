## 시작전
https://github.com/mer1-97/Study/blob/main/%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/%EC%9D%B4%EC%BD%94%ED%85%8C/%EA%B8%B0%EC%B4%88%EC%9D%B4%EB%A1%A0.md
<br>
위 링크에서 스택, 큐, 재귀함수, 인접 행렬, 인접 리스트 공부 필요
<br>

### DFS(Depth-First Search) -> 스택 자료구조이며 재귀 함수 이용하여 구현
![image](https://user-images.githubusercontent.com/76419721/141737782-a6da4316-0adf-495d-a9b4-adcfb3d30369.png)
<br>
깊이 우선 탐색이라고 부르며, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
특정한 경로로 탐색하다가 특정한 상황에서 최대한 깊숙이 들어가서 노드를 방문한 후, 다시 돌아가 다른 경로로 탐색하는 알고리즘

DFS는 <b>스택 자료구조</b>를 이용하며 구체적인 동작은 아래와 같음 (선입후출, 프링글스 생각)
1) 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
2) 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리를 한다.
   방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
3) 2번의 과정을 더 이상 수행할 수 없을 떄 까지 반복한다.

cf) '방문 처리'는 스택에 한 번 삽입되어 처리된 노드가 다시 삽입되지 않게 체크하는 것을 의미하며, 방문 처리를 함으로써 각 노드를 한 번씩만 처리할 수 있다.
    코딩 테스트에서는 조건에서 특별한 말이 없다면 번호가 낮은 순서부터 처리하도록 구현하자

<br>

![image](https://user-images.githubusercontent.com/76419721/141738554-04ca559c-9d9e-4fe9-b7dd-35f423aa74fc.png)
<br>
위 그래프를 DFS를 이용하여 탐색해보자.
노드 1을 시작 노드로 설정하고 인접한 노드 중에 방문하지 않은 노드가 여러 개 있으면 번호가 낮은 순서부터 처리하면 된다.

```python
# DFS 예제
def dfs(graph, v, visited):
    # 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
        # visited[i]가 False일 경우 시행, 즉 방문하지 않은 노드일 경우
        if not visited[i]:
            dfs(graph, i, visited)

# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트), graph가 9개 이므로 * 9
visited = [False] * 9

# 정의된 DFS 함수 호출 (1은 가장 첫번째 노드인 1을 뜻함)
dfs(graph, 1, visited)
``` 
방문 순서 : 1->2->7->6->8->3->4->5 (p138 참고)

<br>

### BFS(Breadth-First Search) -> 큐 자료구조이며 deque(덱) 라이브러리를 이용하여 구현
![image](https://user-images.githubusercontent.com/76419721/141740925-343ae2bb-edd0-4a97-bf14-24bf4684bdd0.png)
<br>
너비 우선 탐색이라고 부르며, 가까운 노드부터 탐색하는 알고리즘
최대한 멀리 있는 노드를 우선적으로 탐색하는 DFS와 달리 BFS는 반대임

BFS는 <b>큐 자료구조</b>를 이용하며, 구체적인 동작 방식은 아래와 같음 (선입선출, 놀이공원 대기줄 생각)
1) 탐색 시작 노드를 큐에 삽입하고 방문처리를 한다.
2) 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다.
3) 2번의 과정을 더 이상 수행할 수 없을 때 까지 반복한다.

cf) 인접한 노드가 여러 개 있을 때, 숫자가 작은 노드부터 먼저 큐에 삽입한다고 가정하고 from collections import deque로 구현
    코딩 테스트에서는 보통 DFS보다는 BFS 구현이 조금 더 빠르게 동작함
<br>

![image](https://user-images.githubusercontent.com/76419721/141738554-04ca559c-9d9e-4fe9-b7dd-35f423aa74fc.png)
<br>

```python
# BFS 예제
# 큐 자료구조인 BFS를 구현하기 위해 deque 라이브러리 사용
from collections import deque

# BFS 메서드 정의
def bfs(graph, start, visited):
    # 큐(Queue) 구현을 위해 deque 사용
    queue = deque([start])
    # 현재 노드를 방문 처리
    visited[start] = True
    # 큐가 빌 때까지 반복
    while queue:
        # 큐에서 하나의 원소를 뽑아 출력
        v = queue.popleft()
        print(v, end=' ')
        # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
        for i in graph[v]:
            # visited[i]가 False일 경우 시행, 즉 방문하지 않은 노드일 경우
            if not visited[i]:
                queue.append(i)
                visited[i] = True

# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트), graph가 9개 이므로 * 9
visited = [False] * 9

# 정의된 DFS 함수 호출 (1은 가장 첫번째 노드인 1을 뜻함)
bfs(graph, 1, visited)
```
방문 순서 : 1->2->3->8->7->4->5->6 (p144 참고)

<br>

### 정리
![image](https://user-images.githubusercontent.com/76419721/141744274-9594e092-b018-4ff8-8d93-bba4c48c4769.png)

<br>
앞에 예시는 전형적인 그래프 그림을 이용했으나 1차원 배열이나 2차원 배열 또한 그래프 형태로 생각하면 수월하게 문제를 풀 수 있다.
코딩 테스트 중 2차원 배열에서의 탐색 문제를 만나면 그래프 형태로 바꿔서 생각하면 풀이 방법을 조금 더 쉽게 떠올릴 수 있다고 함

<br>
<br>

![image](https://user-images.githubusercontent.com/76419721/141981768-8d44a20c-20ca-4872-99a5-d5a0765545ca.png)
<br>
https://devuna.tistory.com/32 참고
<br>
<br>

## 음료수 얼려 먹기 (p149)

### 접근법
```python
- 얼음틀 중에서 0인 부분은 뚫려있는 부분으로 아이스크림을 생성하는데 필요한 부분이다. 
- 얼음틀 중 1인 부분은 칸막이가 있는 부분으로 모양을 결정해 준다. 
- 문제에서는 생성 가능한 아이스크림의 개수를 물어봤으므로 0인 부분을 중점적으로 확인해야 한다.

맨 왼쪽 위부터 차례로 모두 탐색해 0인 위치를 찾았으면 그 지점 기준으로 연결된 모든 0인 부분을 모두 1로 만들면 결과적으로 연결된 부분을 한 번만 카운트하게 되는 효과를 얻게 된다. 
즉, 우리는 0인 부분의 총 개수를 구하는 것이 아닌 0으로 연결된 덩어리 개수를 구하므로 한 번만 카운트하면 된다. 
0인 지점에서 카운트를 한 번하고 dfs 알고리즘을 통해 재귀적으로 연결된 모든 0인 부분을 1로 만들게 구현하면 된다. 


1) 구멍이 뚫려있는 부분을 찾았으면 True를 반환하게 하는 함수(dfs)를 구현한다. 
2) 구체적으로 해당 함수는 찾은 구멍이 뚫려있는 부분을 기준으로 최대한 탐색해서 뚫려있으면서 연결되어 있는 모든 0인 부분을 1로 만들고 True를 반환한다. 
3) 이때 모든 탐색하는 알고리즘을 dfs 알고리즘을 사용해 구현하는데 얼음틀을 벗어나면 False를 반환하게 한다. 
4) 탐색한 부분이 0이 아닌 칸막이 부분이면 False를 반환하게 한다. 
5) dfs 함수 결과가 True인 개수를 카운트한다. 

참고) https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=jiyong615&logNo=222219342396
```

```python
n, m = map(int, input().split())

# 2차원 리스트의 맵 정보 입력받기
graph = []
for i in range(n):
    graph.append(list(map(int, input())))

# DFS는 재귀적으로 구현해야 함
def bfs(x, y):
    # 주어진 범위를 벗어나느 경우에는 즉시 종료
    if x <= -1 or x >= n or y <= -1 or y >= m: 
        return False
    # 현재 노드를 아직 방문하지 않았다면
    if graph[x][y] == 0:
        # 해당 노드 방문 처리
        graph[x][y] = 1
        # 상,하,좌,우의 위치도 모두 재귀적으로 호출
        bfs(x-1,y)
        bfs(x+1,y)
        bfs(x,y-1)
        bfs(x,y+1)
        return True
    return False

# 모든 노드(위치)에 대해 음료수 채우기
result = 0
for i in range(n):
    for j in range(m):
        if bfs(i,j) == True:
            result += 1

print(result)
```
<br>

