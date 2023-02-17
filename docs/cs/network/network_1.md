---
layout: default
title: Network Basic
parent: Network
grand_parent: Computer Science
nav_order: 1
---

# **Network Basic**

{: .bg-purple-000}

---

## 프로토콜

프로토콜은 말 그대로 규약이다.

- 물리적 측면\
  데이터 전송 매체, 신호 규약, 회선 규격 등. **이더넷**이 널리 쓰인다.
- 논리적 측면\
  장치들끼리 통신하기 위한 프로토콜 규격. **TCP/IP**가 널리 쓰인다.

ex) HTTP 프로토콜 헤더\
 문자로 정의되어 있어 헤더 정의가 자유롭고 확장이 가능하다. 텍스트 파일과 같은 데이터가 전달되어 효율성은 비트 기반 프로토콜보다 떨어지지만 다양한 확장이 가능하다.

{: .text-red-000}
TCP/IP 프로토콜 스택

- 애플리케이션 계층: FTP, **SSH**, TELNET, **DNS**, SNMP
- 전송 계층: **TCP**, UDP
- 네트워크 계층: ICMP, **IP**, ARP
- 데이터링크 계층
- 피지컬 계층: **이더넷**

{: .bg-purple-000}

---

## OSI 7계층과 TCP/IP

| 계층  | 기본 용어                | 데이터(PDU - Protocol Data Unit) |     |
| :---- | :----------------------- | :------------------------------- | :-- |
| 7계층 | Application Layer        | Data                             | L7  |
| 6계층 | Presentation(표현) Layer | Data                             | L6  |
| 5계층 | Session Layer            | Data                             | L5  |
| 4계층 | Transport Layer          | Segments                         | L4  |
| 3계층 | Network Layer            | Packets                          | L3  |
| 2계층 | Data Link Layer          | Frames                           | L2  |
| 1계층 | Physical Layer           | Bits                             | L1  |

~~OSI 계층이 대헤서 분명 이론적으로 알고 있었다. 그런데 로드 밸런스 개념에서 L4/L7과 같은 용어가 나오길래 뭔가 했는데 그게 이거였다 ㅋㅋ~~

{: .bg-purple-000}

---

## OSI 7계층별 간단히 이해하기

{: .text-red-000}

### 1계층

들어온 전기 신호를 그대로 잘 전달하는 것이 목적.\
전기 신호가 1계층 장비에 들어오면 이 전기 신호를 재생성하여 내보냄.\
1계층 장비는 주소의 개념이 없으므로 전기 신호가 들어온 포트를 제외하고 모든 포트에 같은 전기 신호를 전송.

- 주요 장비\
  케이블, 커넥터 - 케이블 본체를 구성하는 요소\
  트랜시버 - 랜카드와 케이블을 연결\
  탭 - 네트워크 모니터링, 패킷 분석을 위해 전기 신호를 다른 장비로 복제

{: .text-red-000}

### 2계층

데이터 링크 계층으로 전기 신호를 모아 우리가 알아볼 수 있는 데이터 형태로 처리.\
전기 신호를 정확히 전달하기보다 주소 정보를 정의하고 정확한 주소로 통신이 되도록 함. - MAC 주소체계\
데이터에 대한 에러를 탐지하거나 고치는 역할을 수행할 수 있음.\
받는 사람이 현재 데이터를 받을 수 있는지 확인하는 작업 - 플로 컨트롤

- 주요 장비\
  랜카드\
  스위치

{: .text-red-000}

### 3계층

IP 주소와 같은 논리적인 주소가 정의됨.\
MAC 주소와 달리 IP 주소는 사용자가 환경에 맞게 변경해 사용할 수 있고 네트워크 주소 부분과 호스트 주소 부분으로 나뉜다.

- 주요 장비\
  라우터 - IP 주소를 사용해 최적의 경로를 찾아주고 해당 경로로 패킷을 전송하는 역할(패킷 포워딩)

{: .text-red-000}

### 4계층

실제로 아래 계층들의 데이터들이 정상적으로 잘 보내지도록 확인하는 역할을 수행한다.\
패킷 네트워크는 데이터를 분할해 패킷에 실어보내다 보니 중간에 패킷이 유실되거나 순서가 바뀌는 경우가 생길 수 있다.\
이 문제를 해결하기 위해 패킷이 유실되거나 순서가 바뀌었을 때 바로잡아 주는 역할을 4계층에서 담당한다.\
패킷을 분할할 때 패킷 헤더에 보내는 순서와 받는 순서를 적어 통신하므로 패킷이 유실되면 재전송을 요청할 수 있고 순서가 뒤바뀌더라도 바로잡을 수 있다.\
패킷에 보내는 순서를 명시한 것이 **시퀀스 번호**이고 받는 순서를 나타낸 것이 **ACK(Achknowldegement Nubmer)**이다.\
뿐만 아니라 장치 내의 많은 애플리케이션을 구분할 수 있도록 **포트 번호를 사용해 상위 애플리케이션을 구분**한다.

- 주요 장비\
  <span style="color:red; font-weight: 700">로드 밸런서, 방화벽 - 포트 번호와 시퀀스(seq), ACK(ack number) 번호 정보를 이용해 부하를 분산하거나 보안 정책을 수립해 패킷을 통과, 차단하는 기능을 수행한다.</span>

{: .text-red-000}

### 5계층

세션 계층은 양 끝단의 응용 프로세스가 연결을 성립하도록 도와주고 연결이 안정적으로 유지되도록 관리하며, 이 연결을 끊는 역할을 한다.\
흔히 부르는 "세션 관리"의 주요 역할은 TCP/IP 세션을 만들고 없애는 책임을 진다.

{: .text-red-000}

### 6계층

프레젠테이션 계층은 표현 방식이 다른 애플리케이션이나 시스템 간의 통신을 돕기 위해 하나의 통일된 구문 형식으로 변환시키는 기능을 수행한다.\
일종의 변역기나 변환기 역할을 수행.\
7계층에서 데이터의 형식상 차이를 다루는 부담을 덜어준다.\
MIME 인코딩이나 암호화, 압축, 코드 변환가 같은 동작이 이 계층에서 이루어진다.

{: .text-red-000}

### 7계층

애플리케이션 프로세스를 정의하고 애플리케이션 서비스를 수행한다.\
네트워크 소프트웨어의 UI 부분이나 사용자 입,출력 부분을 정의하는 것이 이 계층의 역할이다.\
이 계층의 프로토콜은 엄청나게 많은 종류가 있지만 대표적으로 FTP, SMTP, HTTP, TELNET이 있다.