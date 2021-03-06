---
title: "백준 1052번 with Swift"
sidebar:
  nav: "docs"
permalink: /docs/baekjoon/1052/
layout: single
---

## 백준 - 물병

<img width="1182" alt="스크린샷 2021-01-13 오전 9 01 13" src="https://user-images.githubusercontent.com/74946802/104389153-229eba00-557e-11eb-831f-39ba32e3ffef.png">

항상 문제를 난해하게 설명하는 백준, 그 중 끝판왕이 아닌가 싶은 문제다. 뭘 하라는 건지 잘 생각해보지 않으면 이해하기 어렵다. 결론은 주어진 물병의 수 N개를 합쳐서 K개를 넘지 않게 만들어야 하는 문제다. 조건은 물병을 합치기 위해서는 서로 합치려는 물병에 들어있는 물의 양이 같아야 한다. 즉 1L가 들어있는 물병과 2L가 들어있는 물병은 합칠 수 없다. 두 물병을 하나로 합치려면 1L 물병을 구매해서 기존의 1L 물병과 합쳐 2L 물병을 만든 후에, 기존의 2L 물병과 합쳐야 한다. N개의 물병을 합쳐 K개를 넘지 않게 만들기 위해 총 몇 병의 물병을 구매해야하는 지를 묻는 문제이다.
- 체크포인트1: 2의 제곱 수(2, 4, 8, 16...)의 물병이 주어지면 무조건 1개의 물병으로 만들 수 있다.
- 체크포인트2: 주어진 N개의 물병의 수보다 K가 클 경우에는 바로 0을 출력하면 된다.
- 체크포인트3: K는 1,000보다 작거나 같은 자연수이다.

## N과 K를 입력
``` swift
let input = readLine()!.split(separator: " ").compactMap{Int($0)}
var n = input[0]
var k = input[1]
```
separator: " "를 통해서 공백을 기준으로 값을 나눠서 입력받는다. compactMap을 활용하여 옵셔널 값을 Unwrapping함과 동시에 Int()로 모든 element를 정수화 한다. 첫번째 값을 n, 두번째 값을 k에 저장한다.

## 주어진 물병의 수를 최대한으로 합치는 함수
``` swift
func maxMergeNum(_ num: Int) -> {
  var answer = 0
  var number = num

  while true {
    let a = number / 2
    let b = number % 2
    answer += b
    number = a
    if number == 0 {
      break
    }
  }
  return answer
}
```
이 함수를 이해하는 것이 본 문제 풀이의 핵심이다. 예를들어 주어진 물병의 수 n이 5라고 가정해보자. 이 n을 maxMergeNum 함수로 넘기면 while문이 반복된다. a에는 5를 2로 나눈 몫 2를 넣고, b에는 그 나머지 1을 넣는다. 변수 answer에는 b값을 그대로 더해준다(이 부분을 기억해야한다). 그리고 number에 다시 a값을 대입한다. 즉, a는 number를 2로 나눈 몫을 가지고있기 위한 임시 변수라고 생각하면 된다. 그럼 다시 반복문이 실행되는데(아직 number가 0이 아니기 때문에 종료되지 않는다), 이번에는 2를 2로 나눈 몫 1을 a에 넣고, b에는 그 나머지인 0을 넣는다. 여기서 answer에는 b(즉, 0)를 더하기 때문에 answer값이 변하지 않는다. 다시 한 번 반복문을 돌면 1을 2로 나눈 몫인 0을 a에 넣고, b에는 그 나머지인 1을 넣는다. answer에 b값을 더하면 answer는 2가된다. 그리고 여기서 number가 0이되면서 반복문이 종료되면서 answer를 리턴한다.

