---
layout: default
title: 3 Way Handshake
parent: Network
grand_parent: Computer Science
nav_order: 3
---

# **3 Way Handshake**

{: .bg-purple-000}

---

## TCP

TCP는 4계층 프로토콜로 신뢰없는 공용망에서 정보유실 없는 통신을 보장하기 위해 세션을 안전하게 연결하고 데이터를 분할하고 분할된 패킷이 잘 전송되었는지 확인하는 기능이 있다.

패킷에 번호를 부여(**SEQ Number**)하고 잘 전송되었는지에 대해 응답(**ACK Number**)한다.

가능하면 최대한 많은 패킷을 한꺼번에 보내는 것이 효율적이지만 네트워크 상태가 안좋으면 패킷 유실 가능성이 커지므로 적절한 송신량을 결정해야 하는데 한 번에 받을 수 있는 데이터 크기를 **Window Size**라 하며, 네트워크 상황에 따라 Window Size를 조절하는 것을 **Sliding Window**라고 한다.

{: .bg-purple-000}

---

## 3 Way Handshake

TCP에서는 유실없는 안전한 통신을 위해 통신 시작 전, 사전 연결작업을 진행한다.\
TCP에서는 3번의 패킷을 주고받으면서 통신을 서로 준비하므로 <span style="color:red; font-weight:700">3 Way Handshake</span>이라고 한다.

서버에서는 서비스를 제공하기 위해 클라이언트의 접속을 받아들일 수 있는 **LISTEN** 형태로 대기한다.\
클라이언트에서는 통신을 시도할 떄 **Syn** 패킷을 보내는데 클라이언트에서는 이 상태를 **SYN-SENT**라고 부른다.

### 3 Way Handshake 기본 과정

1. SYN-SENT 상태인 클라이언트가 Syn 패킷을 보낸다.
2. 서버는 LISTEN 상태에서 Syn 패킷을 받고 SYN-RECEIVED 상태로 변경되며 Syn, Ack 패킷으로 응답한다.
3. Sny, Ack 응답을 받은 클라이언트는 ESTABLISHED 상태로 변경되고 그에 대한 응답을 Ack으로 다시 서버에 보낸다.\
   클라이언트의 이 응답을 받고 서버에서도 ESTABLISHED 상태로 변경되며 연결이 성공적으로 완료되었음을 알린다.

3 way handshake 과정이 생기다보니 기존 통신과 새로운 통신을 구분해야한다.\
어떤 패킷이 새로운 연결 시도이고 기존 통신에 대한 응답인지 구분하기 위해 헤더에 <span style="color:red; font-weight:700">Flag</span> 값을 넣어 통신한다.

### TCP 플래그

- SYN\
  연결 시작 용도로 사용한다. 연결이 시작될 떄 SYN 플래그에 1로 표시해 보낸다.
- ACK\
  ACK 번호가 유효할 경우, 1로 표시해 보낸다.
- FIN\
  연결 종료시 1로 표시된다. 데이터 전송을 마친 후 정상적으로 양방향 종료 시 사용된다.
- RST\
  연결 종료 시 1로 표시된다. 연결 강제 종료를 위해 연결을 일방적으로 끊을 떄 사용된다.
- URG\
  긴급 데이터인 경우, 1로 표시해 보낸다.
- PSH\
  서버 측에서 전송할 데이터가 없거나 데이터를 버퍼링없이 응용 프로그램으로 즉시 전달할 것을 지시할 때 사용된다.

### 3 Way Handshake 과정 예시

1. 클라이언트(SYC-SENT)는 통신을 처음 시도할 때 SYN 필드를 1로 표기해 패킷을 보낸다.\
   이 때 자신이 사용할 첫 seq no를 적어 보낸다.\
   <span style="background-color:yellow;  font-weight:700">Syn(seq=10)</span>
2. 위 SYN 패킷을 받은 서버는 LISTEN -> SYN-RECEIVED 상태로 변경된다.\
   SYN과 ACK 비트를 플래그에 1로 표기해 응답한다.\
   자신이 보내는 첫 패킷이므로 SYN을 1로 표기하고 기존 송신자가 보냈던 패킷의 응답이기도 하므로 ACK 비트도 함께 1로 표기한다.\
   이 패킷은 송신자의 연결 시도를 허락하는 의미로 사용된다.\
   이 떄 자신이 사용할 seq no를 적고, ack no는 클라이언트가 보낸 seq no에 1을 추가한 값을 넣어 응답한다.\
   10번까지 잘 받았으니 다음번에는 10 + 1번을 달라는 의미로 ack no는 11을 보낸다.\
   <span style="background-color:yellow;  font-weight:700">Syn, Ack (seq=20, ack=11)</span>
3. 서버의 응답을 받은 클라이언트는 연결을 확립하기 위해 다시 한 번 응답 메시지를 보낸다.\
   이 때부터는 기존 메시지의 응답이므로 ACK 필드만 1로 표기된다.\
   서버가 ack no를 11로 표기해 보냈으므로 seq no를 11로 표기해 응답한다.\
   동시에 서버의 seq no 20에 대한 응답이므로 ack no를 21로 보낸다.\
   <span style="background-color:yellow;  font-weight:700">Ack (seq=11, ack=21)</span>
