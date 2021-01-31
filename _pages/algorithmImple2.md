---
title: "알고리즘 기초 - 코드 구현력 기르기(2)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation2/
layout: single
---

## K번째 수

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26913?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

N개의 숫자로 이루어진 배열이 주어졌을 , s부터 e번째까지 오름차순으로 정열하고 k번째 수를 출력하시오.

- 입력예제

2(테스트케이스)  
6 2 5 3(n개의수, s, e, k)  
5 2 7 3 8 9(정수형 배열)  
15 3 10 3  
4 15 8 16 6 6 17 3 10 11 18 7 14 7 15  

- 출력예제

\#1 7  
\#2 6

## 내 풀이
``` swift
let T = Int(readLine()!)!
for i in 1...T {
    let input = readLine()!.split{$0==" "}.map{Int($0)!}
    let (s, e, k) = (input[1], input[2], input[3])
    let a = readLine()!.split{$0==" "}.map{Int($0)!}
    let answer = a[s-1..<e].sorted()
    print("#\(i) \(answer[k-1])")
}
```
테스트 케이스의 수를 T에 저장하고 그만큼 for-loop를 돌면서 입력값을 받는다. N개의 수라고했지만, 문제를 해결하는데있어서 해당 정보는 필요없기 때문에 별도 N값에 저장하지 않았다. 입력 배열을 a에 저장하고 a의 s-1부터 e-1까지의 수를 정렬하여 answer에 저장한다. 이후 answer의 k-1번째 값을 형식에 맞춰서 출력하였다.

## 강의 풀이

강의 풀이와 차이점이 없기 때문에 파이썬 코드를 제공하고 끝내도록 하겠다.

## 파이썬 코드
```python
T=int(input())
for t in range(T):
  n, s, e, k = map(int, input().split())
  a = list(map(int, input().split()))
  a = a[s-1:e]
  a.sort()
  print("%#d %d" %(t+1, a[k-1]))
```
