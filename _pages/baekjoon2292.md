---
title: "백준 2292번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/2292/
layout: single
---

## 벌집

<img width="1164" alt="스크린샷 2021-02-14 오후 3 24 48" src="https://user-images.githubusercontent.com/74946802/107870100-18534100-6ed9-11eb-995c-83a1c491deba.png">
<img width="1164" alt="스크린샷 2021-02-14 오후 3 24 36" src="https://user-images.githubusercontent.com/74946802/107870109-26a15d00-6ed9-11eb-8cbd-cf6b4bcd5228.png">

육각형으로 이루어진 벌집이 주어질 때, 숫자 N이 주어지면 1에서 부터 N까지 최소 몇 개의 방을 지나서 갈 수 있는지 프로그램을 작성하면된다.

## 입력값 저장 및 방 최대값 생성
```swift
let n=Int(readLine()!)!
var a=1
```
특정 숫자 n까지 몇 개의 방을 지나야 하는지 구하는 프로그램을 만들어야 하기 때문에, 상수 n에 입력값을 저장하고 1번 부터 방번호를 시작한다.

## 방최대값 증가 패턴만큼 for-loop
```swift
for i in 1..<n+1 {
    if n==1{print(1);break}
    a+=i*6
    if n <= a {
        print(i+1)
        break
    }
}
```
1부터 n까지 for-loop를 돌면서 방 최대값 a를 6의 배수 단위로 증가시키면서 n이 a에 포함되는지를 탐색한다.

1번 방 이후 2번방에는 6개의 숫자가 포함되고, 3번 방에는 12개의 숫자가 포함되고 이후 6의 배수만큼 방 안에 숫자가 포함된다. 따라서 주어진 숫자 n이 6곱하기 i를 더해준 i방의 최대값인 a보다 작거나 같아지면 i+1을 출력하고 for-loop탐색을 중지한다.

n이 1인 경우는 1을 출력하고 for-loop를 종료하도록 예외처리를 해준다.

## 전체코드
```swift
let n=Int(readLine()!)!
var a=1
for i in 1..<n+1 {
    if n==1{print(1);break}
   a+=i*6
    if n <= a {
        print(i+1)
        break
    }
}
```
