---
title: "알고리즘 기초 - 코드 구현력 기르기(10)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation10/
layout: single
---

## 주사위 게임

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26921?tab=curriculum)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

1~6까지의 눈을 가진 주사위 3개를 던져 나온 값을 바탕으로 상금을 계산하시오. (1). 같은 눈이 3개나오면 10,000원 + (같은눈) * 1,000원, (2). 같은 눈이 2개나오면 1,000원 + (같은눈) * 100원, (3). 모두 다른 눈이 나오면 (가장 큰 눈) * 100원을 받게된다. N명이 각각 3개의 주사위를 던질 때, 가장 큰 상금을 출력하시오.

- 입력예제

3 (N명의 참여자)    
3 3 6 (3개의 주사위를 던진 눈)   
2 2 2  
6 2 5  

- 출력예제

12000 (가장 큰 상금)

## 내 풀이
``` swift
let n = Int(readLine()!)!
var res = [Int]()
for _ in 0..<n {
    var m = readLine()!.split{$0==" "}.map{Int($0)!}
    let tmp = Set(m)
    if tmp.count == 1 {
        res.append(10000 + m[0]*1000)
    }
    else if tmp.count == 3 {
        res.append(m.max()! * 100)
    } else {
        for i in tmp {
            m.remove(at: m.firstIndex(of: i)!)
        }
        res.append(1000 + m[0]*100)
    }
}
print(res.max()!)
```
set을 활용하여 문제를 해결했다. set의 count가 1이라면 모두 같은 눈이 나왔기 때문에, 해당 값에 1,000원을 곱한뒤에 10,000원을 더하여 정수행 배열 res에 저장했다. set의 count가 3이라면 모두 다른 값이라는 의미로, max값을 뽑아서 100원을 곱한 뒤에 저장했다. 마지막으로 count가 2인 경우에는 2개는 같은 값, 1개는 다른값이므로, for-loop로 set을 탐색한 값을 처음 입력을 받은 m배열에서 제거했다. 그렇게되면 세 값 중 두개가 제거되고, 두개의 같은 값 중 나머지 하나만 남게된다. 그 값에 100원을 곱하고 1,000원을 더해주고 max를 활용하여 최대 상금을 출력하면된다.

## 강의 풀이
``` swift
let n = Int(readLine()!)!
var res = 0
for _ in 0..<n {
    let tmp = readLine()!.split{$0==" "}.map{Int($0)!}.sorted()
    let (a, b, c) = (tmp[0], tmp[1], tmp[2])

    var money = 0
    if a==b && a==c {
        money = 10000 + a * 1000
    } else if a==b || a==c {
        money = 1000 + a * 100
    } else if b==c {
        money = 1000 + b * 100
    } else {
        money = c * 100
    }
    if money > res {
        res = money
    }
}
print(res)
```
각 눈의 값을 a, b, c 상수에 별도로 저장하여 if문으로만 문제를 해결했다. 코드 가독성이나 시간복잡도 측면에서 훨씬 뛰어난 코드였다. 주사위의 눈이 주어지면 정렬을 한 뒤에 각 값을 a, b, c에 저장한다. 그리고 모두 같은 경우, 두개만 같은 경우, 모두 다른 경우를 if문으로만 해결하면 된다. 두개의 눈이 같고 하나의 눈만 다를 경우에는 else if문을 두 번 활용하여 둘 중에 하나에 충족되도록 설계했다. 모두 다른 경우에는 눈이 정렬되어 있기 때문에 별도로 max함수를 활용하지 않고 그냥 c값에 100원을 곱해주면 된다.

## 파이썬 코드
``` python
n=int(input())
res=0
for i in range(n):
    tmp = input().split()
    tmp.sort()
    a, b, c = map(int, tmp)
    if a==b and b==c:
        money = 10000 + a * 1000
    elif a==b or a==c:
        money = 1000 + a * 100
    elif b==c:
        money = 1000 + b * 100
    else:
        money = c * 100
    if money>res:
        res=money
print(res)
```
