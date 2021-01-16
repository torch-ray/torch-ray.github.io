---
title: "백준 2839번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/2839/
layout: single
---

## 백준 - 설탕배달

<img width="1157" alt="스크린샷 2021-01-16 오전 11 40 05" src="https://user-images.githubusercontent.com/74946802/104795162-a01d3100-57ef-11eb-83d9-89aefa51e9b5.png">

설탕 Nkg이 주어지면 3kg 봉지와 5kg 봉지를 활용하여 Nkg를 모두 담을 수 있는 가장 적은 봉지의 수를 구하는 문제이다. 예를들면 18kg은 3kg봉지 6개로도 가능하지만, 5kg 3개 3kg 1개로 포장할 경우 4개로도 가능하기 때문에 답은 4개이다. 정확히 Nkg을 모두 포장하여야 하며 불가능할 경우 -1을 출력하면 된다. 즉, 4kg은 3과 5를 활용하여 0을 만들 수 없기 때문에 -1이 답이된다.

- 체크포인트: 가장 적은 봉지의 수를 출력해야하기 때문에 5kg으로 나누는 수가 답이된다.

## Count 변수 선언

``` swift
var n = Int(readLine()!)!
var c = 0
```
readLine()함수를 통해 받는 값은 Optional String 값으로 반드시 Int() 및 !를 활용하여 정수로 만들어줘야한다. 추가적으로 default값인 5kg이 아닌 3kg을 빼줄 경우를 카운트하기 위해 c변수를 선언한다.

## While 반복문 활용

``` swift
while true {
  if n % 5 == 0 {
    c += n/5
    print(c)
    break
  }
  n -= 3
  c += 1
  if n < 0 {
    print(-1)
    break
  }
}
```
일단 주어진 수가 5로 나눠서 떨어질 경우에는 해당 수를 5로 나눈 몫을 출력하고 while문을 종료하면된다. 해당 수가 3으로 나눠서도 나머지가 0이된다고 하더라도 그 몫이 5가 더 적을 수밖에 없기 때문이다(예를들면 15의 경우 5로 나눈 몫은 3, 3으로 나눈 몫은 5이기 때문에 5로 나눈 몫인 3이 정답이다). 5로 나눈 나머지가 0이 되지 않을 경우에는 n값에서 3을 빼주고 3을 빼줄때마다 count수를 올린다. 3을 빼주다가 해당 수를 5로 나눈 나머지가 0이되면 3을 빼줄때 마다 올렸던 count수와 5로 나눈 몫을 더해서 출력하면된다. 하지만 n이 0보다 작아질 때까지 if n % 5 == 0 코드가 실행되지 않았다면 해당 수는 3과 5로 0을 만들 수 없는 수이기 때문에 -1을 출력한다.

## 전체코드

``` swift
var n = Int(readLine()!)!
var c = 0
while true {
    if n%5 == 0 {
        c += n/5
        print(c)
        break
    }
    n -= 3
    c += 1
    if n < 0 {
        print(-1)
        break
    }
}
```
