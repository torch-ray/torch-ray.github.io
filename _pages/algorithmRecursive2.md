---
title: "알고리즘 기초 - Recursive(2)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/recursive2/
layout: single
---

## 순환적으로 사고하기

참고자료: [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/lecture/4072?tab=curriculum)

일반적으로 for문이나, while문을 사용해서 해결하는 문제를 recursion을 활용하여 해결할 수 있다.

## 문자열의 길이 계산하기

문자열의 길이를 계산하기 위한 방법은 각 언어별 함수(count, len 등)를 활용하는 방법이 있을 수 있지만, 해당 챕터에서는 함수자체가 아닌 함수가 작동하는 방법 중 재귀적인 방법에 대해 살펴보고자 한다.  

문자열을 계산하는 대표적인 방법으로는 반복문을 활용하여 주어진 문자열을 앞에서부터 하나씩 카운팅하는 방법이 있을 것이다. 이러한 방식을 절차적인 프로그래밍이라고 볼 수 있다. 그렇다면 recursive한 방법으로 문자열의 길이를 계산하는 방법은 무엇일까? 예를들면, 10의 길이를 가진 문자열의 경우 전체 문자열에서 첫번째 문자를 뺀 나머지의 문자열의 길이에 1을 더한 값이라고 계산할 수 있다. 물론 앞서 Recursion의 개념에서 살펴봤듯이, 이러한 방식은 반드시 BaseCase가 있어야하기 때문에 문자열이 주어지지 않은 경우는 0을 return해주면 된다. 무슨 말인지 이해하기 어렵다면 아래 코드를 통해 쉽게 이해할 수 있다.

``` swift
func length(_ str: String) -> Int {
    if str.isEmpty { return 0 }
    return 1 + length(String(str.suffix(str.count-1)))
}
```

코드를 따라가보면 length함수에 "abc"라는 문자열이 입력됐다고 가정해보자. 그렇다면 비어있는 문자열이 아니기때문에 if문은 실행되지 않고 다시 length함수에 첫번째 문자열을 제외한 "bc"가 입력된다. 같은 함수가 반복되면 결국 빈 문자열이 입력되고 0을 반환한다. 반환한 0에는 1이 더해지고, 1에 다시 1이 더해져 2가되고, 2에 다시 1이 더해져 3을 반환하며 함수가 종료된다.


## 2진수로 변환하여 출력하기

이런 방식으로 10진수가 주어졌을 때 recursion을 활용하여 2진수로 변환해줄 수 있다. 다음 코드를 통해 살펴보자.

``` swift
func printBinary(_ n: Int){
    if n<2 {
        print(n, terminator: "")
    } else {
        printBinary(n/2)
        print(n%2, terminator: "")
    }
}
```

10이 주어지면 2로 나누어진 몫인 5로 재귀함수를 호출하고, 이 과정은 n이 2보다 작아질 때까지 반복된다. 그리고 2를 2로 나눈 몫인 1이 재귀함수로 호출되는 순간 1이 출력되고 순차적으로 2의 나머지값 0, 5의 나머지값 1, 10의 나머지값 0이 출력되고, 결과적으로 1010이 출력되면서 종료된다.

## 배열의 합 구하기

마찬가지로 recursion을 활용하여 배열의 합을 구할 수도 있다.

``` swift
func sum(_ n: Int, d: [Int]) -> Int {
    if n<=0 {return 0}
    return sum(n-1, d: d) + d[n-1]
}
```

코드를 살펴보면 n은 배열의 길이, d는 정수를 element로 가지고 있는 배열이다. 예를들면 (3, [3,2,1])이 입력되면 n이 0이 될때까지 재귀함수가 반복된다. 코드를 따라가보면 (3, [3,2,1]) => (2, [3,2,1] + 1) => (1, [3,2,1] + 2) => (0, [3, 2, 1] + 3) => return 0이 된다. 0 반환되는 순간 역순으로 올라가며 덧셈이 진행되어 3 + 2 + 1의 합인 6이 반환되며 함수가 종료된다.

## 내용정리

모든 반복문은 재귀함수로 변경이 가능하고, 그 역도 성립한다. 순환함수는 복잡한 알고리즘을 단순하고 알귀쉽게 표현이 가능하다는 장점이 있다. 하지만, 함수 호출에 따른 [오버헤드](https://ko.wikipedia.org/wiki/%EC%98%A4%EB%B2%84%ED%97%A4%EB%93%9C)가 있다. 따라서 재귀함수는 상황에 따라 필요한 경우에 적절하게 사용해야한다.