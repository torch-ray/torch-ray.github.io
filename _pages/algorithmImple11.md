---
title: "알고리즘 기초 - 코드 구현력 기르기(11)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation11/
layout: single
---

## 점수 계산

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26922?tab=curriculum)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

어떤 시험 문제의 채점 결과가 정답(1)과 오답(0)으로 주어질 때, 해당 채점 결과의 점수를 계산하시오. 연속으로 정답을 맞춘 경우에는 가산점을 부여하며 오답이 나오면 가산점이 초기화된다. 예를들어, 1 1 1의 경우 세번째 1의 경우에는 3점을 부여하며, 1 1 1 0 1 의 경우 마지막 1은 1점을 부여한다.

- 입력예제

10(문제의 개수)       
1 0 1 1 1 0 0 1 1 0(채점 결과)  

- 출력예제

10(점수)  

## 내 풀이
``` swift
readLine()
let n = readLine()!.split{$0==" "}.map{Int($0)!}
var s = 0
var res = 0
for i in n {
    if i == 1 {
        s = s+1
        res += s
    } else {
        s = 0
    }
}
print(res)
```
연속된 정답의 경우 연속된 수만큼 가산점을 부여하고 오답이 등장하면 가산점을 초기화하여 점수를 계산하면 된다. 문제의 수는 풀이에 필요가 없어서 따로 저장하지 않았고, 채점 결과는 정수형 배열로 n에 저장한다. 이후 for-loop로 n을 돌면서 정답인 경우에는 변수 s에 s+1값을 더해준다. s+1값을 더해주는 이유는 가산점을 계산하기 위해서다. 그리고 추후 가산점을 초기화할 경우를 대비하여 s값은 따로 res에 저장한다. 그리고 정답이 아닌 경우에는 s를 0으로 초기화 해주고 for-loop가 종료되면 res를 출력하면 된다.

## 추가 풀이
``` swift
readLine()
let n = readLine()!.split{$0==" "}.split{$0=="0"}
var res = 0
for i in n {
    let a = i.count
    res += (a * (a+1)) / 2
}
print(res)
```
가우스의 법칙을 활용한 풀이다. 0 제거하고 문자열을 입력받으면 입력 예제의 경우 ["1", "111", "11"]과 같이 n에 저장된다. 이후 i의 길이에 가우스의 법칙을 적용하여(n까지의 연속된 수의 합은 n * (n+1) / 2) 변수 res에 저장한 뒤에 출력하면 된다.

## 강의 풀이

강의 풀이와 차이점이 없기 때문에 파이썬 코드를 제공하고 끝내도록 하겠다.

## 파이썬 코드
``` python
n=int(input())
a=list(map(int, input().split()))
sum = 0
cnt = 0
for x in a:
    if x==1:
        cnt+=1
        sum+=cnt
    else:
        cnt=0
print(sum)
```
