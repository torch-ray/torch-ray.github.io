---
title: "알고리즘 기초 - 탐색&시뮬레이션(1)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search1/
layout: single
---

## 회문 문자열 검사

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26920?tab=curriculum)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

N개의 문자열 데이터를 입력받아 해당 문자열이 앞에서 읽으나 뒤에서 읽으나 같은 경우(회문 문자열) YES, 아닌 경우 NO를 출력하시오. 단, 대소문자는 구분하지 않는다.

- 입력예제

5  
level  
moon  
abcba  
soon  
gooG  

- 출력예제

\#1 YES  
\#2 NO  
\#3 YES  
\#4 NO  
\#5 YES  

## 내 풀이
``` swift
let n = Int(readLine()!)!
for i in 0..<n {
    let m = readLine()!.lowercased()
    if m == String(m.reversed()) {
        print("#\(i+1) YES")
    } else {
        print("#\(i+1) NO")
    }
}
```
대소문자를 구분하지 않기 위해 입력받은 문자열을 모두 소문자화하여 m에 저장한다. reverse를 활용하여 입력받은 문자열을 뒤집어서 원래 문자열과 같은지 비교하여, 같은 경우 YES, 아닌 경우 NO를 출력하면 된다.

## 강의 풀이
``` swift
let n = Int(readLine()!)!
for i in 0..<n {
    var s = readLine()!
    s = s.uppercased()
    let size = s.count
    for j in 0..<size/2 {
        if s[s.index(s.startIndex, offsetBy: j)] != s[s.index(s.endIndex, offsetBy: -1-j)] {
            print("#\(i+1) NO")
            break
        } else {
            print("#\(i+1) YES")
            break
        }
    }
}
```
강의에서는 실제 구현능력을 위해 reverse를 활용하지 않고 for-loop를 통해 비교하였다. 입력받은 문자열을 모두 대문자화 해주고, for-loop를 입력받은 문자열의 크기의 나누기 2만큼 돌면서 문자열의 첫번째와 마지막을 비교하여 같은지 확인하는 방식으로 풀이를 진행하였다. level로 예를들면, 첫번째 l과 마지막 l을 비교하고, 두번째 e와 네번째 e를 비교하는 방식이다. 짝수의 경우 모두 비교하고 끝이나고, 홀수의 경우 가운데 문자열은 비교하지 않게되는데, 가운데 문자열은 앞에서 읽으나 뒤에서 읽으나 같기 때문에 상관없다. 단, 본 풀이를 활용할 경우 swift는 문자열 인덱스에 대한 이해가 필요하다. 강의에서도 reverse를 활용한 파이썬 코드를 제공하긴했기 때문에 아래 파이썬 코드에는 두 가지 풀이식을 모두 제공한다.

## 파이썬 코드
``` python
n=int(input())
for i in range(n):
    s=input()
    s=s.upper()
    size=len(s)
    for j in range(size//2):
        if s[j] != s[-1-j]:
            print("#%d NO" %(i+1))
            break
    else:
        print("#%d YES" %(i+1))
```

``` python
n=int(input())
for i in range(n):
    s=input()
    s=s.upper()
    if s==s[::-1]:
        print("#%d YES" %(i+1))
    else:
        print("#%d NO" %(i+1))
```
