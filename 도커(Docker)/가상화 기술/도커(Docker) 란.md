---
상태: 완료
시작일: 2024-05-26
마감일: 2024-05-26
---
### 도커
> **컨테이너(Container)라는 가벼운 독립 실행형 패키지**로, 배포, 테스트, 실행할 수 있게 해주는 2013년 최초로 공개된 오픈 소스 플랫폼입니다.

#### 도커 아키텍처
클라이언트 - 서버 모델
![](https://i.imgur.com/3KpzjhK.png)

**클라이언트**: 사용자의 명령을 전달 </br>
**도커 데몬** : 실제 컨테이너를 관리, 클라이언트가 기능을 사용할 수 있게 API를 전달

도커데몬이 API를 제공하지만 이를 읽고 이해하기에는 비효율적이기 때문에 **도커에서는 Docker CLI를 제공**합니다.
![](https://i.imgur.com/N4EcWhN.png)
사용자가 명령어를 입력하면 서버의 API 양식에 맞게 만들어서 대신 전달합니다.

### 정리
도커는 가벼운 독립 실행형 패키지이고, 클라이언트-서버 모델로 이루어져 있습니다.
클라이언트는 Docker CLI를 통해서 편리하게 컨테이너를 관리할 수 있습니다. CLI는 API 맞게 변경되어 Docker데몬에게 전달되고 Docker 데몬은 컨테이너 런타임을 통해서 컨테이너를 조작하고 그 결과를 CLI로 다시 전달합니다.