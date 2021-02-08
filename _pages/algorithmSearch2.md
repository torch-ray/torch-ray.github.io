---
title: "알고리즘 기초 - 탐색&시뮬레이션(2)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search2/
layout: single
---

## 숫자만 추출

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26923?tab=curriculum)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

문자와 숫자가 섞여있는 문자열이 주어지면 그 중 숫자만 추출하여 그 순서대로 자연수를 만들어 출력하시오. 0, 0, 1, 2, 0의 경우라면 120이 된다. 첫번째 줄에는 자연수, 두 번째 줄에는 자연수의 약수의 개수를 출력하시오.

- 입력예제

g0en2Ts8eSoft

- 출력예제

28  
6

## 내 풀이
``` swift
let n = readLine()!
var m = ""
for i in n {
    if i.isNumber {
        m += String(i)
    }
}
let a = Int(m)!
var cnt = 0
for i in 1...a {
    if a%i == 0 {
        cnt+=1
    }
}
print(a)
print(cnt)
```
문자열을 입력받아서 상수 n에 저장하고 숫자만 저장할 변수 m을 생성한다. 그 후 n을 for-loop로 탐색하면서 isNumber를 활용하여 숫자인 경우에 m에 저장한다. 그 후 m을 정수로 변환하여 a에 저장하고 for-loop를 1부터 돌면서 a의 약수를 찾아서 약수일 때마다 cnt값을 1씩 증가해준다. 이 후 a와 cnt를 출력한다.

## 강의 풀이
``` swift
let s = readLine()!
var res = 0
for x in s {
    if x.isNumber {
        res = res * 10 + Int(String(x))!
    }
}
print(res)
var cnt = 0
for i in 1...res {
    if res%i == 0 {
        cnt+=1
    }
}
print(cnt)
```
전체적인 풀이 로직은 다르지 않다. 다만 숫자로 이루어진 문자열을 정수로 변환할 때 함수를 사용하여 한 번에 변환하지 않고, 계산식을 활용하였다. 0, 2, 8로 예를들면, 0에 10을 곱하고 0을 더해봤자 0이기 때문에 0은 자동으로 생략된다. 2의 경우 0곱하기 10 더하기 2가되기 때문에 2가 저장이되고, 8의 경우 2곱하기 10 더하기 8이기 때문에 28이 저장된다. 이후 풀이과정은 내 풀이와 같다.

## 파이썬 코드
``` python
s=input()
res=0
for x in s:
    if x.isdecimal():
        res = res * 10 + int(x)
print(res)
cnt=0
for i in range(1, res+1):
    if res%i==0:
        cnt+=1
print(cnt)
```
