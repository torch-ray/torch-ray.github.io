---
title: "백준 2667번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/2667/
layout: single
---

## 백준 - 단지번호붙이기

<img width="1143" alt="스크린샷 2021-02-03 오전 9 31 30" src="https://user-images.githubusercontent.com/74946802/106680946-d71e7f80-6602-11eb-86ac-b1be6fa97d8a.png">
<img width="1143" alt="스크린샷 2021-02-03 오전 9 31 38" src="https://user-images.githubusercontent.com/74946802/106680968-e1d91480-6602-11eb-8eab-50973db02314.png">

대각선을 제외하고 상하좌우로 1이 붙어있을 경우 아파트 단지를 형성한다. NxN 지도가 주어질 때, 해당 지도 안에 존재하는 단지의 수와 각 단지별 가구의 수(즉, 붙어있는 1의 개수)를 출력하면된다.

## 지도의 크기 및 아파트 정보 입력
``` swift
let n=Int(readLine()!)!
var apart=[[Int]]()
var cnt=0
var res=[Int]()
for _ in 0..<n {
    apart.append(readLine()!.map{Int(String($0))!})
}
```
상수 n에 지도의 크기를 입력받는다. 변수 apart는 아파트 단지 정보를 입력받을 변수이고, for-loop를 통해 정수형 배열을 입력받아서 저장한다. cnt값은 단지 내에 가구가 몇개나 존재하는지 카운팅할 변수이고, res는 단지별 cnt정보를 저장할 변수이다.

## 단지별 탐색함수
``` swift
func dxdy(_ x:Int, _ y:Int) -> Bool{
    if x<0 || y<0 || x>=n || y>=n {
        return false
    }
    if apart[x][y]==1 {
        apart[x][y]=2
        cnt+=1
        dxdy(x+1, y)
        dxdy(x-1, y)
        dxdy(x, y+1)
        dxdy(x, y-1)
        return true
    }
    return false
}
```
좌표를 입력받으면 아파트 단지를 탐색할 함수를 생성한다. 좌표가 0보다 작거나 n보다 크거나 같다면 지도의 범위를 벗어나는 것이기 때문에 false를 반환하면된다. 지도의 좌표가 1이라면 가구가 존재한다는 뜻이기 때문에 해당 좌표를 2로 바꾸고(중복방지를 위한 방문표시), cnt값을 올려준 뒤에 상하좌우로 재귀함수 탐색하고 true를 반환한다. 가구가 존재하는 경우(좌표의 값이 1인경우)만 탐색이 필요하기 때문에 해당 조건에 걸리지 않았다면 false를 반환한다.

## 모든 좌표 탐색
``` swift
for i in 0..<n {
    for j in 0..<n {
        cnt=0
        if dxdy(i, j) {
            res.append(cnt)
        }
    }
}
```
1이 연결되어 있는 미로탐색이 아니라, 각 단지마다 0으로 끊겨있기 때문에 모든 좌표를 탐색하기 위해 NxN에서 모두 함수를 실행해본다. 함수 실행 전 cnt값을 초기화 시켜야 단지별로 가구의 수가 중복되지 않는다. true를 반환한 경우 해당 시점의 cnt값을 res에 저장한다.

## 정렬 및 출력
``` swift
res.sort()
print(res.count)
res.forEach{
    print($0)
}
```
오름차순 정렬하여 출력하는 것이 조건이었기 때문에 정렬을 해주고, res의 수와 각 단지별 가구수를 출력한다.

## 전체코드
``` swift
let n=Int(readLine()!)!
var apart=[[Int]]()
var cnt=0
var res=[Int]()
for _ in 0..<n {
    apart.append(readLine()!.map{Int(String($0))!})
}

func dxdy(_ x:Int, _ y:Int) -> Bool{
    if x<0 || y<0 || x>=n || y>=n {
        return false
    }
    if apart[x][y]==1 {
        apart[x][y]=2
        cnt+=1
        dxdy(x+1, y)
        dxdy(x-1, y)
        dxdy(x, y+1)
        dxdy(x, y-1)
        return true
    }
    return false
}

for i in 0..<n {
    for j in 0..<n {
        cnt=0
        if dxdy(i, j) {
            res.append(cnt)
        }
    }
}
res.sort()
print(res.count)
res.forEach{
    print($0)
}
```
