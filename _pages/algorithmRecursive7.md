---
title: "알고리즘 기초 - Recursive(7)"
sidebar:
  nav: "docs"
permalink: /docs/algorithm/recursive7/
layout: single
---

## 멱집합

참고자료: [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/lecture/4078?tab=curriculum)

멱집합이란 임의의 집합에 대한 모든 부분집합을 뜻하며, n개의 데이터를 가지고있는 집합의 멱집합은 2^n개이다. 이를 재귀함수를 통해 구현하려면 이전 재귀함수의 경우와 마찬가지로 n-1의 모든 부분집합을 나열하고 그 모든 부분집합에 처음에 빼줬던 element를 추가한 집합들을 나열하면 된다. 예를들어, {a, b, c, d, e, f}의 멱집합은 a를 제외한 {b, c, d, e, f}의 멱집합에 a를 추가한 집합이 되는 것이다.

## 수도코드
```
powerSet(s)
if s is an empty set
  print nothing;
else
  let t be the first element of s;
  find all subsets of s-{t} by calling powerSet(s-{t});
  print the subsets;
  print the subsets with adding t;
```
이 코드의 베이스케이스는 공집합일 경우 아무것도 출력하지 않는 것이다. 공집합이 아니라면 위에서 설명한 것처럼 s에서 t를 제외한 나머지 집합의 모든 부분집합을 재귀함수를 통해 구하고 그 결과에 t를 더해주면 된다. 하지만 이 수도코드에는 문제점이 있다. 바로 호출한 재귀함수가 값을 반환하지 않는다는 것이다. 따라서 이러한 방식으로 코드를 구현하려면 멱집합을 구하는 powerSet함수가 여러 개의 집합들을 return해야한다(return을 해야 해당 값을 메모리에 저장하든, 또는 단순 출력만하든이 가능해진다).

```
powerSet(p, s)
if s is an empty set
  print p;
else
  let t be the first element of s;
  powerSet(p, s-{t})
  powerSet(pU{t}, s-{t})
```
이 코드를 보면 s의 멱집합을 구한 후, 각각에 집합 p를 합집합하여 출력하는 것이다. 즉, 두 번째 집합의 모든 부분집합들에 첫번째 집합을 합집합하여 출력하면 된다. 그렇다면 집합 p, s를 이해해야하는데, 이 때는 k라는 기준만 있으면 쉽게 이해할 수 있다. 예를들면 {a, b, c, d, e, f}집합이 있을때 집합 s는 항상 k부터 마지막 원소를 갖는다. k가 2라면 {c, d, e, f}가 될 것이다. 반대로 집합 p는 첫번째 원소로부터  k-1까지의 원소 중 일부를 갖는 집합을 의미하고, 이 경우에는 {a, b}가 될 것이다.

## 코드구현

``` swift
var data = ["a","b","c","d","e","f"]
var n = data.count
var include = [Bool](repeating: false, count: n+1)

func powerSet(_ k: Int) {
    if k==n {
        for i in 0..<n {
            if include[i] {
                print(data[i] + " ")
            }
        }
        print()
        return
    }
    include[k] = false
    powerSet(k + 1)
    include[k] = true
    powerSet(k + 1)
}
```
include 변수를 통해 해당 element가 포함될 경우와 포함되지 않을 경우를 모두 가정하여 재귀함수를 호출한다. include가 true라면 포함할 때, false라면 포함하지 않을 때이다. data, n include는 전역변수로 활용하여 매개변수의 역할을 할 수 있도록 코드를 작성하였다.
