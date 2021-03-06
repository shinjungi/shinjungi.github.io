---
title: 인터넷은 어떻게 동작할까?
author: jungi
date: 2021-05-10 21:00:00 +0900
categories: [develop, 개발 상식]
tags: [개발 상식, 인터넷]
image:
  src: "/assets/img/contents/internet_1.jpg"
---

인터넷이 없는 삶을 생각하기도 싫을 정도로 인터넷은 우리의 삶에 중요한 기반이 되었다.  
가령 우리는 맛있는 음식점을 찾기위해 포털 사이트에서 검색을 하고, 친구와 메시지를 주고받기 위해 메신저를 이용하며, 무료한 시간을 보내기 위해서 동영상 스트리밍이나 온라인 게임을 즐기는 것처럼말이다. 이렇듯 인터넷은 우리에게 너무나도 친숙한데 정작 인터넷은 어떤것인지 또, 어떻게 동작하는지에 대해 잘 알고 있는 사람은 많지 않다. 물론 나를 포함해서 말이다. 그래서 나 같은 사람들을 위해 아래와 같이 짧게나마 정리를 해보고자 한다.

## 인터넷의 기원

과거에는 내 컴퓨터에 있는 데이터들을 다른 사람에게 공유하기 위해서 디스켓이나 CD와 같은 외부 저장장치를 이용해서 상대방에게 전달하곤 했다. 하지만 이 방법은 상대방이 가까이 있을 경우에는 편리했지만 상대방이 아주 멀리있는 경우에는 너무나도 불편했다. 이를 개선하기 위해 컴퓨터와 컴퓨터를 케이블로 연결하게 되었고 이렇게 컴퓨터와 컴퓨터를 직접 연결하고 케이블을 통해 데이터를 전달하는 방법을 네트워크라고 명명했다. 하지만 이 방법도 문제가 있었는데, 통신을 위해 두 개의 컴퓨터를 연결하면 하나의 케이블이 필요하지만 다섯 개의 컴퓨터를 연결하기 위해서는 10개의 케이블이 필요하고 이 이상 컴퓨터가 더 증가하게 되면 케이블의 수도 제곱으로 증가하게 되는 것이었다.
이를 보완하여 여러대의 컴퓨터를 하나의 선으로 연결하여 서로 소통하는 이더넷이 등장했는데 이 마저도 소규모의 네트워크를 구축하는데에는 괜찮았지만 전 세계 수십억명의 인구와 연결하기에는 무리가 있었다. 이런 이더넷을 한번 더 보완하여 이더넷 마다 라우터를 두어 이더넷간 통신을 하는 인터네트워크라는 뜻의 인터넷이 등장하게 되었고, 이는 전 세계의 컴퓨터들이 연결되어있는 거대한 네트워크를 의미하게 되었다.

## 인터넷의 동작 방식

인터넷의 동작방식을 이해하기 전에 ip주소에 대해서 알아두어야 한다.
ip서버란, 광활한 인터넷상에서 데이터가 목적지까지 정확하게 전달되도록 하는 주소이며, 서버, 컴퓨터, 휴대폰등 인터넷에 연결된 모든 장치는 고유한 ip주소를 부여받는다. 쉽게 설명하면 인터넷 세계에서 사용하는 집 주소의 개념이다.

```
ip 주소의 형태
123.123.123.123
```

상대방과 데이터를 주고 받기 위해서는 상대방의 집 주소(ip주소)를 알아야 하는데 위와 같은 형태의 주소를 모두 다 외우기에는 무리가 있기때문에 ip주소 대신 흔히 도메인 이름을 사용한다. 도메인 이름은 ip주소에 대한 가명이라고 생각하면 되고, 우리가 흔히 사용하는 "google.com", "naver.com" 등이 모두 도메인 이름이다.

```
복잡한 ip 주소 대신 사용하는 도메인 이름
google.com
naver.com
daum.net
등등..
```

전체 작동방식을 살펴보면, 브라우저의 주소창에 도메인 이름을 입력하면 브라우저가 해당 ip주소를 받기 위해 DNS(거대한 주소록)서버로 요청을 보낸다. DNS에서는 해당 도메인 이름이 가진 ip주소를 찾아서 브라우저로 반환해주고, ip주소를 전달받은 브라우저는 사용자의 요청을 해당 ip주소를 가진 서버로 전달하게 된다.

```
브라우저 주소창에 도메인 이름 입력 ->
브라우저가 DNS서버에 해당 도메인 이름의 ip주소 요청 ->
DNS서버에서 확인 후 해당 도메인 이름의 ip주소 반환 ->
브라우저는 전달받은 ip주소로 사용자의 요청을 전송
```

이 때, 요청과 응답간의 데이터 전송은 "패킷"단위로 전송되며, 하나의 큰 0과 1의 데이터를 잘게잘게 쪼개어 전송하는 단위이다. 그리고 각 패킷은 목적지인 ip번호와 데이터의 순서인 시퀀스로 구분된다. 패킷들은 모두 독립적으로 움직이며, 해당 시점에 사용 가능한 최적의 경로를 통해 전송(라우팅)되고, 목적지에 도착한 패킷들은 시퀀스 번호에 따라 다시 재조립된다.  
이 복잡한 패킷들의 흐름을 관리하기 위해 프로토콜 즉, 전송규칙을 사용하며, 프로토콜은 데이터 패킷변환, 각 패킷에 대한 발신처 및 수신처 주소 첨부, 라우터 규칙등을 설정한다. 그리고 이 프로토콜로 인해 데이터 전송간 유실된 패킷을 체크하여 재전송 받을 수 있도록 해준다.

## 망 중립성

덧붙여, 인터넷은 망 중립성의 원칙을 가지는데 이는 온라인상에서의 자유로운 의사소통을 보장하는 개념으로, 모든 데이터(패킷)를 전달하는 과정에 있어 차별이 없어야 하며, 패킷 전달에 대해서는 조건도, 돈도 받지 말자는 조건이다. 즉, 통신업체가 별도의 욕므을 받고 일부 사이트에만 더 빠른 속도를 보장하거나 합법적인 콘텐츠를 차단하고, 트래픽을 조절하는 것을 허용하지 않으며, 인터넷 망을 중립적이고 개방된 상태로 유지해 최종 사용자나 콘텐츠 업체들이 인터넷을 기반으로 자유롭게 활동할 수 있게 보장하는 원칙이다.
