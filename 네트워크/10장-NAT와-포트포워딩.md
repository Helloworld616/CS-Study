[TOC]

<hr>

<br>

<br>

# [NAT란?](https://youtu.be/Qle5cfCcuEY?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

### NAT

- NAT(Network Address Translation)은 IP 패킷의 TCP/UDP 포트 숫자과 소스 및 목적지의 IP 주소 등을 재기록하면서 라우터를 통해 네트워크 트래픽을 주고 받는 기술을 말한다.
  - 3, 4 계층을 수정하면서 수정했다는 사실을 기록함.
  - 원래의 목적지를 다른 목적지로 변경함.
  
- 패킷에 변화가 생기기 때문에 IP나 TCP/UCP의 체크섬(checksum)도 다시 계산되어 재기록해야 한다.

- NAT를 이용하는 이유는 대개 **사설 네트워크에 속한 여러 개의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위함**이다.

- 하지만 꼭 사설 IP를 공인 IP로 변환하는 데에만 사용하는 기술은 아니다.

  <img src="10장-NAT와-포트포워딩.assets/3.PNG" width="750px" height="400px">

<br>

<br>

# 포트 포워딩이란?

### 포트 포워딩

- 포트 포워딩 또는 포트 매핑(port mapping)은 패킷이 라우터나 방화벽과 같은 네트워크 장비를 가로지르는 동안  특정 IP 주소와 포트 번호의 통신 요청을 특정 다른 IP와 포트 번호로 넘겨주는 네트워크 주소 변환(NAT)의 응용이다.

- 이 기법은 게이트웨이(외부망)의 반대쪽에 위치한 사설 네트워크에 상주하는 호스트에 대한 서비스를 생성하기 위해 흔히 사용된다.

- 직접 사설 IP로 보내지 않고, 공인 IP의 특정 포트로 보낸다.

- 이후 공유기가 특정 포트로 들어온 요청을 다른 특정 IP의 특정 포트로 전송

  <img src="10장-NAT와-포트포워딩.assets/4.PNG" width="750px" height="400px">

<br>

<br>

# [포트 포워딩 설정 실습](https://youtu.be/EvYI14QdM6A?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 일반적으로 포트 포워딩 설정은 공유기에서 한다.
- 호스트 PC에 접속을 해야 사설 PC에도 접속할 수 있다.
- 실습 시에는 방화벽을 끄는 것이 좋다! 방화벽이 통신을 막기 때문.