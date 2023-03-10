---
pubDatetime: 2023-02-19
title: "네트워크관리사2급 필기노트"
description: "네트워크 관리사 2급 노트 정리"
postSlug: "network2-note"
tags: 
  - "note"
---


# DNS(Domain Name System)
- 리소스 레코드(Resource record)를 가지며, 이 리소스 레코드는 A, AAA, CNAME, NS, MX, SPF, PTR 등으로 이루어져 있음
- Forward Zone(도메인 이름 -> IP)과 Reverse Zone(IP -> 도메인 이름)을 가짐
- 주로 Forward Zone에는 도메인을 구성하는 호스트에 대한 정보를, Reverse Zone에는 DNS 서버 자기 자신에 대한 정보를 기록한다.
- DNS 서버에 질의하면 돌아오는 응답은 Authoritative answer와 Non-authoritative answer로 나뉨

## DNS 각 레코드 의미
- **A** : 레코드 A는 주어진 호스트에 대한 Ip주소(IPv4)를 알려줌
- **AAA(IP Version 6 Address records)** : 주어진 호스트에 대해 IPv6 주소를 알려줌 
- **CNAME(canonical name)** : 하나의 도메인 네임을 다른 도메인 네임으로 연결해주는 레코드
- **MX(Mail eXchanger)** : MX 레코드는 DNS 도메인 이름에 대한 메일 교환 서버를 알려줌
- **NS** : NS 레코드는 주어진 호스트에 대한 공식적인 이름 서버를 알려줌
- **PTR(Reserve-lookup Pointer records)** : IP 주소를 기반으로 도메인 이름을 찾는데 사용함(역방향)
- **SOA(Start Of Authority) 레코드** : 도메인의 모든 정보와 권한 의미. 도메인의 주 DNS 서버에 이름을 할당하고 데이터를 얼마나 오래 캐시에 저장할 수 있는지 지정(DNS의 정보를 저장한 레코드). 도메인 영역이 구분된 관리영역을 갖는 독립적인 도메인 존(Zone)임을 표시함

# TTL(Time to Live)
- 컴퓨터나 네트워크에서 데이터의 유효기간을 나타내기 위한 방법
- 컴퓨터 애플리케이션에서 캐시의 성능이나 프라이버시 수준을 향상시키는 데에도 사용

# RIP(Routing Information Protocol) 라우팅 프로토콜
- 기업의 근거리통신망, 또는 그러한 랜(LAN)들이 서로 연결된 그룹과 같은 독립적인 네트워크 내에서 라우팅 정보 관리를 위해 광범위하게 사용된 프로토콜
- 경유하는 라우터의 Hop Count에 따라 최단 경로를 동적으로 결정하는 벡터 알고리즘을 사용
- 현재 2개의 버전 중에서 버전 1은 인터넷, 인트라넷에 널리 사용되고 있으며 UNIX의 routed가 유명함
- 버전 2는 CIDR에 대응할 수 있도록 기능이 확장됨
- 버전 1은 RFC 1058, 버전 2는 RFC 1723으로 각각 규정되어 있음

## 특징
1) 라우팅 프로토콜 분류
- RIP는 내부 네트워크에 주로 사용
- 경로 지정을 하나밖에 할 수 없는 단일 경로 라우팅 프로토콜임
- 알고리즘은 거리 벡터 방식을 사용

2) 서비스하는 네트워크 주소
- RIP는 다양한 네트워크 주소 중에서도 IP 네트워크만 지원하면 IP 네트워크 주소를 이용

3) Metric
- RIP는 Hop Count 만으로 경로를 결정하며 최대 홉수는 15개

4) 경로 정보 갱신 주기
- 거리 벡터 알고리즘을 사용하기 때문에 매 30초마다 이웃 네트워크에 대한 정보를 교환함

5) 갱신 방법
- 변화된 정보만 갱신하는게 아니라 모든 정보를 동시에 갱신함

6) 이웃 설정 관계
- 이웃한 라우터들과 대등한 관계로 정보를 교환하는 Flat 구조 방식 지원

7) IP 네트워크 주소 형태
- RIP는 클래스 형태로만 광고하며, 네트워크를 세분할 수 있는 서브넷 단위로는 전송이 불가능

# TCP 헤더 플래그 비트
- URG, ACK, PSH, RST, SYN, FIN이 있음

# IPv4, IPv6
1. IPv4 
- 32bit
- 유니캐스트, 멀티캐스트, 브로드캐스트(UMB)

2. IPv6
- 128bit
- 유니캐스트, 멀티캐스트, 애니캐스트(UMA)
	- 애니캐스트 : 1 대 1(Client와 가장 가까운 PC가 대답) 전송방식

# PCM 변조 과정(아날로그 데이터 > 디지털 신호로 변환하는 과정)
- 표본화 > 압축 > 양자화 > 부호화

