---
title: "알고리즘 기초 - 코드 구현력 기르기(4)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/implementation4/
layout: single
---

## 최소값 구하기

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/49905?tab=curriculum&speed=2)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 최소값 구하는 알고리즘 학습

## 강의내용
``` swift
let arr = [5, 3, 7, 9, 2, 5, 2, 6]
var arrMin = Int.max
for i in 0..<arr.count {
    if arr[i] < arrMin {
        arrMin = arr[i]
    }
}
print(arrMin)

```
arr에서 최소값을 찾는 알고리즘을 구현한다. arrMin 변수에는 가장 큰 정수 값을 저장한다. 이후 arr의 길이만큼 for-loop를 돌면서 arr[i]값이 arrMin보다 작으면 arrMin에 arr[i]값을 저장한다. 정수의 가장 큰 값을 활용하지 않는 방법도 있다.

``` swift
let arr = [5, 3, 7, 9, 2, 5, 2, 6]
var arrMin = arr[0]
for i in 1..<arr.count {
  if arr[i] < arrMin {
    arrMin = arr[i]
    }
}
print(arrMin)
```
이런식으로 arr[0]값을 먼저 arrMin에 저장해놓고, for-loop를 1부터 시작하여 비교하는 방법도 가능하다.

## 파이썬 코드
``` python
arr=[5, 3, 7, 9, 2, 5, 2, 6]
arrMin=float('inf')
for i in range(len(arr)):
  if arr[i] < arrMin:
    arrMin = arr[i]
print(arrMin)
```