위 함수를 이해하기 위해 다시 한 번 핵심포인트를 정리하자면, 모든 수는 2로 나눌 경우 나머지가 1또는 0이다. 이 함수의 포인트는 나머지가 1인 경우를 카운트하는 것이다. 나머지가 1인 경우를 카운트하면 어떤수의 물병을 합쳤을 때 최대로 줄일 수 있는 물병의 수와 같다. 다시말하면, 물병 5병이 다음과 같이 주어졌을 때 [1, 1, 1, 1, 1] 이것을 한 번 합치면 [2, 2, 1]과 같이 3병으로 합쳐진다. 이를 다시 한 번 합치면 [4, 1]로 총 2병으로 합쳐진다. 2와 1, 4와 1을 합칠 수 없는 이유는 앞서 언급한 같은 양의 물을 가진 물병끼리만 합칠 수 있다는 조건 때문이다. 5가 0이 될때까지 2로 나눌경우 1이 나머지로 나타나는 경우를 세어보면 2번이다. 즉, 어떤 수의 물병이 주어졌을 때 그것을 최대로 줄일 수 있는 물병의 수와 그 수를 0이 될 때까지 나눠서 나머지가 1인 경우를 세어보면 결과가 같다는 것이다.

그럼 5의 경우는 2를 리턴하게 되는데 이 2를 처음에 주어진 k와 비교해주면 된다.

## 예외처리
``` swift
if n <= k {
  print(0)
}
```
전 단계의 함수가 리턴한 값을 k와 비교하기에 앞서서 예외처리를 해줘야한다. 체크포인트에서 설명한대로 주어진 물병의 수 n보다 K가 큰 경우에는 n을 줄이기 위한 어떠한 시도도 할 필요가 없기 때문에 추가로 물병을 구매할 필요가 없다. 즉, 바로 0을 출력하면 된다.

## 추가로 필요한 물병의 수
``` swift
if n <= k {
  print(0)
} else {
  var cnt = n
  while true {
    if maxMergeNum(cnt) <= k {
      print(cnt - n)
      break
    } else {
      cnt += 1
    }
  }
}
```

물병 문제를 풀이하기 위한 마지막 단계이다. if문은 전 단계에서 설명한 예외처리부분이기 때문에 신경쓰지 않고 else문 부터 확인하면 된다. 일단 임시변수 cnt에 주어진 물병의 수 n을 입력한다. 그리고 while문을 반복하며 maxMergeNum(cnt)값이 k보다 작거나 같은지를 확인하며 된다. maxMergeNum(cnt) 부분은 본 문제의 핵심 부분으로 이전 단계에서 설명한 바와 같다. 즉 5를 입력할 경우 2를 리턴하는 함수이다. k값이 1이라고 가정해보자. 그렇다면 k값이 더 작기 때문에 while문은 종료되지 않고 cnt += 1 코드가 실행된다. 그럼 다시 maxMergeNum(6)이 실행되고 2를 리턴하기 때문에(k값보다 크기 때문에), cnt값이 1증가하고 maxMergeNum(7)이 실행된다. maxMergeNum(7)은 3을 리턴하기 때문에 cnt값이 증가하여 maxMergeNum(8)이 실행되고 maxMergeNum(8)은 1을 리턴한다. 드디어 k값 이하의 값이 리턴됐다. while문은 최종 cnt값인 8에서 처음에 주어진 n(즉, 5)을 뺀 값인 3을 출력하며 종료된다. 다시말하자면 5병을 1병으로 합치기 위해서 추가로 구매해야하는 물병은 3개인 것이다.

체크포인트에서 확인한대로 2의 제곱수는 모두 1병으로 합쳐질 수 있고, k는 자연수라는 조건때문에 물병 문제는 정답이 없어서 -1을 리턴하는 경우는 생기지 않는다. k가 아무리 작아도 1이고 주어진 물병의 수는 1씩 더하다보면 2의 제곱수가 되는 순간이 생기기 때문이다.

## 전체코드
<img width="523" alt="스크린샷 2021-01-13 오전 9 40 02" src="https://user-images.githubusercontent.com/74946802/104391514-5b8d5d80-5583-11eb-8369-bed3485efba7.png">
