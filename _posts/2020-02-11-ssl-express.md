---
layout: post
title: "[Express] SSL 인증서 Express에 적용하기"
date: 2020-2-11 00:00:00 +0300
comments: true
img: expressjs.jpg
visible: 0
description: expressJS 공부중입니다.
categories: Backend
tags: [Backend, Express, SSL]
---

Express에 SSL을 적용하는 것은 매우 간단하다.

```typescript
...
// 라이브러리 두개를 불러와 주고
import * as fs from 'fs';
import * as https from 'https';
...

// express app을 실행시킬 때 https를 통해 실행시킨다.
// + https에 인증서 정보를 설정한다.
https.createServer({
    ca: fs.readFileSync('/certs/ca_bundle.crt'),
    cert: fs.readFileSync('/certs/certificate.crt'),
    key: fs.readFileSync('/certs/private.key')
}, app).listen(3000, () => {
    console.log('hosting on https://localhost:3000!!')
})
```

위의 코드를 추가해주면 끝이다.