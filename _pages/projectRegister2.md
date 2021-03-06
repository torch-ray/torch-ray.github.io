---
title: "CPU만들기3 - Register간 데이터복사"
permalink: /docs/project/register2/
layout: single
---

## 레지스터간 데이터 복사

<img width="910" alt="스크린샷 2021-01-14 오후 5 36 32" src="https://user-images.githubusercontent.com/74946802/104569960-b1055f80-5694-11eb-8357-3d42fee4b84c.png">

이전 시간에 만든 8bit Register 2개를 활용하여, RegisterA(이하 RA)에서 RegisterB(이하 RB)로 데이터를 복사하는 과정에 대해 학습하고자 한다. 단순히 RA와 RB를 연결시킨다음 입력값을 넣으면 아래와 같이 버스(데이터가 이동하는 통로)에서 충돌이 일어난다. 그림에서 볼 수 있듯이 입력값과 출력값이 연결되어 있기 때문에 어느 값이 어디로 입력 또는 출력되는지 알 수 없기 때문이다.

<img width="917" alt="스크린샷 2021-01-14 오후 5 36 56" src="https://user-images.githubusercontent.com/74946802/104570032-c4b0c600-5694-11eb-99dd-ede8d2b95356.png">

이것을 방지하기 위해 버퍼가 필요하다. 버퍼는 입력값을 받으면 지연시켜서 출력하는 장치인데, 데이터 충돌을 막기위해 필요한 버퍼는 단순한 버퍼는 아니고 Controlled Buffer이다. 즉 데이터를 제어할 수 있는 버퍼장치가 필요하다.

<img width="314" alt="스크린샷 2021-01-14 오후 5 41 20" src="https://user-images.githubusercontent.com/74946802/104570109-ddb97700-5694-11eb-930f-3d47c4130a9e.png">
<img width="336" alt="스크린샷 2021-01-14 오후 5 41 37" src="https://user-images.githubusercontent.com/74946802/104570155-ead66600-5694-11eb-87d3-6b08173bc725.png">

컨트롤 버퍼는 컨트롤 비트가 0일 때는 입력과 출력이 끊긴다. 입력이 0일 때, 출력이 0이되는 것이 아니라 아예 연결 자체가 끊긴다. 컨트롤 비트를 켜주면 입력값이 0일 때는 0을 출력하고, 입력값이 1일 때는 1을 출력하는 일반적인 버퍼와 똑같이 작동한다. 이제 이 Controlled Buffer를 활용하여 RA에서 RB로 데이터를 복사하면서 생기는 데이터 충돌을 해결할 수 있다.

<img width="332" alt="스크린샷 2021-01-14 오후 5 42 51" src="https://user-images.githubusercontent.com/74946802/104570207-f88beb80-5694-11eb-83ae-a21d2f0e8507.png">

입력값에 버퍼를 붙여주고 Enabler에 NotGate를 붙여서 버퍼와 연결하여 Enabler가 0일 때는 버퍼값이 1, Enabler가 1일 때는 버퍼가 0이 되도록 만들어준다. 두 개의 Enabler를 연결해야 하기 때문에 AndGate로 묶어준다.

<img width="1038" alt="스크린샷 2021-01-14 오후 5 48 35" src="https://user-images.githubusercontent.com/74946802/104570246-06da0780-5695-11eb-9e52-8d915506d2ca.png">
<img width="1043" alt="스크린샷 2021-01-14 오후 5 48 46" src="https://user-images.githubusercontent.com/74946802/104570286-148f8d00-5695-11eb-9533-4895f641399b.png">

문제는 이렇게 조치를 해도 위 그림과 같이 여전히 데이터가 충돌한다는 것이다. 입력값은 제어를 했지만, RA와 RB의 출력값을 제어하지 않았기 때문이다. 다시 말하자면 두 출력값이 버스를 통해 입력값으로 흘러들어갈 수도 있기 때문에 충돌이 생기는 것이고 이를 방지하기 위해서는 출력값에도 Controlled Buffer가 필요하다. 출력값은 Enabler가 1일 때만 작동하도록 만들어준다.

<img width="1040" alt="스크린샷 2021-01-14 오후 5 55 17" src="https://user-images.githubusercontent.com/74946802/104570386-312bc500-5695-11eb-9d05-356b22edf876.png">

이제 입력값을 넣고 RA에 set을 켰다가 꺼준다. 이렇게 되면 이전 시간에 학습했듯이 RA에 들어온 값이 저장된다. 그리고 RA의 Enabler를 켜는 순간 InputBuffuer가 꺼져서 입력값은 막히고 OutputBuffer는 켜저서 버스에 내용이 채워진다.

<img width="1043" alt="스크린샷 2021-01-14 오후 5 56 51" src="https://user-images.githubusercontent.com/74946802/104570457-49034900-5695-11eb-876d-cfdb2b239006.png">
<img width="1041" alt="스크린샷 2021-01-14 오후 5 57 52" src="https://user-images.githubusercontent.com/74946802/104570496-56b8ce80-5695-11eb-918b-baf5eddc98bd.png">

이제 RA에 있는 내용을 RB로 보낼 수 있다. RA의 Enabler가 켜져있는 동안에 RB의 set을 켰다가 꺼준다. 마찬가지로 데이터를 저장하기 위해서다. 그 다음 RA의 Enabler를 꺼주고 RB의 Enabler를 켜주면 RB에 RA의 값이 그대로 복사된 것을 확인할 수 있다.

<img width="1045" alt="스크린샷 2021-01-14 오후 5 59 02" src="https://user-images.githubusercontent.com/74946802/104570523-63d5bd80-5695-11eb-9a97-9215158ea070.png">
<img width="1033" alt="스크린샷 2021-01-14 오후 5 59 19" src="https://user-images.githubusercontent.com/74946802/104570543-6d5f2580-5695-11eb-826f-d3574ccd2265.png">

이것이 버스를 활용하여 레지스터간 데이터를 복사하는 방법이다. 가장 기초적이고 원시적인 복사방법이고, 살펴본대로 버스의 데이터 충돌을 막기 위해서는 InputBuffuer와 OutputBuffer가 모두 필요하다.
