---
title: "백준 2941번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/2941/
layout: single
---

## 백준 - 크로아티아 알파벳

<img width="1014" alt="스크린샷 2021-02-03 오전 9 10 19" src="https://user-images.githubusercontent.com/74946802/106679324-bd2f6d80-65ff-11eb-8cbc-bfcc185a2e53.png">
<img width="1014" alt="스크린샷 2021-02-03 오전 9 10 34" src="https://user-images.githubusercontent.com/74946802/106679339-c6b8d580-65ff-11eb-8e9d-c18223e74211.png">

크로아티아 알파벳이 주어지면, 해당 문자열의 개수를 반환하면 된다. 예를들어, lj는 두 개의 알파벳으로 이뤄져있지만, 크로아티아 알파벳 기준으로는 1개의 알파벳이다.

- 체크포인트: dz=와 z=를 구분하여 카운팅해야한다.

## 크로아티아 알파벳 리스트 생성
``` swift
import Foundation
var n = readLine()!
let m = ["c=", "c-", "dz=", "d-", "lj", "nj", "s=", "z="]
```
Foundation을 활용할 예정이기 때문에 미리 import해준다. 이후 변수 n에 카운팅 할 문자열을 입력받고, 상수 m에 크로아티아 알파벳을 입력해준다.

## 알파벳으로 변환
``` swift
for i in 0..<m.count {
  n = n.replacingOccurrences(of: m[i], with: "a")
}
print(n.count)
```
이 문제의 포인트는 swift 문법을 얼마나 이해하고 있느냐로 쉽게 풀 수 있을지 없을지가 결정된다. replacingOccurrences를 활용하면 비교 대상 문자열을 원하는 문자로 바꿀 수 있다. 예를들어 본 문제에서는 for-loop를 돌면서 크로아티아 알파벳과 입력받은 알파벳을 비교하여 크로아티아 알파벳이 존재한다면 해당 문자열을 "a"로 바꾼 것이다. 크로아티아 알파벳 리스트 m에서 dz=가 z=보다 앞에 있기 때문에 둘 사이를 구분하는 것도 쉽게 가능해진다. "a"는 임의로 정한 문자일뿐 해당 위치에 무엇을 사용해도 결과는 같다.

## 전체코드
``` swift
import Foundation
var n = readLine()!
let m = ["c=", "c-", "dz=", "d-", "lj", "nj", "s=", "z="]
for i in 0..<m.count {n = n.replacingOccurrences(of: m[i], with: "a")}
print(n.count)

```
