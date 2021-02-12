---
title: "알고리즘 기초 - 탐색&시뮬레이션(4)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search4/
layout: single
---

## 두 리스트 합치기

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26925?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

정렬된 두 리스트가 주어지면, 두 리스트를 합쳐 오름차순으로 정렬된 리스트를 출력하시오.

- 입력예제

3  (첫 번째 리스트의 길이)  
1 3 5  
5  (두 번째 리스트의 길이)  
2 3 6 7 9  

- 출력예제

1 2 3 3 5 6 7 9

## 내 풀이
``` swift
var m = [[Int]]()
for _ in 0..<2 {
    let _ = Int(readLine()!)!
    m.append(readLine()!.split{$0==" "}.map{Int($0)!})
}
var (a, b) = (m[0], m[1])
var (p1, p2) = (0, 0)
var answer = [Int]()

while p1<a.count && p2<b.count {
    if a[p1] >= b[p2] {
        answer.append(b[p2])
        p2+=1
    }
    else {
        answer.append(a[p1])
        p1+=1
    }
}
let (c, d) = (a.count>b.count ? a:b, a.count>b.count ? p1:p2)
answer += c[d...]
answer.forEach{print($0, terminator:" ")}
```
단순히 두 배열을 합쳐서 sort를 할 경우 시간복잡도에서 손해가 생길 점을 고려하여 sort를 활용하지 않고 문제풀이를 진행했다. 사실 이전시간까지 탐색의 개념을 잘 살리지 못했기 때문에 억지로 풀어본 방식이다. 먼저 두 배열을 변수 a와 b에 저장하고 각 배열을 비교할 포인터를 p1, p2로 생성한다. 그리고 짧은 쪽의 배열의 길이를 모두 탐색할 때까지 while-loop를 돌면서 a[p1]과 b[p2]를 비교하여 더 작은 값을 answer에 append한다. 짧은 배열의 탐색이 끝나면 while문이 종료된다. 이 때 더 긴 배열을 c에 저장하고 더 긴 배열의 포인터를 d에 저장한다. 그 후 answer에 해당 배열의 포인터부터 남은 값을 그대로 이어붙여준 뒤, 출력하면 정답이다.

## 강의 풀이
``` swift
let n = Int(readLine()!)!
let a = readLine()!.split{$0==" "}.map{Int($0)!}
let m = Int(readLine()!)!
let b = readLine()!.split{$0==" "}.map{Int($0)!}
var (p1, p2) = (0, 0)
var answer = [Int]()

while p1<n && p2<m {
    if a[p1]<=b[p2] {
        answer.append(a[p1])
        p1+=1
    } else {
        answer.append(b[p2])
        p2+=1
    }
}
if p1<n {answer+=a[p1...]}
else if p2<m {answer+=b[p2...]}
answer.forEach{print($0, terminator:" ")}
```
전체적인 문제풀이 로직에는 차이가 없다. 다만, 삼항연산자를 사용하지 않고 p1과 n을 비교하고 p2와 m을 비교하여 남은 배열을 처리하였다.

## 파이썬 코드
``` python
n = int(input())
a = list(map(int, input().split()))
m = int(input())
b = list(map(int, input().split()))
p1=p2=0
c=[]
while p1<n and p2<m:
    if a[p1]<=b[p2]:
        c.append(a[p1])
        p1+=1
    else:
        c.append(b[p2])
        p2+=1
if p1<n:
    c=c+a[p1:]
elif p2<m:
    c=c+b[p2:]
for x in c:
    print(x, end=' ')
```
