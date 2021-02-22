---
title: "알고리즘 기초 - 탐색&시뮬레이션(8)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search8/
layout: single
---
## 곳감(모래시계)

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/27683?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

NxN 격자판 모양(N은 항상 홀수)의 마당의 각 격자에는 곳감의 수가 적혀져있다. 그런데 해의 위치에 따라 특정 감은 잘 마르지 않는다. 따라서 회전명령 정보가 [2, 0, 3]과 같이 주어지면 2번째 행을 왼쪽으로 3번 회전시킨다. 첫번째 수는 행의 번호, 두 번째수는 0이면 왼쪽, 1이면 오른쪽이고, 세 번째 수는 회전희 횟수를 의미한다. M개의 회전 명령을 수행한 후 마당의 모래시계 영역에 있는 곳감의 수를 출력하는 프로그램을 작성하세요.

- 입력예제

5 (N)  
10 13 10 12 15
12 39 30 23 11
11 25 50 53 15
19 27 29 37 27
19 13 30 13 19
3 (M)  
2 0 3
5 1 2
3 1 4

- 출력예제

362

## 내 풀이
``` swift
let n = Int(readLine()!)!
var m = [[Int]]()
for _ in 0..<n {
    m.append(readLine()!.split{$0==" "}.map{Int($0)!})
}
let a = Int(readLine()!)!
var b = [[Int]]()
for i in 0..<a {
    b.append(readLine()!.split{$0==" "}.map{Int($0)!})
    for _ in 0..<b[i][2] {
        if b[i][1] == 0 {
            m[b[i][0]-1].append(m[b[i][0]-1].removeFirst())
        } else {
            m[b[i][0]-1].insert(m[b[i][0]-1].removeLast(), at: 0)
        }
    }
}

var(s, e) = (0, n-1)
var sum = 0

for i in 0..<n {
    for j in s...e {
        sum += m[i][j]
    }
    if i < n/2 {
        s+=1
        e-=1
    } else {
        s-=1
        e+=1
    }
}

print(sum)
```
지난 문제인 사과나무(다이아몬드)와 전체적인 풀이로직은 다르지 않기 때문에 풀이과정 설명은 생략한다. 단, 회전의 경우에는 for-loop를 회전 정보의 세 번째 수만큼 돌면서 두 번째 수가 0인 경우에는 m.append(m.removeFirst())를 하였고, 두 번째 수가 1인 경우에는 m.insert(m.removeLast(), at:0)을 하였다. 이렇게 코드를 설계하면 전자는 왼쪽으로 회전하는 결과와 같고 후자는 오른쪽으로 회전하는 결과와 같다.

## 강의 풀이
```swift
let n = Int(readLine()!)!
var a = [[Int]]()
for _ in 0..<n {
    a.append(readLine()!.split{$0==" "}.map{Int($0)!})
}
let m = Int(readLine()!)!
for _ in 0..<m {
    let input = readLine()!.split{$0==" "}.map{Int($0)!}
    let (h, t, k) = (input[0], input[1], input[2])
    if t==0 {
        for _ in 0..<k {
            a[h-1].append(a[h-1].removeFirst())
        }
    } else {
        for _ in 0..<k {
            a[h-1].insert(a[h-1].removeLast(), at: 0)
        }
    }
}


var(s, e) = (0, n-1)
var res = 0

for i in 0..<n {
    for j in s...e {
        res += a[i][j]
    }
    if i < n/2 {
        s+=1
        e-=1
    } else {
        s-=1
        e+=1
    }
}

print(res)

```
전체적인 풀이로직이 같기 때문에 별도 설명은 생략한다.

## 파이썬 코드
``` python
n=int(input())
a=[list(map(int, input().split())) for _ in range(n)]
m=int(input())
for i in range(m):
    h, t, k=map(int, input().split())
    if t == 0:
        for _ in range(k):
            a[h-1].append(a[h-1].pop(0))
    else:
        for _ in range(k):
            a[h-1].insert(0, a[h-1].pop())
res=0
s=0
e=n-1
for i in range(n):
    for j in range(s, e+1):
        res+=a[i][j]
    if i<n//2:
        s+=1
        e-=1
    else:
        s-=1
        e+=1
print(res)
```
