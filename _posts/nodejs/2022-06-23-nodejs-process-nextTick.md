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

# `process.nextTick` 의 시점 원문 설명
- Use nextTick() when you want to make sure that in the next event loop iteration that code is already executed.
* [process.nextTick](https://nodejs.org/dist/latest-v16.x/docs/api/process.html#processnexttickcallback-args)
- This is important when developing APIs in order to give users the opportunity to assign event handlers after an object has been constructed but before any I/O has occurred:
- `이미 모듈 내 스크립트 수행이 끝난 이후`이거나 `queue 대상 이벤트들보다 우선시 하는 이벤트 핸들러를 작성하고 동작시키고 싶을 때` 작성하면 될 것 같다.

# `process.nextTick` 시점 예시
- `이미 모듈 내 스크립트 수행이 끝난 이후`

```javascript
const { nextTick } = require('process');

console.log('start');
nextTick(() => {
  console.log('nextTick callback');
});
console.log('scheduled');
```

```terminal
start
scheduled
nextTick callback
```

- `queue 대상 이벤트들보다 우선시 하는 이벤트 핸들러를 작성하고 동작시키고 싶을 때`

```javascript
const { nextTick } = require('process');

console.log('start');
nextTick(() => {
  console.log('nextTick callback');
});
console.log('scheduled');

setTimeout(()=>{
  console.log('setTimeout cb!')
}, 1000);

setImmediate(()=>{
  console.log('setImmediate cb!')
});

Promise.resolve().then(()=>{
    console.log("process.pid " , process.pid);
})
```

```terminal
start
scheduled
nextTick callback -> 모듈내 스크립트 끝난 후 수행 , queue 에서 수행되는 이벤트핸들러보다는 우선
process.pid  27632 -> 같은 microstack 내의 Promise callback 보다 nextTick의 cabllback이 앞에서 수행
setImmediate cb!
setTimeout cb!
```