---
title: "알고리즘 기초 - 탐색&시뮬레이션(6)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search6/
layout: single
---

## 격자판 최대합

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26927?tab=curriculum)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

NxN 격자판이 주어지면 각 행의 합, 각 열의 합, 두 대각선의 합 중 가장 큰 값을 출력하시오.

- 입력예제

5
10 13 10 12 15
12 39 30 23 11
11 25 50 53 15
19 27 29 37 27
19 13 30 13 19

- 출력예제

155

## 내 풀이
``` swift
let n = Int(readLine()!)!
var m = [[Int]]()
for _ in 0..<n {
    m.append(readLine()!.split{$0==" "}.map{Int($0)!})
}
var maxNum = 0
var dia1 = 0
var dia2 = 0

for i in 0..<n {
    var row = 0
    var col = 0
    dia1 += m[i][i]
    if dia1 > maxNum {maxNum =  dia1}
    dia2 += m[i][n-1-i]
    if dia2 > maxNum {maxNum = dia2}
    for j in 0..<n {
        row += m[i][j]
        if row > maxNum {maxNum = row}
        col += m[j][i]
        if col > maxNum {maxNum = col}
    }
}
print(maxNum)
```
이중 for-loop문 안에서 인덱스를 활용하여 각 행의합, 각 열의 합, 두 대각선의 합을 구한다.

좌측상단에서 우측하단으로 내려오는 대각선은 [i][i]인덱스를 가진다. 즉, [0][0], [1][1], [2][2]...과 같은 인덱스를 가진다고 보면된다. 반대로 우측상단에서 좌측하단으로 내려오는 대각선은 같은 형태의 인덱스를 내림차순으로 가진다. 5x5 격자판이라면 [4][4], [3][3], [2][2]...과 같다. 따라서 dia1에 [i][i]값을 저장하고 dia2에 [i][n-1-i]값을 저장하여 maxNum과 비교하여 더 큰 경우에만 값을 대입한다.

j문으로 들어가기 전에 i문에서 row와 col값을 0으로 초기화시켜주는 이유는 모든 행의 합, 모든 열의 합이 아니라 각 행과 각 열의 합을 구해야하기 때문이다. 행의 경우는 [i][j]형태의 인덱스를 가지고, 열의 경우는 [j][i]형태의 인덱스를 가진다. 대각선의 경우와 마찬가지로 maxNum보다 큰 경우에만 값을 대입해주면 된다.

## 강의 풀이

전체적인 풀이로직에서 차이가 없기 때문에 파이썬 코드를 살펴보고 끝내도록 하겠다.

## 파이썬 코드
``` python
n=int(input())
a=[list(map(int, input().split())) for _ in range(n)]
largest = -2147000000
for i in range(n):
    sum1=sum2=0
    for j in range(n):
        sum1+=a[i][j]
        sum2+=a[j][i]
    if sum1>largest:
        largest=sum1
    if sum2>largest:
        largest=sum2
sum1=sum2=0
for i in range(n):
    sum1+=a[i][i]
    sum2+=a[i][n-i-1]
if sum1>largest:
    largest=sum1
if sum2>largest:
    largest=sum2
print(largest)
```
