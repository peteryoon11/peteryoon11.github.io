---
title: Blog 올리기 
layout: single
author_profile: true
comments: true
share: true
related: false
date: '2018-10-10'
tags:
    - tech_blog
category: tech_blog
---

## Tech Blog 만들기 (주관적 관점에서의)

우선 의식의 흐름으로 나열 해 보겠습니다.

* 취업 활동이나 그 동안의 행적들을 기록해야 할 필요가 있다고 느꼈다.
* 이전에 jeykll을 통해서 간단하게 github 블로그를 만들어 보려고 했다. 
* 인터넷에 올라와 있는 여러개의 가이드를 보다 보니 엉겨서 실패했다. 
* 기본 테마는 마음에 들지 않았다.
* 같이 스터디를 하는 분의 기술 블로그를 보니 마음에 들었다. 
* 허락을 구하고 git repository 를 fork 해 오고 문제가 생길 때 마다 조언을 구했다. 
* 처음에 생각 했던 시간 보다 단 시간에 블로그의 구색을 갖추고 글을 추가 하고 있다. 

절차적으로만 정리하면 
1.  fork 
2.  _config.yml 내부 부분 수정 / host 하는 부분과 기타 자신의 랑크드인이나 메일 등의 부분을 수정 한다.
3.  /assets/images/bio/avatar2.png 를 자신이 원하는 사진으로 바꾼다.
    * 프로필 관련 파일 지정은 _config.yml 내부에 있습니다. 
    * 이때 기존에 있던 png 파일과 다른걸로 지정하는게 좋습니다. 아니면 git rm --cached 파일명 으로 기존의 캐쉬를 날려주세요 
    
4. _pages/about-me.md 를 자신의 프로필에 맞게 바꿔 줍니다. 
5.  블로그 검색에 노출 되기 쉽게 구글 어널리스트에 등록하기 
    * 지킬 블로그 구글 검색 가능하게 하는 방법[https://wayhome25.github.io/etc/2017/02/20/google-search-sitemap-jekyll/]
6. 블로그 내부에 댓글 달기 
    * _config.yml 내부에 short_name 을 수정 합니다. 
    * https://junhobaik.github.io/jekyll-apply-theme/
7. goolge-gtag 추가 하기 - 18.10.14일 추가 
    * _config.yml 내부에 아래 부분을 바꿔 줍니다.
        *  provider               : google-gtag
            * tracking_id          : "UA-당신의 아이디"
    * 위의 tracking_id 는 https://analytics.google.com/analytics/web/
        * 위의 사이트 접속 후에 왼쪽 아래의 관리 부분에서 준간의 속성 만들기에 tech_blog 등의 이름으로 생성하고 나서 나오는 UA-11111 같은 id 를 넣으시면 됩니다.
        

<pre>
 정리하고 나면 아무것도 아닌 내용이지만 헤맬수 있는 내용이니까 정리를 해둡니다. 
 추후에 누군가에게 도움이 되었으면 좋겠네요. 
</pre>
