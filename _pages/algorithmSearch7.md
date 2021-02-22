---
title: "알고리즘 기초 - 탐색&시뮬레이션(7)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search7/
layout: single
---
## 사과나무(다이아몬드)

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26928?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

NxN 격자판 모양(N은 항상 홀수)의 과수원의 각 격자에는 사과나무의 수가 적혀져있다. 다이아몬드 모양으로 사과나무를 수확한다고 할 때, 총 수확하는 사과나무의 수를 구하시오.

- 입력예제

5
10 13 10 12 15
12 39 30 23 11
11 25 50 53 15
19 27 29 37 27
19 13 30 13 19

- 출력예제

379

## 내 풀이
``` swift
let n = Int(readLine()!)!
var m = [[Int]]()
for _ in 0..<n {
    m.append(readLine()!.split{$0==" "}.map{Int($0)!})
}
var mid = n/2
var (s, e, i) = (mid, mid, 0)
var sum = 0

while true {
    if s==0 && e==n-1 {break}
    sum += m[i][s...e].reduce(0, +)
    i+=1
    s-=1
    e+=1
}

while true {
    if s==mid && e==mid {break}
    sum += m[i][s...e].reduce(0, +)
    i+=1
    s+=1
    e-=1
}
sum += m[i][s...e].reduce(0, +)
print(sum)
```
s, e포인터와 while-loop를 활용하여 문제를 해결했다. 먼저 시작점과 끝점인 mid값을 n/2를 통해 구해준다. 이후 첫 번째 while-loop는 다이아몬드 모양을 위해 s는 1씩 빼주고, e는 1씩 더해주며 각 구간의 값을 더해준다. s가0, e가 n-1이되면 반대로 s를 1씩 더해주고 e를 1씩 빼줘야하기 때문에 while-loop를 종료한다.

두 번째 while-loop에서는 첫 번째와는 다르게 s를 1씩 더해주고, e를 1씩 빼주면된다. 마찬가지로 s와 e가 모두 mid값에 도달하면 while-loop를 종료해준다. 단, 이렇게 되면 m의 마지박 배열에 [s...e]값이 더해지지 않기 때문에 while-loop를 벗어난 후 해당 값을 더해주고 총 더해준 값을 출력하면 된다.

## 강의 풀이
```swift
let n = Int(readLine()!)!
var m = [[Int]]()
for _ in 0..<n {
    m.append(readLine()!.split{$0==" "}.map{Int($0)!})
}
var res = 0
var (s, e) = (n/2, n/2)
for i in 0..<n {
    for j in s...e {
        res += m[i][j]
    }
    if i<n/2 {
        s-=1
        e+=1
    } else {
        s+=1
        e-=1
    }
}
print(res)
```
강의풀이에서는 loop를 둘로 나누지 않고 이중loop를 활용하여 문제를 해결했다. 조금 더 탐색이라는 취지에 잘 맞는 풀이였던 것 같다. 전체적인 풀이로직은 다르지 않지만 구간의 값을 reduce로 더해서 sum에 더해줬던 내 풀이와는 다르게, 강의 풀이에서는 s부터 e까지 구간을 탐색하면서 하나씩 숫자를 더해줬다. i값을 기준으로 s,e포인터의 값을 더해줄지 빼줄지를 정한 것도 내가 생각하지 못했던 부분이라 참고가 많이 됐다.

## 파이썬 코드
``` python
n=int(input())
a=[list(map(int, input().split())) for _ in range(n)]
res=0
s=e=n//2
for i in range(n):
    for j in range(s, e+1):
        res+=a[i][j]
    if i<n//2:
        s-=1
        e+=1
    else:
        s+=1
        e-=1
print(res)
```
