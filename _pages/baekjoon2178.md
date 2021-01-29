---
title: "백준 2178번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/2178/
layout: single
---

## 백준 - 미로탐색

<img width="1160" alt="스크린샷 2021-01-29 오전 8 50 23" src="https://user-images.githubusercontent.com/74946802/106213062-3fd6b800-620f-11eb-80eb-1292e6048a62.png">
<img width="1160" alt="스크린샷 2021-01-29 오전 8 50 38" src="https://user-images.githubusercontent.com/74946802/106213082-49f8b680-620f-11eb-9943-d5ef4df6e02a.png">

N x M 미로가 주어질 때 (1, 1)에서 출발하여 도착지 (N, M)까지 이동하는 최소의 칸 수를 구하는 프로그램을 작성하면 된다. 주어지는 미로 1은 이동할 수 있는 길, 0은 이동할 수 없는 길이다.

- 체크포인트: BFS를 활용한다.

## 입력값 저장 및 미로생성
``` swift
let input = readLine!.split{$0==" "}.map{Int($0)!}
let (n, m) = (input[0], input[1])

var maze = [[Int]]()
for _ in 0..<n {maze.append(readLine!.map{Int(String($0))!})}
```
N x M 을 받아서 (n, m)에저장하고 n만큼 돌면서 미로정보를 입력받는다. 미로는 각 행이 [Int]로 구성되어있기 때문에 [[Int]]배열에 저장한다.

## 큐 및 상하좌우 이동 좌표생성
``` swift
var queue = [(0, 0)]
let dx = [-1, 1, 0, 0], dy = [0, 0, -1, 1]
```
미분에서 d를 구하는 것과 마찬가지로 dx, dy의 d는 변화량을 의미한다. 즉, dx, dy는 (x, y)좌표를 상하좌우로 이동시킬 기준값을 담은 배열이다. x가 -1 이면 북쪽, x가 +1이면 남쪽이며 y가 -1이면 서쪽, y가 +1이면 동쪽이다. queue는 BFS를 위해 출발점인 (0, 0)으로 생성해둔다.

## BFS
``` swift
while !queue.isEmpty {
  let (x, y) = queue.removeFirst()
  for i in 0..<4 {
    let nx = x + dx[i], ny = y + dy[i]
    if nx<0 || ny<0 || nx>=n || ny>=m {continue}
    if maze[nx][ny] == 0 {continue}
    if maze[nx][ny] == 1 {
      maze[nx][ny] = maze[x][y] + 1
      queue.append((nx, ny))
    }
  }
}
print(maze[n-1][m-1])
```
queue가 빌 때까지 BFS를 활용하여 탐색한다(n, m에 도착하게되면 더이상 queue.append가 실행되지 않는다). 먼저 queue에 담긴 (0, 0)을 각각 x와 y에 저장한다. 이후 for-loop를 4번 돌면서 조건별로 탐색한다. 4번을 도는 이유는 상하좌우 모두 탐색을 해야하기 때문이다. 그리고 앞서 만들어뒀던 dx, dy를 활용하여 현재 위치 (x, y)의 상하좌우를 모두 탐색한다. 이때 (x, y)의 상하좌우의 좌표가 0보다 작거나, x가 n보다 크거나 같거나, y가 m보다 크거나 같으면 좌표의 범위를 벗어나는 것이 되기 때문에 탐색을 멈추고 다른 방향으로 나아간다.

현재 좌표의 상하좌우의 좌표값이 0인 경우에도 0은 나아갈 수 없는 길이기 때문에 탐색을 멈추고 다른 방향으로 나아간다. 위 조건을 모두 벗어나서 maze[nx][ny]가 1인 경우에만 이전 위치(현재위치)의 값에 1을 더하고 나아간다. 이를 반복하면 (n, m)에 도착했을 때 이전에 이동했던 최종 횟수가 더해져서 출력된다. 시작 위치가 (0, 0)이고 마지막 위치가 maze[n-1][m-1]인 이유는 index가 0부터 시작하기 때문이다.

## 전체코드
``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}  
let (n, m) = (input[0], input[1])

var maze = [[Int]]()
for _ in 0..<n {maze.append(readLine()!.map{Int(String($0))!})}

var queue=[(0, 0)]
let dx=[-1, 1, 0 , 0], dy=[0, 0, -1, 1]

while !queue.isEmpty {
    let (x, y) = queue.removeFirst()
    for i in 0..<4 {
        let nx = x + dx[i], ny = y + dy[i]
        if nx<0 || ny<0 || nx>=n || ny>=m {continue}
        if maze[nx][ny]==0 {continue}
        if maze[nx][ny]==1 {
            maze[nx][ny] = maze[x][y] + 1
            queue.append((nx, ny))
        }
    }
}
print(maze[n-1][m-1])
```
