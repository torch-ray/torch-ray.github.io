---
title: "리트코드 7 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/leetcode/7
layout: single
---

## 리트코드 - Reverse Integer

<img width="793" alt="스크린샷 2021-01-15 오전 8 48 38" src="https://user-images.githubusercontent.com/74946802/104662566-7cce8500-570e-11eb-8b16-859e3224f745.png">

Int32 x가 주어지면 x의 Reverse 형태를 반환하는 문제이다. 즉, 321의 경우 123을 반환하고 -123의 경우 -321을 반환하면된다. 단 Reverse 형태가 Int32를 초과하는 경우에는 0을 반환해야한다.

- 체크포인트1: 음수부호를 별도로 처리해줘야한다.
- 체크포인트2: Int32 초과여부를 확인해야한다.

## 문자열로 만들어서 Reverse

``` swift
func reverse(_ x: Int) -> Int {
  let str = String(x)
  var reverseStr = String(str.reversed())
}
```

정수를 바로 reverse로 뒤집을 수는 없기 때문에 문자열 변환을 해준다. 123이 입력됐을 경우 "123"으로 변환된다. reversed()를 사용할 경우 Reversed Collection 타입으로 바뀌기 때문에 다시 한 번 String을 활용하여 문자열 변환을 해준다.

## 음수부호 처리

``` swift
if reverseStr.hasSuffix("-") {
  reverseStr.removeLast()
  reverseStr.insert("-", at: reverseStr.startIndex)
}
```

x값으로 -123이 입력된 경우 Reverse형태로 변환하면 "321-" 형태로 변환된다. 그래서 이 경우에 문자열 끝에 "-" 부호가 붙어있는지 확인하고 붙어있다면 해당 값을 삭제하고 문자열 맨 앞으로 "-" 부호를 삽입해준다. 문자열의 경우 1, 2, 3 등과 같은 정수형 Index를 사용할 수 없기때문에 문자열 Index를 활용해야한다.

## Int32 초과여부 확인

``` swift
if let result = Int32(reverseStr) {
  return Int(result)
}
return 0
```

if let 구문을 활용하여 reverseStr을 Int32로 변환한 값이 true 인지 false인지를 확인한다. true일 경우 해당 값을 그대로 Int로 변환하여 반환하면되고, false일 경우 if문이 실행되지 않고 바로 0을 반환한다.

## 전체코드

<img width="472" alt="스크린샷 2021-01-15 오전 9 08 08" src="https://user-images.githubusercontent.com/74946802/104663850-3c243b00-5711-11eb-89af-4db89109f6f5.png">
