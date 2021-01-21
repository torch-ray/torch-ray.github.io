---
title: "백준 1157번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/1157/
layout: single
---

## 백준 - 단어공부

<img width="1152" alt="스크린샷 2021-01-22 오전 8 20 38" src="https://user-images.githubusercontent.com/74946802/105424438-bf520d80-5c8a-11eb-8c50-8d463cdd2d88.png">

알파벳 대소문자로 구성된 문자열이 주어지면 가장 많이 사용된 알파벳을 출력하면 된다. 대문자와 소문자는 구별하지 않는다. 가장 많이 사용된 알파벳이 여러개일 경우에는 ?를 출력한다.

- 체크포인트: 출력은 반드시 대문자로한다.

## 입력값 대문자변환 및 빈 딕셔너리 생성
``` swift
let n = readLine()!.uppercased()
var g = [String : Int]()
```
대문자와 소문자를 구별하지 않고 알파벳을 카운팅해야 하기 때문에 입력받은 문자열을 모두 대문자로 만들어준다. 숫자나, 기호가 포함되어 있다면 문제가 생길 수 있지만 문제의 단서에 알파벳으로 구성된 문자열이라고 명시되어 있기 때문에 바로 대문자로 변환해도 문제가 없다. 물론 소문자로 통일해도 상관없으나, 출력을 대문자로 해야하기 때문에 번거롭게 소문자로 변환할 필요는 없다. 입력받은 알파벳과 사용된 숫자를 저장할 빈 딕셔너리를 생성한다.

## 알파벳 카운팅
``` swift
n.forEach{
  if g[String($0)] == nil { g[String($0)]=1 }
  else { g[String($0)]? += 1 }
}
```
입력값을 대문자로 변환하여 저장한 변수 n을 탐색하면서사용된 횟수만큼 카운팅을 하여 딕셔너리에 저장한다. 예를들면 g["M"]이 nil이면 1을 넣어주고 이미 g["M"]에 값이 있다면 + 1을 해주는 방식이다.

## 최대값 탐색
``` swift
var result = [String]()
for key in g.keys {
  if g[key] == g.values.max()! { result.append(key) }
}
print(result.count > 1 ? "?" : "\(result[0])")
```
결과값을 저장할 빈 배열을 만들어주고 알파벳과 사용된 횟수 정보가 담겨있는 딕셔너리를 탐색한다. "Mississipi"라는 문자열이 입력값으로 들어왔다고 가정하면, 현재 g["M"]이라는 key에는 1이라는 value가 저장되어있다. 딕셔너리의 모든 key에 담겨있는 value를 최대값과 비교하며 최대값과 같은 경우 result변수에 저장한다. 그리고 result의 count가 1보다 큰 경우는 가장 많이 사용된 알파벳이 2개 이상이라는 의미이기 때문에 ?를 출력하고, 그렇지 않은 경우에는 result값을 출력한다.

## 전체코드
``` swift
let n=readLine()!.uppercased()
var g=[String: Int]()
n.forEach{
    if g[String($0)] == nil {g[String($0)]=1}
    else {g[String($0)]?+=1}
}
var result = [String]()
for key in g.keys {
    if g[key] == g.values.max()! {result.append(key)}
}
print(result.count>1 ? "?" : "\(result[0])")
```
