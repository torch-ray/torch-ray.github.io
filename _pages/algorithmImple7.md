---
title: "알고리즘 기초 - 코드 구현력 기르기(7)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation7/
layout: single
---

## 자릿수의 합

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26916?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

첫 줄에 자연수의 개수 N이 주어지고, 그 다음 N개의 자연수가 주어질 때 자릿수의 합이 최대인 자연수를 출력하시오.

- 입력예제

3  
125 15323 97

- 출력예제

97

## 내 풀이

``` swift
readLine()
let input = readLine()!.split{$0==" "}.map{Int($0)!}
var arr = input
var a = [Int]()
for i in 0..<arr.count {
    var sum = 0
    while arr[i] > 0 {
        sum += arr[i] % 10
        arr[i] = arr[i] / 10
    }
    a.append(sum)
}
print(input[a.firstIndex(of: a.max()!)!])
```
자연수의 개수는 문제풀이에 활용을 하지 않아서 별도로 저장하지 않고, 바로 자연수 값을 input에 입력받았다. 이후 각 자연수가 0이될 때까지 나머지를 더해주는 연산을 통해서 각 자릿수를 sum에 더하고 그 값을 배열 a에 저장한다. 입력예제 대로면 for-loop가 종료됐을 때 a에는 [8, 13, 16]이 저장된다. 따라서 16이 가장 큰 수이고 이에 해당하는 자연수인 97을 출력하면된다. 즉, a의 최대값인 16의 인덱스를 가져와서 input으로 출력하면 정답이다.

## 강의 풀이

``` swift
readLine()
let input = readLine()!.split{$0==" "}.map{Int($0)!}
var arr = input
var maxVal = Int.min

func sumNum(_ i:Int) -> Int {
    var x = i
    var sum = 0
    while x > 0 {
        sum += x % 10
        x = x / 10
    }
    return sum
}

var res = 0

for i in arr {
    let tmp = sumNum(i)
    if tmp > maxVal {
        maxVal = tmp
        res = i
    }
}
print(res)
```
내 풀이와 전체적인 로직은 똑같기 때문에 별도 설명은 필요없다. 다만, while-loop를 따로 함수로 만들어서 실행했다. 훨신 가독성이 좋은 코드였다. 백준 숏코딩에 재미가 들려서 너무 짧게만 풀려고했던 것 같다. 다음 문제풀이부터는 참고할 예정이다.

## 파이썬코드
``` python
n=int(input())
a=list(map(int, input().split()))
def digit_sum(x):
    sum=0
    while x > 0:
        sum+=x%10
        x=x//10
    return  sum
max = -2147000000
for x in a:
    tot = digit_sum(x)
    if tot > max:
        max=tot
        res=x
print(res)
```
