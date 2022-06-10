---
title:  "mysql-rownum-표시"
excerpt: "mysql-rownum-표시"

toc: true
toc_sticky: true

published: true

categories:
  - mysql
tags:
  - mysql
  - oracle
last_modified_at: 2022-06-07T14:58:00+09:00
sitemap:
  changefreq: daily
  priority: 0.8
---

# `oracle` 에서 `ROWNUM` 사용 시 

```
select ROWNUM , employee_id from hr.employees where ROWNUM < 5;
```

![oracle](/assets/images/2022-06-07-mysql-rownum-15-07-28.png)

# `mysql` 에서 rownum을 쿼리 결과에 출력하기

mysql 에선 변수 선언시 @ 기호 뒤에 변수이름 선언
- 프로시져 내부 변수 활용 시 변수에 값 할당 
```
@var = 0
```
- select 쿼리에서 활용 시
```
@var := 0
```

```
select  a.test_id , @row_num := @row_num+1 
from test_table as a , (select @row_num:=0) as temp 
where @row_num < 10;
```

![mysql](/assets/images/2022-06-07-mysql-rownum-16-40-16.png)