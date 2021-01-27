---
title: "알고리즘 기초 - Recursive(5)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/recursive5/
layout: single
---

## Counting cells in a Blob

참고자료: [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/lecture/4076?tab=curriculum)

아래와 같이 Binary이미지가 주어진다. image pixel이거나 background pixel이다. 여기서 서로 연결된 image pixel의 집합을 blob이라고 한다. 상하좌우뿐만 아니라 대각선 방향까지 연결된 것으로 간주한다.

<img width="560" alt="스크린샷 2021-01-27 오후 3 54 14" src="https://user-images.githubusercontent.com/74946802/105954499-15beb200-60b8-11eb-9821-247d885ed935.png">

## Blob의 크기와 수를 계산하기

- 현재 픽셀이 이미지 픽셀이 아니라면 0을 반환
- 현재 픽셀이 이미지 픽셀이라면?
- 현재 픽셀을 카운팅 (count = 1)
- 중복 카운팅 방지를 위해서 visited 표시
- 인접한(상하좌우 및 대각선) 이미지 픽셀의 수만큼 카운팅해주고 visited 표시
- 카운트를 반환

수도 코드는 아래와 같다.

```
if the pixel (x, y) is outside the grid
  the result is 0
else if pixel (x, y) not an image pixel or already counted
  the result is 0
else
  set the colour of the pixel (x, y) to a red(visited) colour
  the result is 1 plus the number of cells in each piece of the blob
    that includes a nearest neighbour
```

## 전체코드

``` swift
let background = 0
let image = 1
let visited = 2
let n = 8
var grid = [[1,0,0,0,0,0,0,1],
            [0,1,1,0,0,1,0,0],
            [1,1,0,0,1,0,1,0],
            [0,0,0,0,0,1,0,0],
            [0,1,0,1,0,1,0,0],
            [0,1,0,1,0,1,0,0],
            [1,0,0,0,1,0,0,1],
            [0,1,1,0,0,1,1,1]]

func countCells(_ x: Int, _ y: Int) -> Int {
    if x<0 || x>=n || y<0 || y>=n {return 0}
    else if (grid[x][y] != image) {return 0}
    else {
        grid[x][y] = visited
        return 1 + countCells(x-1, y+1) + countCells(x, y+1)
        + countCells(x+1, y+1) + countCells(x-1, y)
        + countCells(x+1, y) + countCells(x-1, y-1)
        + countCells(x, y-1) + countCells(x+1, y-1)
    }
}
```
