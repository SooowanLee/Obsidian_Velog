---
상태: 진행중
tags:
  - HTTP
시작일: 2024-12-20
마감일:
---
## 인터넷 프로토콜 스택의 4계층
>애플리케이션 - HTTP, FTP
전송 계층 - TCP, UDP
인터넷 계층 - IP
네트워크 인터페이스 계층

## 프로토콜 계층
![](https://i.imgur.com/zzsSWgB.png)

## IP 패킷 정보
출발지 IP와 목적지 IP 등을 가진다.

## TCP/IP 패킷 정보
**TCP 세그먼트를 IP 패킷으로 감싼다.**
TCP 세그먼트 정보 : 출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보 등

## TCP(Transmission Control Protocol) 전송 제어 프로토콜 특징
**연결지향** : TCP 3 way handshake (가상 연결) 메세지를 수신하는 쪽과 연결을 한 다음 메세지를 전송한다.
**데이터 전달 보증** : 메세지 수신 여부를 알려준다.
**순서 보장**
**신뢰할 수 있는 프로토콜**
**현재는 대부분 TCP 사용**

## TCP 3 way handshacke
![](https://i.imgur.com/9wGpWYC.png)
SYN: 접속 요청
ACK: 요청 수락
참고: 3. ACK와 함께 데이터 전송 가능

