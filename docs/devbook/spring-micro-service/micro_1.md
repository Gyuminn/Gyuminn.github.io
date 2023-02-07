---
layout: default
title: 마이크로 서비스 개발을 시작하기 전에 생각해야할 원칙
parent: 스프링 마이크로서비스 코딩 공작소 개정2판
grand_parent: Dev Book
nav_order: 1
---

# **마이크로 서비스 개발을 시작하기 전에 생각해야할 원칙**

{: .bg-purple-000}

---

1. **마이크로서비스는 일체형(self-contained)이어야 한다.**\
   하나의 소프트웨어 산출물로 시작 및 종료할 수 있는 서비스의 여러 인스턴스를 <span style="background-color:yellow;  font-weight:700">독립적으로 배포</span>할 수 있어야 한다.

2. **마이크로서비스는 구성 가능(configurable)해야 한다.**\
   서비스 인스턴스가 시작하면 <span style="background-color:yellow;  font-weight:700">필요한 구성 정보를 한 곳에서 읽어오거나 환경 변수로 전달</span>받아야 한다.\
   서비스 구성 정보를 설정하는데 사람의 개입이 없어야 한다.

3. **마이크로서비스는 인스턴스는 클라이언트에 투명(transparent)해야 한다.**\
   클라이언트는 서비스의 정확한 위치를 알고 있어서는 안된다.\
   그 대신 애플리케이션이 마이크로서비스 인스턴스의 물리적 위치를 몰라도 인스턴스 위치를 찾을 수 있도록 마이크로서비스 클라이언트는 <span style="background-color:yellow;  font-weight:700">서비스 디스커버리 에이전트와 통신</span>해야 한다.

4. **마이크로서비스는 자기 상태(health)를 전달해야 한다.**\
   이는 클라우드 아키텍쳐에서 매우 중요한 부분이다.
   마이크로서비스 인스턴스는 고장날 수 있으며 <span style="background-color:yellow;  font-weight:700">디스커버리 에이전트는 고장난 인스턴스를 우회해서 라우팅</span>해야 한다.\
   스프링부트에서는 액추에이터(actuator)를 사용해서 각 마이크로서비스 상태를 표시할 수 있다.

{: .important}

> 데브옵스 관점에서 마이크로서비스와 관련된 운영상 요구 사항을 사전에 해결하고, 이러한 네 가지 원칙을 마이크로서비스를 빌드하고 환경에 배포할 때마다 발생하는 <span style="color:red; font-weight:700">표준 수명 주기 이벤트</span>로 변환해야 한다.
>
> 이 네 가지 원칙은 다음에 나오는 <span style="color:red; font-weight:700">운영 수명 주기에 매핑</span>할 수 있다.

1. **서비스 조립(service assembly)**\
   <span style="background-color:yellow;  font-weight:700">동일한 서비스 코드와 런타임이 정확히 동일한 방식으로 배포되도록</span> 반복성과 일관성을 보장하면서 서비스를 패키징하고 배포하는 방법이다.

2. **서비스 부트스트래핑(service bootstrapping)**\
   마이크로서비스를 사람의 개입없이 모든 환경에서 빠르게 시작하고 배포할 수 있도록 <span style="background-color:yellow;  font-weight:700">런타임 코드에서 애플리케이션 코드와 환경별 구성 코드를 분리하는 방법</span>이다.

3. **서비스 등록 및 디스커버리(service registration/discovery)**\
   새 마이크로서비스 인스턴스가 배포될 때 <span style="background-color:yellow;  font-weight:700">애플리케이션 클라이언트가 새 서비스 인스턴스를 발견할 수 있는 방법</span>이다.

4. **서비스 모니터링(service monitoring)**\
   마이크로서비스 환경에서 높은 가용성이 요구되므로 한 서비스에 여러 인스턴스를 실행하는 것이 일반적이다.\
   데브옵스 관점에서 마이크로서비스 인스턴스를 모니터링해야 하며 <span style="background-color:yellow;  font-weight:700">장애가 발생한 서비스 인스턴스를 우회해서 라우팅하고 종료되는지 확인</span>해야 한다.
