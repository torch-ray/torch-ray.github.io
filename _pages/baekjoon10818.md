---
title: "백준 10818번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/10818/
layout: single
---

## 백준 - 최소, 최대

<img width="1173" alt="스크린샷 2021-01-18 오전 7 35 21" src="https://user-images.githubusercontent.com/74946802/104858073-1e004a00-5960-11eb-8a55-fd144f587048.png">

문제가 어렵지는 않다. N개의 정수가 주어지면 그 중 최소값, 최대값을 구해 출력하는 문제다. 주어지는 정수의 범위는 -1,000,000 이상 1,000,000이하

- 체크포인트: readLine(map)에서 시간초과가 발생한다.

## 시간초과 발생

본 문제는 사실 문제 해결에는 큰 어려움이 없다. 다만, 시간초과가 발생하는데 이 부분을 해결해줘야 한다. 첫번째로 작성해서 시간초과가 발생한 코드는 아래와 같다. 두 코드 모두 시간초과가 발생했다.
``` swift
readLine()
let m = readLine()!.split{$0==" "}.map{Int($0)!}.sorted()
print(m.first!, m.last!)
```
``` swift
readLine()
let m = readLine()!.split{$0==" "}.map{Int($0)!}
print(m.min()!, m.max()!)
```

## 정수 범위 활용
``` swift
readLine()
let a=readLine()!.split(separator: " ").map{Int($0)!}
var (n,m)=(1000000, -1000000)

for i in a {
    if n>i {n=i}
    if m<i {m=i}
}

print(n, m)
```
문제를 다시 읽어보니 정수 범위가 -1,000,000부터 1,000,000까지로 주어져 있어서 해당 정수 범위를 활용하여 코드를 작성해서 출력해봤다. 하지만 여전히 시간초과가 발생했다.

## 문제는 Map(Int vs Int(String))

문제 없이 통과한 코드는 아래와 같다. 아래 두 코드 모두 통과한 것으로 보아 정수 범위 활용과 문제 해결에는 큰 연관성이 없다.
``` swift
readLine()
let a=readLine()!.split(separator: " ").map{Int(String($0))!}
print(a.min()!, a.max()!)
```
``` swift
readLine()
let a=readLine()!.split(separator: " ").map{Int(String($0))!}
var (n,m)=(1000000, -1000000)

for i in a {
    if n>i {n = i}
    if m<i {m=i}
}

print(n, m)
```

아래 두 코드는 위 코드에서 Map의 String변경 부분을 제외한 코드, 다시 시간초과가 발생했다.

``` swift
readLine()
let a=readLine()!.split{$0==" "}.map{Int($0)!}
print(a.min()!,a.max()!)
```
``` swift
readLine()
let a=readLine()!.split(separator: " ").map{Int($0)!}
var (n,m)=(1000000, -1000000)

for i in a {
    if n>i {n = i}
    if m<i {m=i}
}

print(n, m)
```

결국 map{Int($0)!} vs map{Int(String($0))!}에서 후자가 승리한 것인데, 해당 부분이 아직 이해되지 않는다. 어떤 메카니즘으로 전자는 시간초과가 되고 후자는 통과 할 수 있는지 학습 후에 관련 내용을 재업로드할 예정이다.
