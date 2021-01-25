---
title: "프로그래머스 모의고사 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/programmers/test/
layout: single
---

## 프로그래머스 - 모의고사

<img width="1227" alt="스크린샷 2021-01-25 오후 7 47 31" src="https://user-images.githubusercontent.com/74946802/105696086-323add00-5f46-11eb-8327-8545be9e57d0.png">

수포자 1, 2, 3이 찍은 답과 주어진 정답을 비교하여 가장 많은 문제를 맞춘 사람을 찾는 문제다.

- 체크포인트: 주어진 반복 패턴을 벗어나는 경우를 대비하여 나머지 연산을 해준다.

## 수포자 패턴 입력
``` swift
func solution(_ answer:[Int]) -> [Int] {
  let usrNumber = [[1, 2, 3, 4, 5],
  [2, 1, 2, 3, 2, 4, 2, 5],
  [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]]
  var winner = [Int]()
  var count = [0, 0, 0]
}
```
수포자의 찍기 반복 패턴을 입력한다. 추가적으로 정답을 담아 반환할 변수와, 각 몇문제를 맞췄는지 카운팅 할 변수를 선언한다.

## 정답체크
``` swift
for i in 0..<answer.count {
  if answers[i] == usrNumber[0][i%usrNumber[0].count] {count[0]+=1}
  if answers[i] == usrNumber[1][i%usrNumber[1].count] {count[1]+=1}
  if answers[i] == usrNumber[2][i%usrNumber[2].count] {count[2]+=1}
}
```
정답의 길이만큼 for-loop를 돌면서 수포자의 답과 정답을 하나씩 비교하여 맞은 경우 해당 수포자의 카운트값을 + 1 해준다. 본 문제에서 가장 중요한 파트인데, i를 반드시 해당 수포자의 정답 패턴의 길이로 나눠서 나머지 연산을 해줘야한다. 예를들면, 첫번째 수포자는 [1, 2, 3, 4, 5]로 패턴의 길이가 5인데, 문제수가 6개만 주어져도 나머지 처리를 하지 않는다면 인덱스 6을 찾아야하기 때문에 index 에러가 발생한다. 문제 수가 정답패턴을 초과하는 경우를 대비하여 나머지 연산처리를 해준다.

## 최대값 체크
``` swift
let maxNum = count.max()!

for i in 0..<count.count {
  if maxNum == count[i] {
    winner.append(i+1)
  }
  return winner
}

```
각 수포자별로 정답을 맞춘 횟수가 담긴 count배열에서 최대값을 찾아서 최대값과, 정답을 맞춘 횟수를 비교한다. 항상 index 0번부터 비교하기 때문에 1등이 여러명일 경우 자동적으로 정렬된 값을 반환한다. 0번 index를 가지고 있는 수포자는 수포자 1이기 때문에 index i값에 + 1을 하여 정답 배열에 추가한다.

## 전체코드
``` swift
import Foundation

func solution(_ answers:[Int]) -> [Int] {
    let usrNumber = [[1, 2, 3, 4, 5],
     [2, 1, 2, 3, 2, 4, 2, 5],
      [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]]
    var winner = [Int]()
    var count = [0, 0, 0]

    for i in 0..<answers.count {
        if answers[i] == usrNumber[0][i%usrNumber[0].count] {count[0]+=1}
        if answers[i] == usrNumber[1][i%usrNumber[1].count] {count[1]+=1}
        if answers[i] == usrNumber[2][i%usrNumber[2].count] {count[2]+=1}
    }

    let maxNum = count.max()!

    for i in 0..<count.count {
        if maxNum == count[i] {
            winner.append(i+1)
        }
    }
    return winner
}
```
