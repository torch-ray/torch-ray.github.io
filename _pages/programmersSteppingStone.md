---
title: "프로그래머스 징검다리 건너기 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/programmers/steppingstone/
layout: single
---

## 프로그래머스 - 징검다리 건너기

<img width="1033" alt="스크린샷 2021-02-07 오후 9 01 31" src="https://user-images.githubusercontent.com/74946802/107145864-dc275a00-6987-11eb-89df-e1b6ef374c3a.png">
<img width="1033" alt="스크린샷 2021-02-07 오후 9 01 44" src="https://user-images.githubusercontent.com/74946802/107145870-e77a8580-6987-11eb-8357-d0afa59470ce.png">
<img width="1033" alt="스크린샷 2021-02-07 오후 9 01 59" src="https://user-images.githubusercontent.com/74946802/107145881-f2cdb100-6987-11eb-94b8-8c891f2fe534.png">
<img width="1033" alt="스크린샷 2021-02-07 오후 9 02 20" src="https://user-images.githubusercontent.com/74946802/107145884-fbbe8280-6987-11eb-83c5-5e3dd3b89caf.png">


[2, 4, 5, 3, 2, 1, 4, 2, 5, 1]의 형태로 징검다리가 주어질 때, 최대 몇명이 징검다리를 건널 수 있는지 구하는 문제다. 한 명이 건널때마다 징검다리의 숫자는 1씩 줄어든다. 또한, 한 번에 점프로 뛰어넘을 수 있는 징검다리의 수는 k로 제한되며 다음으로 밟을 수 있는 돌이 여러 개일 경우 무조건 가장 가까운 디딤돌로 건너 뛴다.

- 체크포인트1: 효율성 테스트를 고려하여 시간복잡도 설계를 잘해야 한다.
- 체크포인트2: 이분탐색을 활용한다.

## 이분탐색을 위한 최대값, 최소값 생성
``` swift
func solution(_ stones:[Int], _ k: Int) -> Int {
    var answer = 0
    var left = 1
    var right = stones.max()!
}    
```
정답을 리턴할 변수 answer와 이분탐색을 진행할 최소값, 최대값을 만들어준다. 문제에서 가장 작은 수를 1로 언급했기 때문에 최소값은 1이되며, 최대값의 경우 stones에서 가장 큰 값으로 설정한다.

## 건널 수 있는 최대 인원수 확인
``` swift
func jumpCheck(_ stones:[Int], _ k: Int, _ number: Int) -> Bool {
    var jump = k
    for i in stones {
        if i < number {
            jump -= 1
            if jump == 0 {
                return false
            }
        } else {
            jump = k
        }
    }
    return true
}
```
징검다리와, 최대점프 가능 수, 점프인원(이전 함수의 mid값)을 인자로 전달 받아서, 전달받은 점프인원만큼 징검다리를 건널 수 있는지 없는지 여부를 반환한다. 먼저 점프 가능 수를 jump 변수에 저장하고 징검다리(stones)를 for-loop로 돌면서 각 돌멩이의 수가 점프인원보다 작은 경우에만 점프횟수를 차감한다. 돌멩이의 숫자가 연속적으로 number보다 작은 경우에만 0에 도달하기 때문에 이 때는 해당 인원만큼 건널 수 없다는 뜻이되어 false를 반환한다. 연속적인 경우에만 불가능한 것이기 때문에(연속적이지 않으면 k만큼의 점프력으로 건너뛸 수 있음) else문에서는 jump 횟수를 k로 초기화시킬 수 있도록 한다. 해당 for문을 return없이 통과하였다면, 주어진 number는 건널 수 있다는 의미가 되어 true를 반환해준다.

## 이분탐색을 진행할 반복문
``` swift
while left <= right {
  let mid = (left + right) / 2
  if jumpCheck(stones, k, mid) {
    answer = mid
    left = mid + 1
    } else {
      right = mid - 1
    }
  }
  return answer
```
while-loop를 최소값이 최대값과 같거나 작을 경우까지 돌면서 mid값을 기준으로 jumpCheck함수를 통해 최대 몇 명까지 징검다리를 건널 수 있는지 확인한다. 건널 수 있는 경우 true를 반환하는데 이 때는 최소값을 증가시켜 건널 수 있는 인원을 늘려서 확인해보고, false를 반환하면 mid값만큼 건널 수 없다는 뜻이기 때문에 mid값을 줄여서 확인해본다.

## 전체코드
``` swift
func jumpCheck(_ stones:[Int], _ k: Int, _ number: Int) -> Bool {
    var jump = k
    for i in stones {
        if i < number {
            jump -= 1
            if jump == 0 {
                return false
            }
        } else {
            jump = k
        }
    }
    return true
}
func solution(_ stones:[Int], _ k: Int) -> Int {
    var answer = 0
    var left = 1
    var right = stones.max()!

    while left <= right {
        let mid = (left + right) / 2

        if jumpCheck(stones, k, mid) {
            answer = mid
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return answer
}
```
