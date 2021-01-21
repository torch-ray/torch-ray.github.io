---
title: "프로그래머스 크레인 인형뽑기 게임 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/programmers/cranedoll
layout: single
---

## 프로그래머스 - 크레인 인형뽑기 게임

<img width="714" alt="스크린샷 2021-01-21 오전 8 36 13" src="https://user-images.githubusercontent.com/74946802/105254202-5a33e480-5bc4-11eb-8908-d4644c261774.png">
<img width="712" alt="스크린샷 2021-01-21 오전 8 36 32" src="https://user-images.githubusercontent.com/74946802/105254228-6750d380-5bc4-11eb-9eb0-ce774e79647c.png">
<img width="724" alt="스크린샷 2021-01-21 오전 8 36 46" src="https://user-images.githubusercontent.com/74946802/105254245-70da3b80-5bc4-11eb-82b2-8738144993ca.png">

[[0,0,0,0,0],[0,0,1,0,3],[0,2,5,0,1],[4,2,4,4,2],[3,5,1,3,1]] 와 같은 형태로 인형이 담긴 배열이 주어진다. 0은 인형이 없다는 뜻이고 1, 2, 3 등의 정수는 인형의 종류를 나타낸다. 즉, 바구니에 [1, 1] 또는 [2, 2]와 같이 같은 종류의 인형이 들어갈 경우 두 인형이 터지면서 바구니에서 사라지게 된다. 이 때 터트려져 사라진 인형의 총 개수를 구하는 문제다.

- 체크포인트1: 문제를 잘 이해한다(배열을 어떻게 읽어야하는지 제대로 파악하지 않으면 테스트케이스는 통과해도 히든 케이스가 풀리지 않는다.)
- 체크포인트2: 인형을 뽑았다면 크레인 작동을 중지해야한다.

## 바구니 및 정답 변수 생성
``` swift
func solution(_ board:[[Int]], _ moves: [Int]) -> Int {
  var boards = board
  var basket = [Int]()
  var answer = 0
}
```
함수의 인풋값으로 들어오는 board의 경우 default 형태가 상수(let)이기 때문에 boards 변수를 선언하여 저장해둔다. 뽑기 인형에서 뽑은 인형을 담아둘 바구니(basket) 변수와 터트려져 사라진 인형의 수를 카운트해줄 answer 변수를 생성한다.

## 인형을 바구니에 옮겨 담으며 카운팅
``` swift
for i in moves {
  for j in 0..<boards.count {
    let pick = boards[j][i-1]
    if pick > 0 {
      if !basket.isEmpty && pick == basket[basket.count-1] {
        basket.popLast()
        answer += 2
      } else {
        basket.append(pick)
      }
      boards[j][i-1] = 0
      break
    }
  }
}
return answer
```
일단 몇번째 줄에 있는 인형을 뽑아야 할지 알기 위해서 for문으로 moves를 탐색한다. 동시에 이중 for문을 활용하여 boards 배열을 동시에 탐색한다. pick 상수에는 moves에서 원하는 인형의 값을 저장한다.  

중요한 포인트는 boards [i-1]과 [j]의 순서다. 입력값으로 주어지는 인형뽑기 기계의 상태, 즉 배열은 boards[i]가 같은 줄이 아니라 boards[j]가 같은 줄이다. boards[i]에는 가로로 같은 줄의 값이 들어간다는 뜻이다. 하지만 moves에서 주는 명령은, 예를들면 moves에서 1이라고 했을 때는 boards의 각 인덱스마다 해당되는 [0] 위치에 있는 인형을 탐색하여 뽑아오라는 뜻이다.  

뽑아온 값이 0이라면 첫번째 if문 이하는 아예 실행되지 않고 j문이 반복된다. 0보다 큰 경우(인형이 있는 경우)는 if문이 실행되고 basket에 같은값이 있으면 인형을 터트리고 answer에 터트린 인형의 수를 더해주며, 그렇지 않으면 해당 인형을 basket에 저장해준다. 이후 뽑은 위치의 값은 0으로 바꿔준다(인형을 뽑았기 때문에 빈칸으로 만들어줘야하기 때문). 그리고 반드시 break를 통해 loop를 중지해야한다. 중지하지 않으면 moves에서 1이라는 명령을 내렸을 때 한 번의 명령으로 첫번째 줄의 모든 인형을 뽑아서 basket에 담아버리게 된다.

## 전체코드
``` swift
import Foundation

func solution(_ board:[[Int]], _ moves:[Int]) -> Int {
    var boards = board
    var basket = [Int]()
    var answer = 0
    for i in moves {
        for j in 0..<boards.count {
            let pick = boards[j][i-1]
            if pick > 0 {
                if !basket.isEmpty && pick == basket[basket.count-1] {
                    basket.popLast()
                    answer += 2
                } else {
                    basket.append(pick)
                }
                boards[j][i-1] = 0
                break
            }
        }
    }
    return answer
}
```
