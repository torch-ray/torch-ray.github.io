---
title: "알고리즘 기초 - 코드 구현력 기르기(9)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation9/
layout: single
---

## 뒤집은 소수

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26919?tab=curriculum)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

N개의 자연수가 주어지면, 각 자연수의 뒤집은 수가 소수인지 판별하여 소수일 경우 출력하시오. 730의 경우 뒤집으면 37로, 첫자리의 0을 허락하지 않으며 거꾸로 뒤집는 함수 reverse와 소수 판별 함수 isPrime을 반드시 생성하시오.

- 입력예제

5 (N개의 자연수)  
32 55 62 3700 250

- 출력예제

23 73

## 내 풀이
``` swift
func reverse(_ x:String) -> Int {
    let str = x.reversed()
    let res = Int(String(str))!
    return res
}
func isPrime(_ x:Int) -> Bool {
    let prime:Set<Int> = [1, x]
    var tmp = Set<Int>()
    for i in 1...x {
        if x % i == 0 {
            tmp.insert(i)
        }
    }
    return prime == tmp ? true : false
}
readLine()
let n = readLine()!.split{$0==" "}
var a = [Int]()
for i in n {a.append(reverse(String(i)))}
for i in a {
    if isPrime(i) {
        print(i, terminator:" ")
    }
}
```
지난 시간에 이어 소수 판별 문제다. 다만, 숫자가 주어지면 해당 숫자를 거꾸로 뒤집었을 때 소수인지를 판별해야 한다. reverse함수를 만들어 입력받은 숫자를 문자로 만들어서 거꾸로 뒤집은 다음 다시 정수로 변환하여 반환하였다. 그렇게 받은 수를 배열에 저장한 뒤에, 이번에는 isPrime함수로 입력하여 소수일 경우 true를 반환하도록 설계하였다. 가장 마지막 for-loop에서는 isPrime이 true를 반환할 경우에만 해당 수를 출력하도록 하였다.

## 강의 풀이
``` swift
func reverse(_ x:Int) -> Int {
    var res = 0
    var n = x
    while n > 0 {
        var t = n%10
        res = res * 10 + t
        n = n / 10
    }
    return res
}

func isPrime(_ x:Int) -> Bool {
    if x==1 {
        return false
    }
    for i in 2..<x/2+1 {
        if x%i==0 {
            return false
        }
    }
    return true
}

let n=Int(readLine()!)!
let a=readLine()!.split{$0==" "}.map{Int($0)!}
for x in a{
    let tmp = reverse(x)
    if isPrime(tmp) {
        print(tmp, terminator: " ")
    }
}
```
숫자를 거꾸로 뒤집을 때, 문자열을 사용하지 않았다. 해당 수를 10으로 나눈 나머지를 t에 저장하고, res에는 res에 10을 곱하고 t를 더한 값을 다시 저장한다. 이 로직을 바탕으로 9010을 뒤집어보면, 처음엔 t에 0이 저장되고, res에도 0이 저장된다. 그 다음은 t에 1이 저장되고, res에도 1이 저장된다. 그 다음은 t에 0이저장되고 res에는 기존에 1이 있었기 때문에 곱하기 10을하여 10이 저장된다. 다음은 t에 9가 저장되고 기존 10에 10을곱하고 9를 더해주니 마지막으로 109가된다. 9010를 뒤집었을 때 값이 나온 것이다.

이를 통해 숫자를 뒤집고 뒤집은 숫자를 바로 isPrime함수를 활용하여 소수 판별해준다. 여기서 for-loop를 x/2까지만 반복한 이유는 모든 자연수는 1과 자기자신을 제외한 약수는 그 반까지만 존재하기 때문이다. 그리고 내 코드와 마찬가지로 true를 반환한 경우에만 해당 수를 출력한다.

## 파이썬 코드
``` python
def reverse(x):
    res=0
    while x>0:
        t=x%10
        res=res*10+t
        x=x//10
    return  res

def isPrime(x):
    if x==1:
        return False
    for i in range(2, x//2+1):
        if x%i==0:
            return False
    else:
        return True

n=int(input())
a=list(map(int, input().split()))
for x in a:
    tmp=reverse(x)
    if isPrime(tmp):
        print(tmp, end=' ')
```
