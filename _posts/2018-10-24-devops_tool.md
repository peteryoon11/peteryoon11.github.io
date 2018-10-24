---
title:  tool for devops
layout: single
author_profile: true
comments: true
share: true
related: false
date: '2018-10-24'
tags:
    - devops
    - path
    - essay
category: tech-essay
---

## tool for devops 

### Why write this
* festa.io 를 둘러 보다가 하시코프 사용자 모임 밋업을 보게 되었습니다. 
  - [festa.io의 정보](https://festa.io/events/105) 
* 마침 저녁 약속이 없는 날이 었고 이전에 ansible 에 대해서 알아 볼때 terraform 에 대해서 궁금 했기 때문에 흥미가 생겼습니다. 
* 주제가 흥미가 있었습니다. 
* 일단 실전 경험도 없고, 튜토리얼 자체도 안해봤지만 기록을 해두고 싶었습니다. 

### 주제 
* Terraform으로 AWS ECS 클러스터 실행하기 | 정창훈, CTO @당근마켓
  - Amazon ECS는 도커 컨테이너를 손쉽게 실행, 중지 및 관리할 수 있게 해주는 컨테이너 관리 서비스입니다. AWS 콘솔에서 실행하려고 하면 여러가지 선택 옵션이 많아 쉽지 않은데, Terraform을 이용해 ECS 클러스터를 실행하고 Service, Schedule Task를 실행하는 방법에 대해 이야기합니다.
* Terraform으로 Kong API Gateway 관리하기 | 박병진, Site Reliability Engineer @Kasa
  - Kong은 Nginx와 Lua를 기반으로 하는 오픈소스 API Gateway입니다. 본 세션에서는 API Gateway가 무엇인지, Kong을 선택한 이유와 사용 방법, Terraform을 이용하여 Kong을 관리한 경험을 공유합니다.

### 정리 / 주관적 
* Terraform 에 대한 정리
  * 장점
    * terraform 에 대해서 기존의 인프라는 버전 관리라는 부분이 없이 누가 언제 변경해서 지금 장애가 생겼는지 추적이 불가능 했다. 
    * terraform 을 이용하면 *.tf 파일로 관리 함으로서 인프라의 버전 관리가 이루어진다. 
  * 단점
    * 현재는 aws 만 지원 한다는 것. 
    * tf 라는 terraform 을 구성하는 언어에 익숙해 져야 하는것 
  * 덧붙이자면 
    * aws 로 직접 ecs 클러스터를 실행해 가면서 실행해 보면 좀 더 자세히 알게 될거 같다.
* Kong API Gateway 관리하기 에 대한 정리 
  * msa 에서의 api gateway 에 대해서 거의 대부분이 주어진 오픈소스 입니다. 
    * logger, traffic control, auth 등등 기본적인 부분이 대부분 제공 
    * community 버전과 enterprise 버전이 존재한다. 
  * 비교적 손쉽게 api gateway를 구축 할수 있다. 
  * 관련 대시보드도 서드 파티 오픈소스로 제공한다. / 엔터프라이즈에서 제공하던 부분 
    * 관리가 지속되는 부분은 보장이 안됨 
    * postegreSQL, Casandra 를 통해서 데이터 저장 지원


### 마치며
* 관련 내용은 페이스북 hashicorp korea user group 에 자세한 내용이 있습니다. 
* 사실 초급을 대상으로 한 교육 같은게 아니라서 모든 내용이 기억 나지 않습니다. 
  * 어느 정도의 정보 손실이 있을수 있습니다. / 사실.. 많은.. 
* 추후에 aws 로 개인 프로젝트 를 하게 된다면 추후의 회사 프로젝트에서 사용 가능하게 한번 정도 사용해 보고 싶습니다. 
  * [mac os 에 kong 설치 하기](https://docs.konghq.com/install/macos/) 
* 피드백은 언제나 환영 입니다!