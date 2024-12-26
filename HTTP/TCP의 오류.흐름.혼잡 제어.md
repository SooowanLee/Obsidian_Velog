---
상태: 진행중
tags:
  - HTTP
시작일: 2024-12-26
마감일:
---
## TCP의 기능
재전송을 기반으로 다양한 **오류**를 **제어**
**흐름 제어**를 통해 처리할 수 있을 만큼의 데이터 송수신
**혼잡 제어**를 통해 네트워크가 혼잡한 정도에 따라 전송량 조절
![](https://i.imgur.com/0e5a4gK.png)

## 오류 검출과 재전송
**TCP 세그먼트의 체크섬 필트, 충분할까?**
- 송신 호스트가 송신한 세그먼트에 문제가 발생했음을 인지할 수 있어야한다.
- 오류를 감지하게 되면 해당 세그먼트를 재전송할 수 있어야한다.
**TCP는 언제 오류를 검출하고 재전송할까?**
- 중복된 ACK 세그먼트를 수신했을 때
- 타임아웃이 발생했을 때

### 중복된 ACK 세그먼트를 수신했을 때
![](https://i.imgur.com/RVr0RC8.png)
### 타임아웃이 발생했을 때
호스트가 세그먼트를 전송할 때마다 재전송 타이머(retransmission timer) 시작
타임아웃이 발생할 때까지 ACK 세그먼트를 받지 못하면 재전송
![](https://i.imgur.com/XuJoIgP.png)

## 재전송 기법: ARQ(Automatic Repeat Request, 자동 재전송 요구)
**수신 호스트의 답변(ACK)과 타임아웃**을 **토대로** 문제를 진단하고 **문제가 생긴** **메시지**를 **재전송함**으로써 신뢰성을 확보하는 방식

## ARQ의 대표적인 세 가지 방식
**Stop-and-Wait ARQ**
**Go-Back-N ARQ**
**Selective Repeat ARQ**
![](https://i.imgur.com/NpiOlbE.png)
**TCP는 ARQ(Automatic Repeat Request)를 사용하는 대표적인 계층이자 프로토콜**

###  ST