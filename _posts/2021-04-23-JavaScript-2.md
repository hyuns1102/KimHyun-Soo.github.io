---
title: "JavaScript-2"
categories: JavaScript
tags: blog JavaScript
published: true

---

## Javascript

---

> new Date(), setInterval, 

---

### 시계 만들기

JS를 활용하여 간단한 시계를 만든다.<br>
먼저 new Date() 라는 객체를 변수로 가져온다.<br>
객체 내에 매소드인 getSeconds(), getMinutes(), getHours() 를 이용해 현재 시간을 가져온다. <br>
현재 시간이 계속 업데이트 될 수 있도록 setInterval을 이용해서 함수를 주기적 (1000ms) 으로 불러낸다.<br>

ex) D-day 시계 만들기 만들어 보자. 

### Point

>변수를 쓸 때, const A = new Date(), B = new Date() ; 처럼 콤마( , ) 를 이용해서 쓸 수 있다.<br>
>클래스 명을 지을 때는 js-[name] 을 쓰자. <br>
>작은 if 문 :

```javascript
clock.innerText = 
 `${dDayTimeMinutes < 10 ? `0${dDayTimeMinutes}`: dDayTimeMinutes}m`
```

