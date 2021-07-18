[TOC]



<hr>

<br>

<br>

# [IPv4 프로토콜](https://youtu.be/_i8O_o2ozlE?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

### IPv4 프로토콜이란?

- 네크워크 상에서 데이터를 교환하기 위한 프로토콜
  - 3계층 프로토콜
  - 3계층의 역할 : 멀리 있는 곳까지 최적의 경로로 찾아가는 것
- 데이터가 **정확하게 전달될 것을 보장하지 않는다**.
  - 전송은 하나 보장은 하지 않음! 데이터가 중간에 깨질 수도 있다.
  - 4계층에서는 보장을 함.
- 중복된 패킷을 전달하거나 패킷의 순서를 잘못 전달할 가능성도 있다.
  - 악의적으로 이용되면 DoS 공격이 됨
- 데이터의 정확하고 순차적인 전달은 그보다 상위 프로토콜인 TCP에서 보장한다.

<br>

### IPv4 프로토콜의 구조

- 크기는 기본적으로 20byte.

- 맨 끝의 IP Option은 붙을 수도 있고, 붙지 않을 수도 있다.

  - 붙을 때마다 크기가 4byte씩 늘어남.

- Source Address : 출발지 IP 주소

- Destination Address : 도착지 IP 주소

- Version : IP 프로토콜의 버전. 무조건 4만 온다고 생각하면 된다. (16진수 하나)

  - 6이 오는 경우는 없는데, IPv6는 구조 자체가 다르기 때문이다!

- IHL : 헤더 길이 (Header Length) → 최소 20byte ~ 최대 60byte

  - 2진수 4개로 표현됨. → 실제 헤더 길이를 4로 나눈 값이 저장됨!
  - 기본 헤더의 길이가 20byte이므로 주로 5가 오게 된다.

- TOS : 예전에 개발했을 때 쓰던 값으로, 지금은 쓰지 않음.

  - 0 0으로 비워져있다.
  - 세팅을 한다고 하더라고, 세팅된 값을 이해할 수 있는 장비가 없음.

- Total Length : 뒤의 페이로드까지 합쳐진 길이

  - 상위 계층에서부터 캡슐화되어서 내려온 데이터의 길이를 합친 전체의 길이

- Identification, IP Flags, Fragment Offset

  - 최대 전송 단위가 있기에 너무 큰 데이터를 보낼 때에는 데이터를 잘게 잘라서 본다.
  - 이 때 사용하는 값들!

- Identification : 잘게 잘라진 데이터들이 가지고 있는 ID 값

  - 데이터를 받는 쪽에서 잘려진 데이터들을 다시 합칠 때 사용함.

- IP Flags

  - 3비트로 이루어져 있음 
  - 첫 번째 값은 아예 쓰지 않음 (X)
  - 두 번째 값은 Don't Fragmentation (D)
    - 패킷을 보내는 사람이 데이터를 통째로 보내겠다고 명시한 것
    - 그러나 이렇게 보내면 최대 전송 단위를 초과해서 전송이 안 됨! 데이터 손실 일어남.
    - 데이터 손실 때문에 거의 사용할 수 없음!
  - 세 번째 값은 More Fragmentaion (M)
    - IP Flags에서 유일하게 사용되는 것
    - 다른 패킷들이 더 있다고 알려주는 역할을 함
    - 최대 전송 단위보다 큰 데이터를 전송하게 될 경우, 무조건 1로 세팅이 됨!
    - 그 이외의 경우 0으로 세팅이 됨.

- Fragment Offset

  - 13비트
  - 데이터를 받는 입장에서 잘게 잘려진 데이터의 순서를 알 수 있게 Offset을 지정함.
  - Offset : 어느 기준으로부터 얼마만큼 떨어져있는지를 의미함!
  - 앞의 데이터들을 합친 만큼의 크기가 Offset 값으로 지정됨.

- TTL (Time To Live) : 패킷이 살아있을 수 있는 시간

  - 패킷이 계속 살아있다면 패킷 경로를 잘못 설정했을 때 DoS 공격이 일어날 수 있음. 언제가는 없어져야 함!

    <img src="6장-IPv4,-ICMP-프로토콜.assets/1-1626598422564.PNG" width="750px" height="400px">

  - 그래서 살아있는 시간은 TTL에 저장함.

  - 특정한 숫자를 지정하는데, 라우터와 같은 3계층 장비를 거칠 때마다 1씩 줄어듦.

  - 0이 되는 순간 네트워크 장비는 네트워크 패킷을 보내지 않고 버린다.

  - 이것을 통해 상대방 컴퓨터의 운영체제가 무엇인지 알 수 있다. → 해킹에 이용됨.

    - 운영체제마다 설정하는 값이 다르기 때문! 
    - 윈도우 : 128
    - 리눅스 : 64

- Protocol : 상위 프로토콜이 무엇인지 알려줌.

  - 이더넷의 이더넷 타입과 비슷한 역할
  - 상위 프로토콜로 올 수 있는 프로토콜 : ICMP, TCP, UDP
    - 3계층 : ICMP (1)
    - 4계층 : TCP (6) , UDP (17)

- Header Checksum : 헤더에 오류가 있는지 없는지 체크함

  - 헤더에 있는 여러 가지 필드들로 값을 계산한 뒤 세팅하여 전송함.

  - 데이터를 받는 쪽에서는 세팅된 값들을 스스로 계산하여 Header Checksum에 들어가있는 값과 비교함.

    <img src="6장-IPv4,-ICMP-프로토콜.assets/image-20210718172659496.png" width="750px" height="400px">

<br>

<br>

# [ICMP 프로토콜](https://youtu.be/JaBCIUsFE74?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 

<br>

<br>

# [IPv4, ICMP프로토콜 실습](https://youtu.be/8ZwTvTuZlVw?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 

<br>

<br>

# [라우팅 테이블](https://youtu.be/CjnKNIyREHA?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 

<br>

<br>

# [라우팅 테이블 확인 실습](https://youtu.be/tVntagSJctc?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 

<br>

<br>

# [IPv4 조각화 이론](https://youtu.be/_AONcID7Sc8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 

<br>

<br>

# [IPv4 조각화 실습](https://youtu.be/QKEL9aBgHtg?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 