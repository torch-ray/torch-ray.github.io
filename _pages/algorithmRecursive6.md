---
title: "알고리즘 기초 - Recursive(6)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/recursive6/
layout: single
---

## N Queens Problem

참고자료: [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/lecture/4077?tab=curriculum)

N x N 체스판이 주어진다. 체스판에 N개의 말을 서로 다른 행, 렬, 대각선 상에 있지 않게 둘 수 있는 프로그래밍을 작성하는 문제이다. 이 문제를 해결하기 위한 방법으로 Backtracking을 활용할 것이다. Backtracking이란 막다른 길까지 나아갔을 때, 다시 돌아가면서 가장 최근에 내렸던 결정부터 번복하는 방법이다. 조금 더 이해하기 쉽게 말하자면 아래와 같은 상태공간 트리를 DFS 방식으로 탐색하여 해를 찾는 알고리즘을 말한다.

<img width="723" alt="스크린샷 2021-01-29 오후 5 37 33" src="https://user-images.githubusercontent.com/74946802/106251797-c368c700-6258-11eb-90b3-b174adb40949.png">

위 그래프를 통해 예를들면, a에서 b를 선택해서 나아가고 b에서 e를 선택하여 나아갔다고 가정해보자. 이 때 h, i, j가 모두 조건에 맞지않다면 가장 최근에 내린 결정인 e를 번복하고 b로 돌아가는 것이다. 마찬가지로 f, g도 맞지 않다면 가장 최근에 내린 결정인 b를 번복하고 다시 a로 돌아가 c 또는 d로 나아가게 되는 방식이 Backtracking이라고 생각하면 된다.

## 코드 설계

```
return-type queens( arguments )
{
  if non-promising
    report failure and return;
  else if success
   report answer and return;
  else
   visit children recursivley;
}
```

코드는 간단하다. 더 이상 나아갈 수 없을 때(non-promising) 돌아가고, 맞는 위치라면(success) 정답을 반환하면 된다. 그리고 위 조건 중 어떤 조건에도 필터되지 않았다면 자식 노드를 재귀함수를 호출하여 반복하면 된다.

```
int [] cols = new int [N + 1];
boolean queens( int level )
{
  if non-promising
    report failure and return;
  else if success
   report answer and return;
  else
   visit children recursivley;
}
```

## 코드 구현

조금 더 상세하게 살펴보면, 매개변수로 행(level, 트리의 레벨)을 전달하고 열(cols)을 전역변수로 선언하여 문제를 해결할 수 있다. 이를 바탕으로 생각해보면 현재 level 2를 기준으로 재귀함수를 통해 다음 위치를 탐색하고 있다면 level 2까지의 말의 위치는 정해져있다는 뜻이다. 리턴 타입은 boolean으로 선언하였는데 이후 필요한 리턴값에 따라 변경이 가능한 부분이다.

``` swift
func queens(_ level:Int) -> Bool {
    if !(promising(level)) {
        return false
    } else if level == N {
        return true
    }
    for i in 0...N {
        cols[level + 1] = i
        if queens(level+1) {
            return true
        }
    }
    return false
}
```

그 다음 부분을 구현해보면 non-promising이 아니라면 false를 반환하도록 설정한다. 그 다음으로는 promising test코드를 통과한 level값이 n과 일치하는지 여부를 판단하는 것이다. n과 일치한다면 모든 말이 자리에 놓였다는 의미이기 때문에 true를 반환한다. 마지막으로 앞선 조건문에 모두 걸리지 않은 경우를 재귀함수를 통해 검증하면 된다. level+1이 true를 반환하게되면 다른 방법을 시도할 필요가 없으니 true를 반환하고 끝내면된다. 그렇지 않다면 다시 for문을 반복하는 형식이다. N개의 열을 모두 시도했지만 실패했을 경우 마지막 return false에 도달하기 때문에, 이때는 false를 반환하게 된다.

``` swift
func promising(_ level:Int) -> Bool {
    for i in 0..<level {
        if cols[i] == cols[level] {
            return false
        } else if level - i == abs(cols[level] - cols[i]){
            return false
        }
    }
    return true
}
```
마지막으로 promising test를 구현하면된다. 첫 번째 if문은 i번째 말이 level번째 말과 같은 '열'에 있는지를 검사하는 단계다. 서로 같은 열에 있다면 cols[i]와 cols[level]이 같을 것이고 그렇게되면 false를 반환한다. 다음으로 같은 열이 아니더라도 대각선상에 놓여있다면 false를 반환해야한다. level번째 말과 i번째 말의 대각선상의 유무는 level - i 의 거리가 |cols[level]-cols[i]|와 같은지 여부를 통해서 알 수 있다. 절대값을 취하는 이유는 둘 중 어느 값이 더 큰지 알 수 없기 때문이다.

## 전체코드
``` swift
var cols = [Int]()
var N = 8

func promising(_ level:Int) -> Bool {
    for i in 0..<level {
        if cols[i] == cols[level] {
            return false
        } else if level - i == abs(cols[level] - cols[i]){
            return false
        }
    }
    return true
}

func queens(_ level:Int) -> Bool {
    if !(promising(level)) {
        return false
    } else if level == N {
        return true
    }
    for i in 0...N {
        cols[level + 1] = i
        if queens(level+1) {
            return true
        }
    }
    return false
}
```
