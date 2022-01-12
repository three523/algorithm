# DFS, BFS
* 모든 예시는 트리구조로 짜여있지만 트리구조가 아니라 이어져있는 노드가 있어도 아무 문제없다
## DFS(Depth-First Serach) 깊이 우선 탐색 이란?
 루트 노드에서 자식노드를 탐색할때 자식노드의 가장 깊은 곳까지 탐색한 뒤에 다른 자식노드를 탐색하는 방식을 말한다.   
 보통 스택과 재귀함수를 사용하여 구현을 한다.
- 길찾기로 예를 들면 가던 방향으로 끝까지 가보고 갈곳이 없다면 전에 가장 가까운 갈림길로 돌아와 다른 방향으로 가보는 방식이다
- **모든 노드를 방문해야 할 떼** 이 알고리즘을 사용한다
- 단순 검색 속도는 보통 DFS보다 BFS가 더 빠르다

```
var graph: [Int:[Int]] = [
    1: [2,4,8],
    2: [3],
    3: [],
    4: [5,7],
    5: [6],
    6: [],
    7: [],
    8: [9],
    9: [],
]
var visited: [Int] = []

func dfs(val: Int) {
    visited.append(val)
    for nextVal in graph[val]! {
        dfs(val: nextVal)
    }
}

dfs(val: 1)
print(visited) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
### DFS 장단점
1. 장점
  - 재귀적으로 사용하지 않는다면 현 경로상의 노드만 기억하므로 저장공간이 적게 사용된다.
  - 목표 노드가 깊이 있을경우 빠르게 구할 수 있다.
2. 단점
  - 얻어진 답이 최단 경로는 아닐 가능성이 있다.



## BFS(Breadth First Search) 너비 우선 탐색이란?
- 길찾기를 예시로 들면 갈림길에서 막다른 길까지 가는게 아니라 한번 갔다가 돌아와 다른길을 가보고 다시 돌아오는식으로 전부 가보는 방식
- 최단 경로를 찾는데 가장 적절하다
- 큐 자료구조를 사용하여 진행한다

```
var graph: [Int:[Int]] = [
    1: [2,4,8],
    2: [3],
    3: [],
    4: [5,7],
    5: [6],
    6: [],
    7: [],
    8: [9],
    9: [],
]

func bfs(val: Int) {
    var queue: [Int] = graph[val]!
    var temp = 0
    visited.append(val)
    while !queue.isEmpty {
        temp = queue.removeFirst()
        visited.append(temp)
        if let node = graph[temp] {
            node.forEach { value in
                queue.append(value)
            }
        }
    }
}

bfs(val: 1)
print(visited) // [1, 2, 4, 8, 3, 5, 7, 9, 6]
```
### BFS 장단점
1. 장점 
  - DFS에 비해 속도가 빠른편이다
  - 최단 경로를 알 수 있다
3. 단점 
  - 큐에 노드에 저장해야하기 때문에 상황에 따라 저장공간이 많이 필요하다

## DFS,BFS 그림
![DFS,BFS](https://user-images.githubusercontent.com/71269216/149136494-78b34a2d-dcf6-4765-8c1d-aaec44b83148.gif)
 출처: 나무위키
