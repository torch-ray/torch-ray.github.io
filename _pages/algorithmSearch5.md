---
title: "알고리즘 기초 - 탐색&시뮬레이션(5)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search5/
layout: single
---

## 수의 합

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26926?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

N개의 수열이 주어지면 연속적인 수의 합이 M이 되는 모든 경우의 수를 구하시오.

- 입력예제

8 3 (N, M)
1 2 1 3 1 1 1 2 (수열)

- 출력예제

5

## 내 풀이
``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}
let m = input[1]
let n = readLine()!.split{$0==" "}.map{Int($0)!}
var cnt = 0

for i in 0..<n.count {
    if n[i] == m {
        cnt += 1
        continue
    }
    var sum = n[i]
    for j in i+1..<n.count {
        sum += n[j]
        if sum == m {
            cnt += 1
            break
        }
    }
}
print(cnt)
```
이중 for-loop문을 활용하여 중복을 없애고 모든 경우의 수를 확인한다. 먼저 n[i]가 m과 같으면 다음 수와 더할 필요가 없기 때문에, 바로 cnt값을 증가시키고 다음 i로 넘어간다.

그렇지 않을 경우 변수 sum에 m[i]값을 더해주고, for-j문을 돌면서 i의 다음 인덱스 값부터 sum에 더해준다. 이때 m과 같아지면 cnt값을 증가시키고 j문을 종료시킨다.

## 강의 풀이
``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}
let (n, m) = (input[0], input[1])
let a = readLine()!.split{$0==" "}.map{Int($0)!}
var (lt, rt) = (0, 1)
var tot = a[0]
var cnt = 0

while true {
    if tot<m {
        if rt<n {
            tot+=a[rt]
            rt+=1
        } else {
            break
        }
    } else if tot==m {
        cnt+=1
        tot-=a[lt]
        lt+=1
    } else {
        tot-=a[lt]
        lt+=1
    }
}
print(cnt)
```
이중 loop를 활용하지 않고, 포인터를 활용해서 해결했다. 시간복잡도 측면에서 내 코드는 O(n^2)이라면 강의코드는 O(n)이다. 포인터를 활용해서 문제를 해결하려는 사고를 꾸준히 해봐야겠다.

lt와 rt를 0, 1로 저장하고 tot에 배열 a의 첫번째 값을 넣고 while-loop를 돌기 시작한다. tot가 비교해야할 값 m보다 작고 rt가 n보다 작은 경우에는 tot에 a[rt]값을 넣고 rt를 1증가시킨다. 이때 rt가 n이상이라면 수열의 길이를 초과했다는 뜻이기 때문에 break해준다.

tot가 m과 같은 경우엔 cnt값을 증가시키고 tot에서 a[lt]값을 빼주고 lt값을 증가시킨다.

마지막으로 tot가 더 큰 경우에도 tot에서 a[lt]값을 빼주고 lt값을 증가시키면 된다.

## 파이썬 코드
``` python
n, m = map(int, input().split())
a = list(map(int, input().split()))
lt = 0
rt = 1
tot = a[0]
cnt = 0

while True:
    if tot<m:
        if rt<n:
            tot+=a[rt]
            rt+=1
        else:
            break
    elif tot==m:
        cnt+=1
        tot-=a[lt]
        lt+=1
    else:
        tot-=a[lt]
        lt+=1
print(cnt)
```
