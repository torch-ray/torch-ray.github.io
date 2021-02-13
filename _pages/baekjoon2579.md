---
title: "백준 2579번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/2579/
layout: single
---

## 계단 오르기

<img width="1164" alt="스크린샷 2021-02-13 오전 8 50 52" src="https://user-images.githubusercontent.com/74946802/107834196-ece92d00-6dd8-11eb-999f-e6883bd84e95.png">
<img width="1164" alt="스크린샷 2021-02-13 오전 8 50 42" src="https://user-images.githubusercontent.com/74946802/107834180-e064d480-6dd8-11eb-808c-e5aa3cf017f6.png">
<img width="1164" alt="스크린샷 2021-02-13 오전 8 50 33" src="https://user-images.githubusercontent.com/74946802/107834162-d5aa3f80-6dd8-11eb-9893-0f981b0b9f08.png">
<img width="1164" alt="스크린샷 2021-02-13 오전 8 50 24" src="https://user-images.githubusercontent.com/74946802/107834144-c7f4ba00-6dd8-11eb-9f34-3d7517b7fd0d.png">

각 계단에 숫자가 적혀있고 계단을 밟아 맨 위로 올라간다고 할 때, 밟은 계단에 적힌 수의 합이 가장 큰 경우를 출력하면 된다.

제한사항은 다음과 같다.

(1). 계단은 한 번에 한 계단 또는 두 계단씩만 오를 수 있다.

(2). 연속된 세 개의 계단을 모두 밟아서는 안 된다. 단, 시작점(즉 첫 번째 계단 전)은 계단에 포함되지 않는다.

(3). 마지막 계단은 반드시 밟아야 한다.

## 입력값 저장 및 DP배열 생성
```swift
let n=Int(readLine()!)!
var dp1=[Int](repeating: 0, count: n), dp2=dp1
```
계단의 숫자를 상수 n에 저장하고, dp1, dp2 배열을 생성한다. 전 계단을 밟은 경우와, 밟지 않은 경우를 나눠서 저장해야 하기 때문에, 두 개의 배열이 필요하다.

## DP를 활용하여 최대값 비교
```swift
for i in 0..<n {
    let m=Int(readLine()!)!

    if i-1>=0 {dp1[i] = dp2[i-1] + m}
    else {dp1[i]=m}

    if i-2>=0 {dp2[i] = max(dp1[i-2], dp2[i-2]) + m}
    else {dp2[i]=m}
}
print(max(dp1[n-1], dp2[n-1]))
```
n만큼 for-loop를 돌면서 각 계단에 적힌 숫자를 dp1과 dp2배열에 더해준다. dp1은 바로 직전 계단을 밟은 경우이며, dp2는 전 계단을 밟지 않은 경우이다.

따라서 dp1에는 i가 0인 경우만 else문이 돌면서 현재 계단 값을 그대로 더해준다. 쉽게 말하자면 첫번째 계단 값만 그대로 더해준다. 첫번째 계단에서 부터는 dp2에 i-1에 저장된 값에 현재값을 더한 값을 더해준다. 이는 현재 계단을 밟기 위해서는 전전 계단을 밟지않았다는 전제조건이 필요하기 때문이다.

dp2는 i가 0과 1인 경우만 else문이 돌면서 현재 계단 값을 그대로 더해준다. 전 계단을 밟지 않은 경우의 최대값이기 때문에 첫 번째 계단과 두 번째 계단은 어떠한 값도 더해지지 않는다. 그 이후부터는 dp1[i-2]값과, dp2[i-2] + m값 중 더 큰값을 더해준다. i-2의 값을 기준으로 비교하는 이유는 연속해서 세 계단을 밟지 않아야 한다는 제한조건을 고려 했기 때문이다.

이렇게 계산을 한 후에, dp1과 dp2의 마지막 값중 더 큰 값을 출력하면된다.

## 전체코드
```swift
let n=Int(readLine()!)!
var dp1=[Int](repeating: 0, count: n), dp2=dp1
for i in 0..<n {
    let m=Int(readLine()!)!

    if i-1>=0 {dp1[i] = dp2[i-1] + m}
    else {dp1[i]=m}

    if i-2>=0 {dp2[i] = max(dp1[i-2], dp2[i-2]) + m}
    else {dp2[i]=m}
}
print(max(dp1[n-1], dp2[n-1]))
```