# CSMA/CD(Carrier Sense Multiple Access/Collision Detetion)
- LAN의 통신 프로토콜 종류 중 하나로 이더넷 환경에서 사용
- 통신을 할 때 PC나 서버가 먼저 네트워크 상에 통신이 일어나는지 확인(Carrier Sense)
- 네트워크 통신이 일어나고 있으면 데이터 보내지 않고 기다리고 통신이 일어나고 있지 않으면 데이터를 네트워크 상에 보냄
- 두 PC나 서버가 동시에 데이터를 보내는 경우를 Multiple Access(다중 접근)이라 함
- 그리고 데이터를 동시에 보내려다 부딪히는 경우 충돌(Collision)이 발생됨
- 충돌이 일어나면 데이터를 전송한 두 PC나 서버는 랜덤한 시간 동안 기다린 다음 다시 데이터를 전송
- 이런 충돌이 계속해서 15번 일어나면 통신을 끊음


# 회선 교환 개념
- 한 번 연결이 이루어지면 안정적으로 통신할 수 있음
- 연결이 이루어진다는 것은 선로를 독점해서 사용한다는 의미로 자원을 많이 사용하고 다중 통신이 어려움
- Point to Point 방식으로 연결을 확립하고 안정적으로 통신할 수 있는 방법
- 예시: 전화
- 장점: 대용량 데이터를 고속으로 전송할 때 좋음, 고정적 대역폭을 사용, 접속에는 긴 시간이 소요되나 접속 이후에는 접속이 항시 유지되며 전송 지연이 없고 데이터 전송률이 일정함, 아날로그나 디지털 데이터로 직접 전달, 연속적인 전송에 적합
- 단점: 회선 이용률 측면에서 비효율적, 연결된 두 장치는 반드시 같은 전송률과 기종 사이에 송수신이 요구됨, 속도나 코드의 변환 불가능(에러제어 기능이 어려움), 실시간 전송보다 에러 없는 데이터 전송이 요구되는 구조에서 부적합, 통신 비용이 고가임

출처 : https://security-nanglam.tistory.com/193

# OSPF(Open Shortest Path First)
- SPF(Shortest Path First) 알고리즘 기반 링크 상태 라우팅 프로토콜
- 링크상태 라우팅 프로토콜에 기초하여, 자치시스템(AS) 내부의 라우터들끼리(IGP, Interior Gateway Protocol) 라우팅 정보를 교환하는 라우팅 프로토콜

# ARQ(전송 오류 제어)
- 전진 에러 수정(FEC, Forward Error Correction) : 데이터 전송 과정에서 발생한 오류를 검출해 재 전송 요구 없이 스스로 수정
- 후진 에러 수정(BEC, Backward Error Correction) : 데이터 전송 과정에서 오류가 발생하면 송신 측에 재 전송 요구
- 자동 반복 요청(ARQ, Automatic Repeat reQuest) : 통신 경로에서 에러 발생시 수신측은 에러의 발생을 송신 측에 통보하고 송신 측은 에러가 발생한 프레임을 재전송
- 정지-대기 ARQ(Stop-and-Wait Automatic Repeat reQuest) : 송신 측이 하나의 블록을 전송한 후 수신 측에서 에러의 발생을 점검한 다음 에러 발생 유무 신호를 보내올 때까지 기다리는 방식. 수신측 응답이 긍정(ACK)이면 다음 블록 전송, 부정 응답(NAK)이면 앞서 송신했던 블록 재전송
- Go-Back-N ARQ : 여러 블록을 연속적으로 전송하고 수신 측에서 부정 응답(NAK)를 보내오면 송신 측이 오류가 발생한 블록부터 모두 재전송(에러가 발생한 이후 모든 블록 재전송 - 중복 전송 문제)
- 선택적 재전송 ARQ : 여러 블록을 연속적으로 전송하고 수신 측에서 NAK 보내면 송신 측이 오류가 발생한 블록만 재전송. 복잡한 논리 회로와 큰 용량의 버퍼 필요
- 적응적 ARQ : 전송 효율을 최대로 하기 위해 데이터 블록의 길이를 채널의 상태에 따라 그때그때 상태에 따라 동적으로 변경. 효율은 좋은데 제어회로가 복잡하고 비용이 많이 들어 현재 거의 사용하지 않음


# 그 외
- 멀티 플렉싱 방식 중 주파수 대역폭을 다수의 작은 대역폭으로 분할 전송하는 방식 : 주파수 분할 다중화(FDM, Frequency Division Multiplexing)
- TCP 프로토콜에서 사용하는 흐름제어 방식 : Sliding Window
- IEEE 802.11 WLAN(무선랜) 접속을 위해 NIC에서 사용하고 있는 다중 접속 프로토콜 : CSMA/CA => 802.11 = CA
