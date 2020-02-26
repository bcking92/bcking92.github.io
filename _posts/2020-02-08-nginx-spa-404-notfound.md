---
layout: post
title: "[Nginx] SPA 호스팅, 새로고침 404 Not Found 문제 해결하기"
date: 2020-2-08 00:00:00 +0300
comments: true
img: Nginx.png
visible: 0
description: Nginx 공부중입니다.
categories: Backend
tags: [Backend, Nginx]
---

Nginx로 정적파일을 호스팅하다가 새로고침시 404 Not Found 페이지가 뜨는 문제가 생겼다.
이 문제를 해결하기 위해 config에 try_files $uri $uri/ /index.htm 를 추가해야했다.

```nginx
server {
    ...
    location / {
        ...
        try_files $uri $uri/ /index.html
    }
}
```

추가된 코드의 뜻은 

location / 에서 먼저 

1. $uri 와 정확히 일치하는 놈이 있는지 봐라.
2. 그 다음 $uri/와 정확히 일치하는 놈이 있는지 봐라.
3. 없으면 root/index.html 을 실행해라

이건데..

SPA에서는 routing이 사실 routing이 아니다. uri가 변함에 따라서 그 정보를 가지고 JS로 다른 컴포넌트를 렌더링 하는 방식이다. 그러므로 이것을 설정해 주지 않는다면 새로고침시 404 Not found page를 찾을 수 밖에 없는 것이다. 왜냐 일치하는 URL이 없으니까! SPA의 진짜 URL은 root 주소 뿐이니까~