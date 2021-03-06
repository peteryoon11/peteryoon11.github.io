---
title:  DevFest in Seoul 2018
layout: single
author_profile: true
comments: true
share: true
related: false
date: '2018-11-13'
tags:
    - GDG
    - Conference
    - daily
category: Conference
---

## DevFest in Seoul 2018

### Why write this
* 블로그를 하면서 참석한 Conference 는 기록을 하자고 생각을 했습니다. 
* 늦었지만 그래도 글을 써야 한다는 생각을 하고 있었습니다. 
* cloud 와 golang 관련 내용을 들으러 갔지만 ML 에 관해서 들어 보고 흥미가 있어서 ML 만 들었습니다. 
* 같이 간 친구가 ML 관련 프로젝트를 하게 되었다고 해서 관련 해서 이야기 할 수도 있다는 장점도 있었습니다. 

### 주제 / 는 너무 많으니 제가 들은 주제만 정리해 보겠습니다. 
* Browsing modern TensorFlow / ML
* 4분이면 충분한 딥러닝 파키슨병 진단기 제작기 / ML
* TensorFlow 기반 Hand Body Pose Estimation과 TensorFlow Lite 기반 모바일 경량화 / ML

* TensorFlow on Backend A.I / ML
* GTA 5를 이용한 자율주행 자동차 만들기 / ML

### 정리 / 주관적 
* Browsing modern TensorFlow / ML
  * 제목에서 와 같이 간단한 소개 였습니다. 
* 4분이면 충분한 딥러닝 파키슨병 진단기 제작기 / ML
  * 그날 처음으로 시간 가는 줄 모르고 들은 세션 이었습니다. 
  * 발표자가 회사 분이 아니었고 학생이어서 "흠 간단한 내용인건가?" 라는 생각으로 들었습니다. 
  * 그렇지만 2분의 생생한 개발기는 나는 저 나이때 뭘 했더라 라는 깊은 반성을 가지게 했었죠.
  * 참고로 두분은 고등학생과 대학원생이었습니다.
  * 기술적인 부분은 tensorflow 에 대해서 무지한지라 자세한 내용을 적을수는 없지만 
  * 생각의 전환이나 생각을 구체화하고 실행하는 부분은 정말 흥미를 유발하는 부분 이었습니다. 
  * 특히 많은 자료를 모아야 한다는 것을 역으로 해서 적은 자료로 모델을 만드는 방법이라거나 
  * 앱이 아니라 타겟 층을 위해서 디바이스를 만들고 해당 하는 부분을 portable 하게 만든 부분 등은 나도 해보고 싶다는 생각이 들게 하였습니다. 
* TensorFlow 기반 Hand Body Pose Estimation과 TensorFlow Lite 기반 모바일 경량화 / ML
  * 우리가 일반적으로 보는 영화에서의 모션 캡쳐는 센서를 달고 해당 센서를 기점으로 모션을 캡쳐하는 것으로 알고 있습니다. 
  * 그렇지만 Body Pose Estimation 을 이용해서 학습을 시키면 센서 없이도 머리와 팔, 다리를 구분 가능합니다. 
  * 일반적으로 학습을 시킬때 숫자와 문자를 가지고 학습을 시키고 필기를 문자로 전환하는 것을 봤는데요 
  * Body pose 는 작은 네모로 나누어서 해당 부분을 식별하기가 매우 힘들기 때문에 다른 방식을 사용 한다고 합니다. 
  * 바로 특정한 기준을 정하고 거기에서 머리는 이쯤 , 팔굽치는 이쯤, 다리는 이쯤에 높은 확률로 있을거야 라고 알려주는 것입니다. 
    * 사실 위의 부분은 정확하지 않습니다/ 기준을 세우거나 하는 방법 론 적인 부분에 대해서
  * 이런 방식으로 확률적으로 어느 위치 안에 있을 것이다 라는걸 학습 해주면 높은 확률로 인식이 된다고 합니다. 
* TensorFlow on Backend A.I / ML
  * notebook이 필요한 세션 이었고 실습 하는 부분 이었는데 저는 가져가지 않았기 때문에 듣기만 했습니다. 
  * codeonweb 에서의 온라인 tensorflow 모델을 활용하는 내용이 주를 이루었습니다. 
* GTA 5를 이용한 자율주행 자동차 만들기 / ML
  * 이전에 유투브에 인공지능 연구가가 GTA 에서 차를 조정하는 영상에 대해서 기사를 쓴걸 본적이 있었습니다. 
  * 그때는 화면에 대한 구현이나 어떻게 구성을 할것인가에 대한 부분은 신경쓰지 않았습니다.
  * 이 세션은 해당 부분을 학습 할 데이터를 모으고 (라고 이야기 하고 연구실에서 게임을..) 
  * 그걸 학습 시키고 운전 시에 예측 모델을 만들고 그걸 작은 전기차(유아용)에 카메라와 방향 조정을 이용해서 벽이나 장애물에 충돌 없이 이동하는 모델을 만드는 내용이었습니다. 


### 마치며
* 당일 날 올렸다면 조금 더 생생한 정보를 전달 할 수 있었을것 같습니다.
* 그래도 약 6시간 정도의 시간이 정신 없이 흘러 갈 정도로 흥미 진진한 시간 이었습니다. 
* 내년에도 가능하면 참석하려고 합니다. 
* 조금 아쉬웠던 점은 pycon 처럼 세션 별로 초급/중급/고급 자에 대해서 안내를 해주었으면 좋겠습니다.
  * 라고 설문 조사에 적긴 했습니다 그렇지만 지금 다시 생각 해 보니 주제도 모르다 다른데 
  * 거기다가 각자의 기준이 다를수도 있으니 생각해 보니 어려운 문제네요.
  * 그렇지만 중급 정도라고 정해두고 이야기 해도 기본적인 부분을 설명하는 시간을 아낄수 있으니까 주제에 대해서 조금 더 집중 할 수 있지 않을까 생각 합니다. 
* 피드백은 언제나 환영 입니다!