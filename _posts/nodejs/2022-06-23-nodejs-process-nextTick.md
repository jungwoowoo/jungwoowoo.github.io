---
title:  "nodejs-process-nextTick"
excerpt: "nodejs-process-nextTick"

toc: true
toc_sticky: true

published: true

categories:
  - nodejs
tags:
  - nodejs
  - process-nextTick
last_modified_at: 2022-06-23T14:11:00+09:00
sitemap:
  changefreq: daily
  priority: 0.5
---

# `process.nextTick` 의 발생 시점
* [process.nextTick](https://nodejs.org/dist/latest-v16.x/docs/api/process.html#processnexttickcallback-args)
- This is important when developing APIs in order to give users the opportunity to assign event handlers after an object has been constructed but before any I/O has occurred:

```
const { nextTick } = require('process');

function MyThing(options) {
  this.setupOptions(options);

  nextTick(() => {
    this.startDoingStuff();
  });
}

const thing = new MyThing();
thing.getReadyForStuff();

// thing.startDoingStuff() gets called now, not before
```

# `process.nextTick` 활용 예시
- 수행할 오브젝트 혹은 모듈 첫라인에 초기코드를 선언하고 수행하면되지,
process.nextTick 은 왜 제공되고 사용할까