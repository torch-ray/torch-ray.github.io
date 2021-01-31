---
title: "알고리즘 기초 - 코드 구현력 기르기(1)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation1/
layout: single
---

## K번째 약수

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26912?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제
두 수 n과 k가 주어지면 n의 약수 중 k 번째 약수를 구하시오.  
k번째 약수가 존재하지 않는 경우 -1을 반환하시오.

## 내 풀이

``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}, (n, k) = (input[0], input[1])
var ans = [Int]()
for i in 1...n {
    if n%i == 0 {
        ans.append(i)
    }
}
print(k==0 ? -1 : ans.count<b ? -1 : ans[k-1])
```

for-loop를 돌면서 모든 약수를 배열에 저장하고 k-1번째를 출력했다. 그리고 k가 0이거나 약수의 범위를 넘어설 경우 -1을 출력하도록 삼항연산자를 활용했다. 강의에서는 cnt와 k값을 매칭시키는 방법을 활용했다. cnt를 활용하면 k번째가 약수의 마지막이 아니라면 시간복잡도 측면에서 효율이 더 좋고, 배열에 약수를 저장하지 않기 때문에 메모리 공간복잡도 측면에서도 효율적이다. 아래 코드는 강의에서 cnt를 활용한 방식이다.

## 강의 풀이

``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}, (n, k) = (input[0], input[1])
var cnt = 0
for i in 1...n {
    if n%i == 0 {cnt+=1}
    if cnt==k {
        print(i)
        break
    }
}
if cnt != k {print(-1)}
```

먼저 주어진 두 수를 n과 k에 각각 저장한다. 이후 1부터 n까지 for문을 돌면서 나누어 떨어지는 경우 cnt값을 증가시킨다. cnt값이 k와 같아진다면 그때의 i를 출력하고 루프를 종료한다. 파이썬 코드에서는 for-else구문을 활용하여 for 문이 정상종료됐을 경우, 즉 break가 실행되지 않았을 경우에는 -1을 출력한다. swift에는 for-else구문이 없기 때문에 마지막에 cnt가 k와 같지 않은 경우에 -1을 출력하도록 한다.

## 파이썬 코드
``` python
n, k = map(int, input().split())
cnt = 0
for i in range(1, n+1):
  if n%i==0:
    cnt+=1
  if cnt==k:
    print(i)
    break
else:
  print(-1)
```
