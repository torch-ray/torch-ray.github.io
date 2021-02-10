---
title: "알고리즘 기초 - 탐색&시뮬레이션(3)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/search3/
layout: single
---

## 카드 역배치

참고자료: [파이썬 알고리즘 문제풀이](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/lecture/26923?tab=curriculum)

상기 강의 내용을 바탕으로 swift 코드로 바꿔서 요약 정리한 내용입니다.

- 문제

1 ~ 20까지의 숫자가 적힌 카드가 놓여있을 때, 각 카드의 위치는 자신의 번호대로 갖는다. 1번카드는 1번에, 4번은 4번, 20번은 20번이다. 이 때, 1 <= a < b <= 20 사의 두 수 a, b가 주어지면 해당 구간의 숫자를 역순으로 재배치한다. a, b 두 수는 10번 주어지며 10번이 모두 적용된 후의 수를 출력하면 된다.

- 입력예제

5 10  
9 13  
1 2  
3 4  
5 6  
1 2  
3 4  
5 6  
1 20  
1 20  

- 출력예제

1 2 3 4 10 9 8 7 13 12 11 5 6 14 15 16 17 18 19 20

## 내 풀이
``` swift
var n = Array(1...20)
for _ in 0..<10 {
    let m = readLine()!.split{$0==" "}.map{Int($0)!}
    n[m[0]-1...m[1]-1].reverse()
}
n.forEach{print($0, terminator:" ")}
```
1부터 20까지의 수를 갖는 배열 n을 생성한 뒤에, for-loop를 10번 돌면서 구간을 입력받는다. 해당 구간을 인덱스로 계산해야하기 때문에 각 값에서 1을 빼준 값을 reverse를 활용하여 역순으로 배치한 후 결과 값을 출력한다.

## 강의 풀이
``` swift
var a = Array(0...20)
for _ in 0..<10 {
    let m = readLine()!.split{$0==" "}.map{Int($0)!}
    let (s, e) = (m[0], m[1])
    for i in 0..<(e-s+1)/2 {
        (a[s+i], a[e-i]) = (a[e-i], a[s+i])
    }
}
a.removeFirst()
for x in a{
    print(x, terminator:" ")
}
```
강의 주제에 맞게 탐색을 활용하여 풀이를 진행하였다. 내 풀이는 단순히 문제만 해결하려다보니 주제를 잊었던 것 같다. 추후 풀이부터는 탐색을 통해 문제를 풀어보도록 해야겠다. 풀이 방식은 간단하다. 0부터 20까지의 배열을 생성하여 각 숫자에게 각 숫자에 해당하는 인덱스를 부여한다. 이후 역배치해야하는 구간을 s, e에 저장하고 (e-s+1)을 2로 나눈 몫만큼 for-loop를 반복한다. 5부터 8을 바꾼다고할 때, 5, 6, 7, 8이면 5와 8을바꾸고 6과 7을 바꾸면되기 때문에 2번만 for-loop로 탐색하면 되기 때문이다. 각 인덱스에 해당하는 수를 서로 바꿔(스왑)주고, 0을 제거한다. 역배치가 완료된 a배열을 for-loop를 돌면서 각 원소를 출력한다.

## 파이썬 코드
``` python
a=list(range(21))
for _ in range(10):
    s, e = map(int, input().split())
    for i in range((e-s+1)//2):
        a[s+i], a[e-i] = a[e-i], a[s+i]
a.pop(0)
for x in a:
    print(x, end=' ')
```
