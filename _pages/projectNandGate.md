---
title: "CPU만들기1 - NandGate"
permalink: /docs/project/nandgate/
layout: single
---

## 논리회로 학습하기 with NandGate  

- NandGate(Negative-AND)는 말그대로 AND연산과 반대되는 개념이다.
모든 입력이 True일때만 True를 출력하는 And와는 반대로, 모든 입력이 True일때 False를 출력한다.
즉, NandGate는 [False, False], [True, False], [False, True]값에 대해서 모두 True를 출력한다.
NandGate의 예시는 아래 그림과 같다.

<img width="400" alt="스크린샷 2021-01-11 오후 7 24 44" src="https://user-images.githubusercontent.com/74946802/104169307-b3707b00-5442-11eb-94d6-301dac850831.png">

- CPU를 만들기 위해서는 논리회로를 이해하는 것이 필수인데, 오늘은 NandGate를 활용하여 다른 Gate를 만들어봄으로써 논리회로에 대해 학습하려고한다.

- AndGate 만들기  
NandGate로 어떻게 하면 AndGate를 만들 수 있을까? AndGate는 모든 출력값이 True일때만 True를 출력한다. 그렇다면 NandGate 두 개를 이어 붙여서 첫번째 NandGate의 출력값을 두번째 NandGate의 입력값으로 보내주면 될 것이다.
말이 조금 복잡할 수 있는데, 아래 그림을 통해 이해하면 훨씬 쉬울 것이다.

<img width="487" alt="스크린샷 2021-01-11 오후 7 28 05" src="https://user-images.githubusercontent.com/74946802/104169611-2c6fd280-5443-11eb-9ea4-064c233afbe8.png">

- 그림을 살펴보면 [False, False] 입력값을 통해 최종적으로 False를 출력하는 것을 알 수 있다. 입력값을 [False, True]로 바꾸더라도 첫번째 NandGate는 [True]를 출력할 것이고, 모든 값을 True로 입력받은 두번째 NandGate는 False를 출력할 것이다. 오직 [True, True]값을 입력해야(중간 출력 값이 False) 최종 출력 값이 True를 출력하는 것으로 보아 위 그림은 AndGate와 똑같은 역할을 하고 있음을 알 수 있다.

- OrGate 만들기  
앞서 NandGate를 활용하여 AndGate를 만들어봤기 때문에 OrGate는 비교적 쉽게 만들 수 있을 것이다. 먼저 두 Gate의 차이점을 찾아야 하는데, Nand와 Or은 두 입력값이 True 혹은 False로 같을 때만 출력 값이 다르다. 즉, 두 Gate 모두 [False, True], [True, Flase]일때는 True를 출력한다. 이를 바탕으로 생각해보면 NandGate를 활용하여 OrGate를 만들기 위해서는 아래와 같이 총 3개의 NandGate가 필요하다.

 <img width="425" alt="스크린샷 2021-01-11 오후 7 33 24" src="https://user-images.githubusercontent.com/74946802/104170112-f717b480-5443-11eb-8d26-a6eb72a04a1e.png">

 - 그림을 살펴보면 입력값이 [True, False]일 때 최종적으로 True 값을 출력하는 것을 알 수 있다. 윗쪽 작은 NandGate는 True를 입력받아 False를 출력하고, 아래쪽 작은 NandGate는 False를 입력받아 True를 출력한다. 그리고 마지막 큰 NandGate가 각각의 값[False, True]을 입력받아 True를 출력한다. OrGate와 같은 결과이다. 마찬가지로 입력값이 [False, False]라면 아래 그림과 같이 False를 출력한다.

<img width="421" alt="스크린샷 2021-01-11 오후 7 33 38" src="https://user-images.githubusercontent.com/74946802/104170142-01d24980-5444-11eb-8398-ea08e3516470.png">

- 슬슬 복잡해지기 시작한다. 하지만 마지막 한 단계가 남았다. 조금만 더 집중해서 마지막 문제를 해결해보자.

- XOR Gate 만들기  
XOR은 입력값이 서로 다를 때만 True를 출력한다. 즉, 입력값이 [True, True]로 같거나 [False, False]로 같다면 모두 False를 출력한다. NandGate와의 차이점은 입력값이 [False, False]일 때, XOR은 False를 Nand는 True를 출력한다는 점에서 다르다. 나머지 입력에 대해서는 같은 결과값을 가진다. 그렇다면 이 차이점을 구현하기 위해서 필요한 NandGate는 몇 개일까? 눈치가 빠른 사람은 감이 왔겠지만(하나씩 늘어났으니...), 총 4개의 NandGate가 필요하다.

<img width="481" alt="스크린샷 2021-01-11 오후 7 46 08" src="https://user-images.githubusercontent.com/74946802/104171513-1d3e5400-5446-11eb-9ada-215c5799941c.png">

- 위 그림을 보면서 NandGate로 만든 XORGate의 논리회로를 따라가보자! 먼저, 첫번째 작은 NandGate에 [True, True]값이 입력되고, False를 출력하게된다. 여기서 출력된 False값은 각각 윗쪽 작은 NandGate와 아래쪽 작은 NandGate의 입력값 중 하나로 전달된다. 나머지 입력값은 첫번째 작은 NandGate로 입력됐던 최초의 입력값이 그대로 전달된다. 그렇게되면 윗쪽 작은 NandGate와 아래쪽 작은 NandGate 모두 [True, False]의 입력값을 받게된다. 그리고 두 Gate 모두 True를 출력하여 마지막 NandGate로 전달한다. 마지막 NandGate는 입력받은 [True, True]값을 False로 출력한다. 결국 XOR과 같은 결과를 출력하게 된다. 아래 그림도 입력값이 다를 뿐, 같은 과정을 통해 결과값을 출력한다.

<img width="463" alt="스크린샷 2021-01-11 오후 7 46 18" src="https://user-images.githubusercontent.com/74946802/104171543-26c7bc00-5446-11eb-9565-82b0fa5d5ddc.png">

- 오늘은 NandGate를 활용하여 다양한 Gate를 만들어봤다. 도대체 이게 CPU만들기와 무슨상관이 있을까 보일 수도 있지만, 논리회로에 대한 이해는 CPU만들기의 가장 기초 중에 기초다. 그리고 놀랍게도 오늘 살펴본 논리회로가 CPU동작원리의 모든 것이라고 볼 수 있을 정도니 다시 한 번 복습해보고 논리회로를 이해하자!
