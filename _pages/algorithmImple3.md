---
title: "알고리즘 기초 - 코드 구현력 기르기(3)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation3/
layout: single
---

## K번째 큰수

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26913?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

1부터 100사이의 N개의 카드가 주어지면, 3장을 뽑아서 더한 값 중 K번째로 큰 값을 구하시오. 중복된 값은 제거하시오.

- 입력예제

10 3 (N개의 카드, K번째 수)  
13 15 34 23 45 65 33 11 26 42 (정수형 배열)

- 출력예제

143

## 내 풀이
``` swift
let input = readLine()!.split{$0==" "}.map{Int($0)!}, (n, k) = (input[0], input[1])
let a = readLine()!.split{$0==" "}.map{Int($0)!}
var tmp = Set<Int>()
for i in 0..<a.count {
    for j in i+1..<a.count {
        for z in j+1..<a.count {
            tmp.insert(a[i] + a[j] + a[z])
        }
    }
}
let answer = Array(tmp).sorted(by:>)
print(answer[k-1])
```
먼저 카드의 수와 출력할 k번째의 수를 각각 n과 k에 저장한다. 입력된 정수형 배열은 a에 저장하고 3장을 더한 값을 저장할 빈 Set인 tmp를 선언한다. 이후 for-loop를 세 번 돌면서 더한 값을 tmp에 저장한다. 이 때 두번째 for-loop는 첫번째 for-loop 다음 값부터 시작하고, 세번째 for-loop는 두번째 for-loop의 다음 값부터 시작하여 중복을 피한다. 중복을 피한다는 것은 같은 카드를 여러번 더하지 않기 위함이고, 실제로 카드가 다르다면 같은 값은 더할 수도 있다. 예를들면, 서로 다른 카드인 25, 25는 더할 수 있다는 뜻이다. 마지막으로 인덱스를 출력하기 위해 Set을 Array로 변경하고 정렬한다음 k번째 수를 출력한다(set은 순서가 없기 때문에 Kth 인덱스를 찾을 수 없다).

## 강의 풀이

강의 풀이와 차이점이 없기 때문에 파이썬 코드를 제공하고 끝내도록 하겠다.

## 파이썬 코드
``` python
n, k = map(int, input().split())
a=list(map(int, input().spiit()))
res=set()
for i in range(n):
  for j in range(i+1, n):
    for m in range(j+1, n):
      res.add(a[i]+a[j]+a[m])
res=list(res)
res.sort(reverse=True)
print(res[k-1])
```
