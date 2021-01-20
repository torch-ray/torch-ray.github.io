---
title: "백준 1260번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/1260/
layout: single
---

## 백준 - DFS와 BFS

<img width="1158" alt="스크린샷 2021-01-20 오전 7 41 49" src="https://user-images.githubusercontent.com/74946802/105102917-fd1c2e00-5af2-11eb-880b-9275d65bae31.png">

문제 제목 그대로 DFS와 BFS를 출력하면된다. 방문할 수 있는 노드가 여러개인 경우 작은 숫자부터 방문하고, 더 이상 방문할 노드가 없으면 종료한다.

- 체크포인트: [DFS와 BFS란?](https://www.youtube.com/watch?v=_hxFgg7TLZQ)

## 입력값을 받아 딕셔너리 형태로 노드 생성
``` swift
let guideLine = readLine()!.split{$0==" "}.map{Int($0)!}
let (n, start) = (guideLine[1], guideLine[2])
var graph = [Int: [Int]()]
```
첫 번째 줄에는 [4, 5, 1]과 같이 정점의 수, 간선의 수, 시작 위치가 주어진다. 정점의 수는 문제를 해결하는데 활용되지 않기 때문에 따로 변수에 저장하지 않는다. 간선의 수는 그 수만큼 간선이 연결하는 정점의 정보를 입력받아야 하기 때문에(for문을 활용하여), n에 저장하고 DFS와 BFS를 시작할 정점의 정보는 start에 저장한다. 이후 각 정점마다 연결되어있는 정점의 정보를 저장할 빈 딕셔너리를 선언한다.

## 정점의 정보를 입력받아 그래프 생성
``` swift
for _ in 0..<n {
  let tmp = readLine()!.split{$0==" "}.map{Int($0)!}
  let a = tmp[0]
  let b = tmp[1]

  if graph[a] == nil {
    graph[a] == [b]
  } else {
    graph[a].append(b)
  }

  if graph[b] == nil {
    graph[b] == [a]
  } else {
    graph[b].append[a]
  }
}
```
간선의 수만큼 for문을 돌면서 연결된 정점의 정보를 tmp에 저장한다. [1, 2]가 tmp에 저장된 경우 [1]은 a, [2]는 b에 저장한다. 첫 번째 if문에서는 graph[1]은 현재 nil값이기 때문에 [1: [2]]의 형태로 저장되고, graph[2]의 값도 nil이기 때문에 [2: [1]]이 저장된다. 이런식으로 [1, 2], [1, 3], [1, 4], [2, 4], [3, 4]를 모두 반복하면 graph에 [1: [2, 3, 4], 2: [1, 4], 3: [1, 4], 4: [1, 2, 3]] 와 같이 저장된다.

## 스택, 큐 형식에 맞춰서 딕셔너리 값을 정렬
``` swift
for key in graph.keys {
  graph[key]?.sort(by: >)
}

var printDFSResult = ""
for i in DFS(graph, start) {
  printDFSResult += String(i) + " "
}

for key in graph.keys {
  graph[key]?.sort(by: <)
}

var printBFSResult = ""
for i in BFS(graph, start) {
  printBFSResult += String(i) + " "
}
```
DFS는 스택, BFS는 큐를 활용할 예정이기 때문에 DFS는 내림차순 정렬, BFS는 오름차순 정렬된 graph값을 입력받을 수 있도록 정렬을 한다. 이전 코드에서 graph값을 정렬하여 설명했지만 graph는 순서가 없기 때문에 정렬하지 않으면 어떠한 형태로 DFS, BFS를 탐색하게 될지 알 수 없다. 참고로 해당 코드에서 DFS(graph, start)나 BFS(graph, start)는 아래에서 설명할 함수의 이름이다.

## DFS
``` swift
func DFS(_ graph: [Int, [Int]], _ start: Int) -> [Int] {
  var visited = [Int]()
  var stack = [start]

  while stack.count > 0 {
    let node = stack.popLast()!
    if visited.contains(node) {
      continue
    } else {
      visited.append(node)
      if let tmp = graph[node] {
        stack += tmp
      }
    }
  }
  return visited
}
```
DFS함수에 내림차순으로 정렬된 graph와 start값을 입력한다. visited 변수는 방문한 정점의 정보를 저장할 예정이기 때문에 현재는 빈 배열로 선언한다. stack에는 start값을 넣고 DFS를 시작한다. while문은 모든 정점을 다 방문한 경우(즉, 스택이 빈 경우) 종료되도록 stack.count가 0보다 큰 경우에만 반복되도록 설정한다. node상수에는 stack의 값을 하나씩 pop해서 저장한다. 현재는 [1]만 들어가있기 때문에 node에 1이 저장된다. 다음 if문이 실행되는데 visited 변수는 현재 비어 있기 때문에 else문이 실행되고 visited에 1이 저장된다. 그리고 graph[node]는 현재 graph[1]이기 때문에 stack에 내림차순된 graph[1]의 값인 [4, 3, 2]가 저장된다. 그리고 while문은 모든 정점을 방문할 때까지 반복되고 종료된다.

## BFS
``` swift
func BFS(_ graph: [Int, [Int]], _ start: Int) -> [Int] {
  var visited = [Int]()
  var queue = [start]

  while queue.count > 0 {
    let node = queue.remove(at: 0)
    if visited.contains(node) {
      continue
    } else {
      visited.append(node)
      if let tmp = graph[node] {
        queue += tmp
      }
    }
  }
  return visited
}
```
BFS도 DFS와 전체적인 동작원리는 비슷하다. 하지만 다른점은 stack대신에 queue 자료구조를 사용한다는 것이다. 따라서 DFS와의 차이점은 popLast가 아니라 remove(at: 0)이 사용된다는 점이고(FIFO), 입력받은 graph의 값도 오름차순이기 때문에 graph[1]을 queue에 저장할 때 [4, 3, 2]가 아닌 [2, 3, 4]가 저장된다는 점이다.

## 전체코드
``` swift
let guideLine = readLine()!.split{$0==" "}.map{Int($0)!}
let (n, start) = (guideLine[1], guideLine[2])
var graph = [Int: [Int]]()

for _ in 0..<n {
    let tmp = readLine()!.split{$0==" "}.map{Int($0)!}
    let a = tmp[0]
    let b = tmp[1]

    if graph[a] == nil {
        graph[a] = [b]
    } else {
        graph[a]?.append(b)
    }
    if graph[b] == nil {
        graph[b] = [a]
    } else {
        graph[b]?.append(a)
    }
}

for key in graph.keys {
    graph[key]?.sort(by: >)
}

var printDFSResult = ""
for i in DFS(graph, start) {
    printDFSResult += String(i) + " "
}

for key in graph.keys {
    graph[key]?.sort(by: <)
}

var printBFSResult = ""
for i in BFS(graph, start) {
    printBFSResult += String(i) + " "
}

func DFS(_ graph: [Int: [Int]], _ start: Int) -> [Int] {
    var visited = [Int]()
    var stack = [start]

    while stack.count > 0 {
        let node = stack.popLast()!
        if visited.contains(node) {
            continue
        } else {
            visited.append(node)
            if let tmp = graph[node] {
                stack += tmp
            }
        }
    }
    return visited
}

func BFS(_ graph: [Int: [Int]], _ start: Int) -> [Int] {
    var visited = [Int]()
    var queue = [start]

    while queue.count > 0 {
        let node = queue.remove(at: 0)
        if visited.contains(node) {
            continue
        } else {
            visited.append(node)
            if let tmp = graph[node] {
                queue += tmp
            }
        }
    }
    return visited
}

print(printDFSResult)
print(printBFSResult)
```
