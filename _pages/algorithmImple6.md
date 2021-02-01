---
title: "알고리즘 기초 - 코드 구현력 기르기(6)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation6/
layout: single
---

## 정다면체

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26916?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

두 개의 정 N면체와, 정M면체가 주어지면, 주사위를 던져서 나올 수 있는 눈의 합 중 가장 확률이 높은 숫자를 출력하시오. 정답이 여러개일 경우 오름차순으로 출력하시오.

- 입력예제

4 6(N, M)

- 출력예제

5 6 7

## 내 풀이
``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}
let (n, m) = (input[0], input[1])
var a = [Int]()
for i in 1...n {
    for j in 1...m {
        a.append(i+j)
    }
}
var b = [Int](repeating: 0, count: a.max()!+1)
for i in a {
    b[i] += 1
}
var maxVal = b.max()!

for i in 0..<b.count {
    if maxVal == b[i] {
        print(i, terminator: " ")
    }
}
```
문제 해결자체가 어렵지는 않았지만 코드가 간결하지 못해서 아쉬운 문제였다. 먼저 input값으로 정N면체와 정M면체를 만들고 각 정다면체가 가지고 있는 모든 숫자를 더해서 배열 a에 저장한다. 그 후 a에서 가장 큰 값만큼 0을 반복하여 정수형 배열 b를 만들고, a를 for-loop로 돌면서 i의 인덱스에 해당하는 b의 값을 1씩 더해준다. 이렇게 되면 b가 가지고 있는 최대값이 가장 확률이 높은 숫자라는 의미이고 그 숫자의 인덱스를 출력하면 정답이다. 따라서 최대값을 maxVal에 저장하고 다시 b를 for-loop로 반복하면서 maxVal과 b[i]값이 같다면 인덱스인 i를 출력하면된다.

## 강의 풀이
``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}
let (n, m) = (input[0], input[1])
var cnt = [Int](repeating: 0, count: n+m+2)
var max = Int.min
for i in 1...n {
    for j in 1...m {
        cnt[i+j]+=1
    }
}
for i in 1...n+m+1 {
    if cnt[i] > max {
        max = cnt[i]
    }
}
for i in 1...n+m+1 {
    if cnt[i] == max {
        print(i, terminator: " ")
    }
}
```
전체적인 로직 자체는 크게 다르지 않다. 난잡하다고 생각했던 내 방식이 정해에 가까워서 다소 놀랐다. 다만 모든 눈의 합을 별도 배열에 저장하지 않고 바로 cnt[i+j]값에 카운팅을 해준 것이 큰 차이다. 시간복잡도는 같더라도 공간복잡도에서 차이가 난다. 조금 더 깊게 생각하고 풀었더라면...하는 아쉬움이 남는다.

## 파이선코드
``` python
n, m = map(int, input().split())
cnt = [0] * (n+m+1)
max = -2147000000
for i in range(1, n+1):
    for j in range(1, m+1):
        cnt[i+j]+=1
for i in range(n+m+1):
    if cnt[i]>max:
        max=cnt[i]
for i in range(n+m+1):
    if cnt[i]==max:
        print(i, end=' ')
```
같은 코드여도 파이썬이 훨씬깔끔하다.
