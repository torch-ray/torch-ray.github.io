---
title: "알고리즘 기초 - 코드 구현력 기르기(5)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation5/
layout: single
---

## 대표값

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26915?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

N명의 학생 수의 수학점수가 주어진다. 이 때 N명의 학생수의 평균을 구하고, 평균의 가장 가까운 점수를 가진 학생이 몇 번째인지 구하시오. 단, 평균과 가장 가까운 학생이 여러명일 때는 가장 높은 점수의 학생을 출력하고, 높은 점수를 가진 학생이 여러명일 경우 가장 빠른 번호의 학생을 출력한다. 평균은 소수 첫번째 자리에서 반올림한다.

- 입력예제

10(N명의 학생 수)  
45 73 66 87 92 67 75 79 75 80(수학점수)

- 출력예제

74 7

## 내 풀이
``` swift
import Foundation
let n = Int(readLine()!)!
let a = readLine()!.split{$0==" "}.map{Double($0)!}
let avg = round(a.reduce(0, +) / Double(n))
var closeVal = Int.max
var std = 0
var answer = 0
for i in 0..<a.count {
    if Int(abs(avg-a[i])) < closeVal {
        closeVal = Int(abs(avg-a[i]))
        std = Int(a[i])
        answer = i
    } else if Int(abs(avg-a[i])) == closeVal {
        if std < Int(a[i]) {
            std = Int(a[i])
            answer = i
        }
    }
}
print(Int(avg), answer+1)
```
학생 수를 n에 입력받고, n명의 학생들의 점수를 a 배열에 입력받아 저장한다. Int형이 아니라 Double로 저장한 이유는 소수를 반올림하기 위해서다. avg에는 평균값을 구해 저장하고, 가장 가까운 값을 저장할 closeVal과 가장 가까운 값의 점수를 저장할 std, 그리고 그 점수를 가지고 있는 학생의 번호를 저장할 answer를 생성한다.

이후 for-loop를 돌면서 평균 값에서 학생 개인의 수학점수를 뺀 값을 closeVal과 비교하여 작을 경우에 저장하고 std와, answer도 해당 학생의 점수와 번호로 바꿔준다. 이때 같은 점수를 가지고 있을 경우 빠른 번호의 학생을 출력해야 하기 때문에 <=기호가 아니라 <기호를 사용해준다. 또한 차이값이 같을 경우에는 std값을 비교하여 더 큰값을 가지고 있는 경우에만 std값과 answer값을 변경해준다.

강의 코드의 경우 enumerate을 활용했지만, 전체적인 코드의 로직에서 차이점은 없다.

## 강의 풀이

강의 풀이와 차이점이 없기 때문에 파이썬 코드를 제공하고 끝내도록 하겠다.

## 파이썬 코드
``` python
n=int(input())
a=list(map(int, input().split()))
ave=round(sum(a)/n)
print(ave)
min=2147000000
for idx, x in enumerate(a):
  tmp = abs(x-ave)
  if tmp<min:
    min=tmp
    score=x
    res=idx+1
  elif tmp==min:
    if x>score:
      score=x
      res=idx+1
print(ave, res)
```
