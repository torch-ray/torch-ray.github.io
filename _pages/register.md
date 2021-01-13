---
title: "CPU만들기2 - Register"
permalink: /cs/register/
layout: single
---

## 레지스터 만들기

- 레지스터란?

간단하게 말하면 CPU가 요청을 처리하는 데이터를 임시저장할 수 있는 공간이다. 컴퓨터에 데이터를 저장할 때 영구적인 저장을 위해서는 HDD, SSD 등의 스토리지를 활용해야한다. 메모리는 속도는 빠르지면 임시적으로만 데이터를 저장하기 때문이다. 그렇다면 CPU에서 처리한 데이터를 메모리로 보내고 이를 다시 스토리지로 보내서 저장해야 한다는 뜻인데, 이러한 명령을 처리하기 위해서는 이들에 대한 주소값과 명령을 저장할 수 있는 공간(기억공간)이 추가적으로 필요하다. 레지스터는 저장할 수 있는 용량이 적은 대신에 저장 공간 중에 가장 빠른 속도를 자랑한다. CPU의 원활한 작업을 위해서 메모리와 CPU를 연결해주는 중간다리 역할이라고 할까?

## 레지스터 만들기

- 1bit Memory만들기

역시 NAND_GATE를 활용해서 메모리를 만들 수 있다.

<img width="538" alt="1bitM" src="https://user-images.githubusercontent.com/74946802/104413967-b8ecd300-55b2-11eb-80c2-dd837fba3d1c.png">

아래와 같이 1번게이트에 Input값을 입력해도 output이 출력되지 않는다. 이는 set때문인데, set에 true(1)를 입력하지 않으면 어떠한 값도 출력하지 않는다.
set의 역할은 Input값을 쓸지말지 결정하는 입력 제어 단자이다.

<img width="535" alt="1bitM2" src="https://user-images.githubusercontent.com/74946802/104418000-9c07ce00-55b9-11eb-948c-0ae585898fde.png">

set에 값을 입력해주면 Input값에 따라 그제서야 True or false를 출력한다.

<img width="554" alt="1bitM3" src="https://user-images.githubusercontent.com/74946802/104418217-e8eba480-55b9-11eb-9aea-96de38f568fc.png">

그 후 set을 0으로 바꿔주면 output값이 저장된 상태로 고정된다. 즉, Input값을 바꿔도 output이 변하지 않는다는 뜻이다.

<img width="540" alt="1bitM4" src="https://user-images.githubusercontent.com/74946802/104418337-19334300-55ba-11eb-8bfd-62e4378bc22f.png">

1bit Memory를 성공적으로 만들었다. 조금 복잡할 수 있는 부분을 지우고 같은 기능을 하는 1bit Memory를 아래와 같이 외형을 변형시켰다.

<img width="398" alt="1bitM9" src="https://user-images.githubusercontent.com/74946802/104418597-8050f780-55ba-11eb-8042-9413af14cab3.png">
<img width="411" alt="1bitM10" src="https://user-images.githubusercontent.com/74946802/104418628-8a72f600-55ba-11eb-9545-fd3fdfe8ffff.png">

- 8bit Memory만들기

이제 1bit Memory 8개를 붙여서 8bit짜리 Memory를 만들고자 한다. 입력과 출력값도 각각 8bit로 수정해주면 아래와 같이 만들 수 있다. 1bit때와 마찬가지로 set에 1을 입력하지 않으면 어떤 Input을 넣어도 출력값은 없다. 동작 원리는 1bit메모리와 같기 때문에 별도로 설명하지 않는다.

<img width="960" alt="8bitM1" src="https://user-images.githubusercontent.com/74946802/104418848-e89fd900-55ba-11eb-9e94-c2d2cec30756.png">
<img width="920" alt="8bitM2" src="https://user-images.githubusercontent.com/74946802/104418974-2270df80-55bb-11eb-99a6-48aa7b59653c.png">

8bit Memory 역시 똑같은 기능을 가진 조금 더 보기 좋은 형태로 외형만 변환하면 아래와 같다.

<img width="357" alt="8bitM4" src="https://user-images.githubusercontent.com/74946802/104419082-4d5b3380-55bb-11eb-9170-90a886a7b8d8.png">

1bit 메모리와의 차이점은 입력값과 출력값이 1bit가 아니라 8bit라는 점이다.

- Enabler 만들기

최종적으로 레지스터로서 기능을 하려면 출력제어기, 즉 Enabler가 필요하다. Enabler는 AndGate 8개를 활용하여 만들 수 있다. 아래와 같은 형태이며, 역시 set에 1값을 입력하지 않으면 어떠한 출력도 하지 않는다.

<img width="648" alt="Enabler1" src="https://user-images.githubusercontent.com/74946802/104419755-44b72d00-55bc-11eb-9ee2-e422b09163c2.png">
<img width="688" alt="Enabler2" src="https://user-images.githubusercontent.com/74946802/104419780-4c76d180-55bc-11eb-96c2-a8511f06bbb9.png">

반대로 set에 1을 입력하면 아래와 같이 입력값에 따라 그대로 출력한다.

<img width="708" alt="Enabler3" src="https://user-images.githubusercontent.com/74946802/104419920-7fb96080-55bc-11eb-87e9-7e983e7d2358.png">

- 레지스터 만들기

이제 앞서 만들었던 8bit 메모리와 Enabler를 활용하여 레지스터를 만들 수 있다. 레지스터 역시 set값을 입력하지 않으면 어떠한 출력을 입력해도 작동하지 않는다.

<img width="583" alt="Register" src="https://user-images.githubusercontent.com/74946802/104420097-b5f6e000-55bc-11eb-8d8d-78fb296dd080.png">

물론 출력값을 넣고 set을 작동시켜도 아래와 같이 메모리 단계까지는 입력값이 전달되지만, enabler를 작동시키지 않으면 최종적으로 레지스터는 아무 값도 출력하지 않는다.

<img width="580" alt="Register1" src="https://user-images.githubusercontent.com/74946802/104420257-f191aa00-55bc-11eb-8b52-fc42dd1b1d46.png">

Enabler를 작동시켜야 레지스터가 입력값대로 출력값을 반환한다.

<img width="578" alt="Register2" src="https://user-images.githubusercontent.com/74946802/104420312-053d1080-55bd-11eb-9f3c-4aa7912b8220.png">

이제 레지스터를 메모리나 Enabler처럼 외형을 보기 좋게 변환시킨다.

<img width="459" alt="Register4" src="https://user-images.githubusercontent.com/74946802/104420377-2271df00-55bd-11eb-97f6-50a951bea33b.png">

위에서 설명한바와 같이 Enabler의 작동여부에 따라 입력값이 들어올 때 0 또는 1을 그대로 출력한다.

<img width="442" alt="Register6" src="https://user-images.githubusercontent.com/74946802/104420423-33225500-55bd-11eb-9334-35964edb4a8f.png">

<img width="429" alt="Register7" src="https://user-images.githubusercontent.com/74946802/104420502-4cc39c80-55bd-11eb-86c4-c1e5c4527075.png">
