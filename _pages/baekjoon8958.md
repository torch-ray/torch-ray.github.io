---
title: "백준 8958번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/8958/
layout: single
---

## 백준 - OX퀴즈

<img width="1171" alt="스크린샷 2021-01-19 오전 8 31 40" src="https://user-images.githubusercontent.com/74946802/104971096-06dd5d00-5a31-11eb-8532-691bd02c849c.png">

테스트 케이스의 숫자와 "OOXXOXXOOO" 형태로 문자열이 주여지면 O의 수를 카운팅하여 더해주면 되는 문제다. 단, O가 연속으로 등장하는 경우에는 추가 점수가 주어진다. 예를 들면 "O(1)"는 1점이지만 "OOO(123)"의 마지막 O는 3점이다. "OOXXO(12- -1)"와 같이 X가 등장하는 경우에는 O의 점수가 초기화된다.

- 체크포인트: 연속된 숫자의 합을 구하는 공식

## 값을 저장할 sum과 연속된 수를 카운팅할 count변수 생성

``` swift
let n = Int(readLine!)!
for _ in 0..<n {
  var(s, c) = (0, 0)
  let m = readLine()!
}
```
상수 n을 선언하여 테스트케이스의 숫자를 입력받고, 테스트케이스만큼 문자열을 입력받기 위해 n만큼 for문을 반복한다. 최종 값을 저장할 sum과 count변수를 for문 안에 선언한 이유는 매 문자열마다 0으로 값을 초기화하지 않으면 이전 문자열 값이 중복되어 더해지기 때문이다.

## 문자열을 for문으로 돌면서 "O"의 수를 카운팅

``` swift
for j in m {
  if j == "0" {
    s += c + 1
    c += 1
  } else {
    c = 0
  }
}
print(s)
}
```
주어진 문자열 m을 for문으로 탐색하면서 "O"를 찾아주고 "O"가 등장할 때 마다 sum변수에 count값과 1을 더해준다. 이어서 "O"가 연속해서 등장할 경우를 대비하여 count변수 값도 1을 더해준다. 예를들면 "O"가 처음 등장한 경우에는 c=0, s=0 이기 때문에 s에 1(0+1)을 더해주고 c에 1을 더해준다. 또 "O"가 등장한다면 현재 상황은 c=1, sum=1이기 때문에 1을 가지고 있는 s에 2(1+1)를 더해줘서 s=3이된다. 반대로 "X"가 등장하는 경우에는 c를 0으로 초괴화시켜서 연속된 값이 더해지지 않도록 해준다.

## 전체코드

``` swift
let n = Int(readLine()!)!
for _ in 0..<n {
    var (s, c) = (0, 0)
    let m = readLine()!
    for j in m {
        if j == "O" {
            s += c+1
            c += 1
        } else {
            c = 0
        }
    }
    print(s)
}
```

## 가우스의 덧셈

사실 이 문제를 읽고 연속된 수의 합을 구하시오. 라는 문구를 떠올릴 수 있었다면 위와 같이 코딩하지 않고 간단하게 풀 수 있는 문제다. 1부터 100까지를 모두 더하라는 문제를 받은 초등학생 가우스는 친구들이 힘들게 덧셈을 하고 있을 때, 짧은 시간만에 문제를 해결했다고 한다. 그 원리는 다음과 같다. 먼저 1에서 부터 100까지 적은 다음 그 밑에 100에서 부터 1까지 거꾸로 적는 것이다. 그리고 덧셈을 해주면 1 + 100 = 101, 2 + 99 = 101, 3 + 98 = 101과 같이 101이 100번 나오게된다. 하지만 이는 1부터 100까지를 두 번 더한셈이 되기 때문에, 이를 2로 나누어주면 1부터 100까지의 총합인 5050이 되는 것이다. 이러한 발견을 일반화하여 만든 공식은 n(n+1)/2의 형태로 나타난다.

## 가우스의 덧셈을 활용한 코드

``` swift
let n = Int(readLine()!)!
for _ in 0..<n {
  print(readLine()!.split{$0=="X"}.map{$0.count*($0.count+1)/2}.reduce(0, +))
}
```

split을 활용하여 "X"를 기준으로 문자열을 나눈다. 예를들면 문자열 "OXOOXOOOO"는 "O OO OOOO"와 같이 입력된다. map을 통해 첫번째 문자열의 수를 count하고 그 수에 1을 더해 곱한 뒤 2로 나누어준다(가우스의 덧셈). 이해하기 쉽게 표현하자면 "OXOOXOOOO"는 "1 12 1234"이기 때문에 연속된 수의 합을 구하면 [1, 3, 10]이 된다는 의미다. 그리고 이를 reduce를 통해 모두 더해주면 14가 된다.
