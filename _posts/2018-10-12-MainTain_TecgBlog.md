---
title:  Maintain_tech_blog
layout: single
author_profile: true
comments: true
share: true
related: false
date: '2018-10-12'
tags:
    - ruby
    - tech_blog
    - tech_dept
category: tech_blog
---

## Maintain_tech_blog

#### 자 이제 새로운 글을 써볼까 하고 나의 블로그를 들어 갔는데... css 가 모두 깨진... 이상한 페이지가 나오는 겁니다.. 
#### 현재는 복구 되었습니다. 

## 제가 예상하는 원인은 2가지 였습니다. 
1. 현재 이 repository 에 assets/css/main.scss 에 있던 에러로 표시 되어 있던 주석 부분 제거 (이게 무슨 상관이 있을까 하지만..)
* 그 후에 commit 및 push 를 하였다.
2. local 에서 테스트 해 보려고 jekyll 관련 된걸 깔아서 실행해 봤지만 여러가지 이유로 실행이 되지 않았다.
* 그 후에 commit 및 push 를 하였다.

## 우선 이전에 정상 동작 했던 부분으로 아래의 방법으로 돌려 놓았습니다.
* git reset --soft 해쉬코드 한 후에 
* force push 로 정상 동작은 하고 있습니다. / git push -f orign master (권장하지 않습니다.. 이전 모든 로그가 날아 갈수 있습니다...)

### jekyll이 ruby 위에서 돌아가니가.. 일단 ruby 는 한번도 사용을 안해봐서.. 라는 핑계로 미루어 두고 있습니다. 
### 나중에 날을 잡아서 ruby 로 간단한 프로그램을 하나 만들어 보면 좀 알게 될까요.. 이렇게 또 tech_dept 가 쌓여 가나 봅니다. 
