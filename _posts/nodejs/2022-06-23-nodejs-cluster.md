---
title:  "nodejs-cluster"
excerpt: "nodejs-cluster"

toc: true
toc_sticky: true

published: true

categories:
  - nodejs
tags:
  - nodejs
  - cluster
  - master
  - worker
last_modified_at: 2022-06-23T14:40:00+09:00
sitemap:
  changefreq: daily
  priority: 0.8
---

# `nodejs` 에서 `cluster` 모듈
process 객체 내 
- 프로시져 내부 변수 활용 시 변수에 값 할당 

```
select ROWNUM , employee_id from hr.employees where ROWNUM < 5;
```

![oracle](/assets/images/2022-06-07-mysql-rownum-15-07-28.png)

# `nodejs` 에서 `cluster` 모듈 활용 예시

mysql 에선 변수 선언시 @ 기호 뒤에 변수이름 선언
- 프로시져 내부 변수 활용 시 변수에 값 할당 