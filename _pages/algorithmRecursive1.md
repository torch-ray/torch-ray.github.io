---
title: "알고리즘 기초 - Recursive(1)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/recursive1/
layout: single
---

## 순환의 개념이해하기

참고자료: [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/lecture/4072?tab=curriculum)

Recursion은 순환 또는 재귀라고 한다. 일반적으로 우리가 말하는 재귀함수는 자기 자신을 호출하는 함수이다. 간단한 예시를 통해 살펴보자.

``` swift
func recursive() {
  print(1)
  recursive()
}
```

recursive함수는 1을 print하고 자기 자신을 호출하는 함수이다. 1을 출력하고 자기자신을 호출하고, 호출된 recursive함수는 또 1을 출력한 뒤에 자기 자신을 호출한다. 이러한 과정이 반복되기 때문에 해당 함수를 실행하면 무한루프에 빠지게된다. (끝나지 않고 계속 1을 출력하고 자기자신을 호출하는 상황) 그렇다면 재귀함수는 항상 무한루프에 빠지게될까? 꼭 그렇지는 않다.

``` swift
func recursive2(n: Int) {
    if n <= 0 {
        return
    } else {
        print("Hello")
        recursive2(n: n-1)
    }
}
```

recursive2 함수에 4를 입력해보면, Hello를 4번 입력하고 함수가 종료된다. 어떤 원리인지 살펴보면, 입력값 4는 if문에서 0보다 작거나 같은지(0 이하)비교되고 0이하면 함수가 종료되고, 그렇지 않으면 else문으로 넘어간다. 4는 0보다 크기 때문에 Hello를 출력하고 -1을 한채로(4 - 1 = 3) 다시 recursive2함수로 입력된다(재귀함수). 위 과정과 마찬가지로 입력값 3은 0보다 작거나 같을 때까지 위 과정을 반복한다. 즉 Hello를 4번출력하고 4가 0이된 순간 함수를 종료한다.

즉, 재귀함수가 무한루프에 빠지지 않기 위해서는 두 가지 조건이 필요하다. 첫번째로 recursion에 빠지지 않는 경우가 적어도 하나는 존재해야한다(BaseCase). 두번째로 recursion을 반복하다보면 결국 BaseCase로 수렴해야 한다. 이를 활용하면 아래와 같이 recursion을 활용하여 factorial을 구현할 수 있다.

``` swift
func factorial(n: Int) -> Int {
    if n == 0 {
        return 1
    } else {
        return n * factorial(n: n-1)
    }
}
```
BaseCase는 n이 0인 경우이다. 0팩토리얼은 1이기 때문에 n이 0인경우 1을 리턴하고 종료한다. n이 0이 아닌 경우(음수제외)는 n에 (n-1)!값을 곱해서 리턴한다. 물론 n에 (n-1)!이 곱해지기 전에 (n-1)!값이 먼저 구해진다(재귀함수를 반복하면서 n이 0이될때까지 1씩 감소한다).

재귀함수는 팩토리얼 외에도 피보나치 수열, 최대공약수 등 다양한 기능을 구현하는데 사용될 수 있다. 마지막으로 최대공약수를 재귀함수를 통해 구할 수 있는지 살펴보겠다.

``` swift
func gcd(m: Int, n: Int) -> Int {
    let a = max(m, n)
    let b = min(m, n)

    if a % b == 0 {
        return b
    } else {
        return gcd(m: b, n: a % b)
    }
}
```

해당 코드는 이해하기 약간 복잡할 수 있지만, 실제로 코드를 따라가보면 크게 복잡하지는 않다. 재귀함수에서는 BaseCase를 찾으면 함수를 쉽게 읽어낼 수 있는데, 위 함수의 경우에는 당연히 a % b == 0 일때 b값을 리턴하는 부분이 BaseCase이다. 입력된 두 수 중에서 큰 수가 작은 수의 배수라면, 두 수의 최대공약수는 작은 수가된다. 배수가 아닌 경우 재귀함수가 호출되고 a % b == 0의 조건문이 만족될 때까지 반복된다. 왜 a % b값을 넣는지는 여러 숫자를 입력하고 계산해보면 쉽게 알게 될 것이다.

오늘은 Recursion의 기초 개념에 대해 학습해봤다. 다음 시간에도 이어서 Recursion의 조금 더 심화된 개념에 대해 학습해볼 것이다.
