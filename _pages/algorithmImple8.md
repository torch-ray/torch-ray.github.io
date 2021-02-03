---
title: "알고리즘 기초 - 코드 구현력 기르기(8)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation8/
layout: single
---

## 소수의 개수(에라토스테네스 체)

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26916?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

자연수 N이 입력되면 1부터 N까지의 소수의 개수를 반환하시오.

- 입력예제

20

- 출력예제

8

## 내 풀이
``` swift
let n = Int(readLine()!)!
var a = [Bool](repeating: false, count: n+1)
var cnt = 0
for i in 2...n {
    if a[i] == false {
        cnt+=1
    }
    for j in stride(from: i, to: n+1, by: i) {
        a[j] = true
    }
}
print(cnt)
```
에라토스테네스 체 알고리즘에 대해 알고 있어서 쉽게 해결한 문제다. 소수는 1과 자기 자신으로만 나누어 떨어지는 수를 의미하는데, 1은 소수가 될 수 없기 때문에 2부터 시작한다. 미리 n의 수만큼 생성해뒀던 Boolean타입 배열 a와 비교하면서 a[i]가 false이면 소수로 cnt 값을 올려주고, 해당 수부터 다시 for-loop를 돌면서 해당 수의 배수는 모두 true로 바꿔준다. 해당 수로 나눠 떨어지는 수는 소수가 될 수 없기 때문이다.

## 추가 풀이
``` swift
let n = Int(readLine()!)!
var cnt=0

func isPrime(_ num:Int) -> Set<Int> {
    var res=Set<Int>()
    for i in 1...num {
        if num % i == 0 {
            res.insert(i)
        }
    }
    return res
}

for i in 2...n {
    let prime:Set<Int> = [1, i]
    if prime == isPrime(i) {
        cnt+=1
    }
}
print(cnt)
```
이런식으로 set과 isPrime함수를 만들어서 비교하는 것도 가능하다. prime이라는 set을 만들어서 1과 비교가 필요한 수 i를 넣어놓고, isPrime함수로 i를 입력하여 나눠떨어지는 수를 모두 리턴하여 prime과 결과가 같으면 소수이다.

## 강의 풀이

강의 풀이와 차이점이 없기 때문에 파이썬 코드를 제공하고 끝내도록 하겠다.

## 파이썬 코드
``` python
n=int(input())
ch=[0]*(n+1)
cnt=0

for i in range(2, n+1):
    if ch[i]==0:
        cnt+=1
        for j in range(i, n+1, i):
            ch[j]=True
print(cnt)
```
