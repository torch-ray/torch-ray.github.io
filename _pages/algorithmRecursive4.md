---
title: "알고리즘 기초 - Recursive(4)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/recursive4/
layout: single
---

## 미로찾기

참고자료: [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/lecture/4075?tab=curriculum)

아래 그림은 N x N 형태의 미로이다. 노란색에서 출발하여 파란색까지 도달하는 경로를 Recursion을 통해 구하려고한다. 빨간색은 벽으로 통과할 수 없고 검은색이 통과할 수 있는 길이다.

<img width="902" alt="스크린샷 2021-01-26 오후 10 52 05" src="https://user-images.githubusercontent.com/74946802/105853517-24aa5380-6029-11eb-8061-d1a36d119beb.png">

현재 위치에서 출구까지 도착하려면 (1). 현재 위치가 출구이거나, (2). 이웃한 셀 중 하나에서 현재 위치를 다시 지나지 않고 출구까지 갈 수 있는 경로일 때다. 해당 아이디어를 바탕으로 코드를 설계해보면 아래와 같다.

- Decision Problem(true or false 문제)

현재 위치 (x, y)가 출구라면 true를 반환한다. 그렇지 않다면 for-loop를 활용하여 인접한 셀을 모두 확인한다. 인접한 셀이 벽이 아닌 통과할 수 있는 길이라면 재귀함수를 호출하고, 해당 값이 true를 반환하면 true를 반환하고 함수를 종료한다. 만약 인접한 셀이 모두 벽이거나 인접한 셀을 통하여 출구를 찾을 수 없는 경우에는 false를 반환하면 된다. 이 경우에는 출구를 찾을 수 없는 것이다.

하지만 이 코드는 무한루프에 빠질 가능성이 있다. 인접한 셀을 탐색한다고 가정할 때 '현재 위치를 다시 지나지 않고' 라는 부분을 간과한 것이다. 즉, (x, y)에서 (x', y')로 이동 했을 때 (x', y')의 인접한 셀이 다시 (x, y)가 된다는 것이다. 따라서 방문한 적이 있는 위치는 탐색하지 않고 건너뛰어야한다. 또는 건너뛰지 않고 해당 셀의 좌표를 재귀함수로 호출하고 재귀함수 첫줄에서 길이아니거나 방문한적이 있으면 바로 false를 반환해도 문제없다. 물론 이 경우에는 재귀함수가 더 많이 호출되지만, 코드 자체는 간결해진다. 최종적인 수도코드는 아래와 같다.

```
boolean findPath(x, y)
  if (x, y) is either on the wall or a visited cell
    return false;
  else if (x, y) is the exit
    return true
  else
    mark(x, y) as a visited cell;
    for each neighbouring cell (x', y') of (x, y) do
      if findPath(x', y')
        return true;
    return false;
```

## 미로찾기 with swift

``` swift
let n = 8
var maze = [[0,0,0,0,0,0,0,1],
            [0,1,1,0,1,1,0,1],
            [0,0,0,1,0,0,0,1],
            [0,1,0,0,1,1,0,0],
            [0,1,1,1,0,0,1,1],
            [0,1,0,0,0,1,0,1],
            [0,0,0,1,0,0,0,1],
            [0,1,1,1,0,1,0,0]]

let pathway = 0 // 갈 수 있는 길
let wall = 1 // 벽으로 막힌 곳
let blocked = 2 // 가봤는데 막힌 길
let visitied = 3 // 가보긴 했는데 출구로 이어지는지는 모르는 길
```

주어진 Maze 변수는 8 X 8 형태의 미로이며, 0부터 7까지의 좌표로 구성되어 있기 때문에 (7, 7) 지점이 탈출구이다. 아래 코드를 통해 탈출 여부 및 경로를 알 수 있다.

``` swift
func findMazePath(_ x: Int, _ y: Int) -> Bool {
    if x<0 || y<0 || x>=n || y>=n {return false}
    else if (maze[x][y] != pathway) {return false}
    else if (x==n-1 && y==n-1) {
        maze[x][y] = visitied
        return true
    }
    else {
        maze[x][y] = visitied
        if findMazePath(x-1, y) || findMazePath(x, y+1)
        || findMazePath(x+1, y) || findMazePath(x, y-1) {
            return true
        }
        maze[x][y] = blocked
        return false
    }
}

func solution() {
    print(maze)
    findMazePath(0, 0)
    print(maze)
}
```

먼저 좌표 x, y가 0보다 작거나 8보다 큰 경우는 주어진 미로를 벗어나는 것이기 때문에 false를 반환한다. 마찬가지로 주어진 좌표가 갈 수 있는 길이 아닐 때도 false를 반환한다. 그리고 (7, 7)에 도착했을 때는 방문표시를 한 뒤에 true를 반환한다. else 부분 코드는 앞서 언급한 false조건에 해당되지 않고, 탈출 좌표가 아닐 경우에 실행된다. 현재 위치를 visited로 체크하고 북, 동, 남, 서 순서로 재귀함수를 호출한다. true가 반환되지 않으면 막힌길에 빠졌다는 뜻이기 때문에 blocked 처리한다.
