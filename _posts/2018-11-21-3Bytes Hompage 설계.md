# 3Bytes 홈페이지 개발기 - 1 [설계] 환경 구축

기존에 활동하던 소모임이 체계가 잡혀버리면서 뭔가 인프라 구축 + 홈페이지 개발이 필요한 시점이 생겨버렸다

그 후, 학과에서 발표를 하라는 통보를 받고 빠르게 개발을 해야 한다는 상황에서 쓸 수 있는 기술을 이용해야 했다.



## 어떤 기술을 선택할 것인가

먼저 사용 가능한 기술을 나열해보니

- Fronted
  - React
  - Vue
  - PHP

- Backend
  - Django
  - Spring
  - SpringBoot
  - PHP

- Server
  - Docker
  - VM
  - Native

- ETC
  - Haproxy
  - Nginx
  - Apache

대충 이 정도 였고 초기 선택지는

- React
- SpringBoot
- Native

로 작성되었다.



## 고려할 점은?

하지만 SpringBoot에서 JWT 인증 관련해서 전부 개발해야 한다는 점, Frontend를 배포 할 정도로 개발을 해본 적은 없었다는 점, AWS를 사용하는 환경에서 여러 사용자가 접근해서 플젝을 작동 시키는 경우 의존성 문제가 발생한다는 점 때문에 아래와 같이 변경되었다

- React
- Django
- Docker

일단, 개발 + 배포 운영을 최대한 빠르게 한 다음 추가적으로 Backend를 SpringBoot 로 옮겨야 하기 때문에 React+Django는 Rest API로 작성 후, Django에서 SpringBoot로 옮겨갈 계획을 세우고, 빌드 배포 자동화를 위한 Jenkins까지 구상한 후, 아래와 같은 아키텍처를 설계했다.



## 아키텍처

![](W:\Blog\img\2018-11-21-3Bytes-홈페이지-개발기-1 1.jpg)

여기서 MariaDB만 Postgres로 변경 된 상태로 개발했다.



## 앞으로...

Backend는 어느정도 구상이 있었기 때문에 Frontend를 중점적으로 공부하면서 진행했다.