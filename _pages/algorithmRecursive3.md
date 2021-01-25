---
title: "알고리즘 기초 - Recursive(3)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/recursive3/
layout: single
---

## 순환 알고리즘의 설계

참고자료: [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/lecture/4073?tab=curriculum)

Recursion을 작성할 때 어떤 방법으로, 어떤 요령을 통해 설계할 수 있는가?

## Base Case

- Recursion 함수의 가장 기본적 형태는 반드시 BaseCase를 가져야한다.
- 모든 다른 케이스는 결국 BaseCase로 수렴해야한다.

## 암시적 매개변수와 명시적 매개변수

- 순차탐색(sequential search)  

``` swift
func search(_ data:[Int], _ n: Int, target: Int) -> Int {
    for i in 0..<n {
        if data[i] == target {
            return i
        }
    }
    return -1
}
```
data[0]에서 data[n-1]사이의 target을 검색하는 코드이다. n-1까지 탐색하라는 것은 주어진 데이터 n에의해 명시적으로 제시되지만 검색 구간의 시작 인덱스인 0은 보통 생략한다. 암묵적으로 당연히 0부터 시작한다고 생각되는 것, 즉 암시적 매개변수이다. 이렇게 Recursion이 아닌 코드에서는 굳이 매개변수를 늘릴 이유가 없기 때문에 암시적인 매개변수를 사용하는 것이 깔끔하고 좋을 수 있다. 하지만 Recursion에서는 그렇지 않다.

- 암시적 매개변수를 명시적 매개변수로!  

``` swift
func search(_ data:[Int], _ begin:Int, _ end:Int, _ target: Int) -> Int {
    if begin>end {return -1}
    else if target == data[begin] {return begin}
    else {return search(data, begin+1, end, target)}
}
```
이전 함수와의 차이점은 끝나는 점뿐만 아니라 시작점까지 명시적으로 매개변수로 제시됐다는 점이다. 그렇다면 왜 이런식으로 설계해야 할까? Recursion의 시작은 사실 크게 다르지 않다. begin에 0이 들어오면 암시적으로 0부터 시작하나, 명시적으로 0에서 시작하나 차이점이 없기 때문이다. 하지만 이후 자기 자신을 호출 할 때 상황이 달라진다. 0에서 부터 탐색한 값을 이제는 1에서 부터 탐색하도록 바꿔야 코드가 성립하기 때문이다. 이렇게 Recursion은 시작 할 때 뿐만 아니라, 자기 자신을 호출할 때의 상황까지 고려해서 코드를 설계해야 한다.

- 이진검색(binary search)  

``` swift
func binarySearch(_ data:[Int], _ target:Int, _ begin:Int, _ end: Int) -> Int {
    if begin > end {return -1}
    else {
        let middle = (begin + end) / 2
        if target == data[middle] { return data[middle]}
        else if target > data[middle] {
          return binarySearch(data, target, middle+1, end)
        }
        else {return binarySearch(data, target, begin, middle-1)}
    }
}
```
Recursion을 활용하여 이진검색을 설계할 때도 마찬가지이다. 암시적인 매개변수를 사용할 경우 자기 자신을 호출하는 부분을 구현할 수 없게된다. 이처럼 Recursion을 활용하여 코드를 설계할 때는 BaseCase뿐만 아니라, 필요에 따라 매개변수를 명시적으로 사용할 필요가 있다.
