---
title: "백준 1076번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/1076/
layout: single
---

## 백준 - 저항

<img width="673" alt="스크린샷 2021-01-12 오전 9 02 32" src="https://user-images.githubusercontent.com/74946802/104252258-f66b3680-54b4-11eb-954d-f26131cb916b.png">

주어진 세가지 색의 값과 곱을 활용하여 저항을 구하는 문제다. 예를들어 yellow, violet, red가 주어진다면 처음 두 색 yellow(4)와 violet(7)의 값을 가져온 후 마지막 색인 red(100)의 곱을 가져와 곱해주면 된다. (답은 47 * 100 = 4700)
- 체크포인트: 인덱스를 활용한다.

## 모든 색을 담고있는 배열을 생성
``` swift
let color = ["black", "brown", "red", "orange", "yellow",
"green", "blue", "violet", "grey", "white"]
```
문제에서 주어진 각 색이 가진 값은 인덱스 순서와 같다. 또한 각 색이 가진 곱의 값도 10^인덱스(10의 인덱스제곱)과 같다. 즉, 해당 문제는 인덱스를 활용하여 풀이가 가능하다. 따라서 color배열에 반드시 순서대로 입력해줘야 한다.

## 입력값을 받아서 배열에 저장
``` swift
var result = [String]()
for idx in 0..<3 {
  let input = readLine()
  result.append(input)
}
```
경우에 따라 입력되는 색깔의 수가 달라지는 것이 아니라, 무조건 3가지 색깔이 입력값으로 들어오기때문에 반복문은 3번만 돌면된다. readLine()으로 입력받은 값은 result 배열에 저장한다.

## 색깔별로 상수 선언
``` swift
let a = color.index(of: result[0])!
let b = color.index(of: result[1])!
let c = color.index(of: result[2])!
```
순서대로 result배열에 append했기 때문에, [0]이 첫번째 색, [1]이 두번째 색, [2]가 세번째 색이다. 각 색의 인덱스를 불러온다.

## 값과 곱을 연산하여 출력
``` swift
let sol = (a * 10 + b) * Int(pow(10, Double(c)))
print(sol)
```
첫번째색(a)과 두번째(b)색을 붙여준다. 이때 유의해야할 점은 각 값을 더하는게 아니라 붙여준다는 것이다. yellow와 violet의 인덱스 값인 4와 7의 경우 11이 아니라 47로 만들어줘야한다. 따라서 첫번째색의 값에 10을 곱해준 후에 더하면 40 + 7 = 47이 된다. 이제 세번째색인 red의 인덱스 값인 2를 10의 지수로 넣어주면 10^2 = 100으로 곱의 값 호출이 완료된다. 이제 47와 100을 곱해준 후에 출력하면 완료

## 전체코드
<img width="758" alt="스크린샷 2021-01-12 오전 9 25 53" src="https://user-images.githubusercontent.com/74946802/104253596-3849ac00-54b8-11eb-9a7e-cf45dd910ab4.png">
