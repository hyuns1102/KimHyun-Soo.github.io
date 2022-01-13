---
title: "kokoa clone-2"
categories: htmlcss
tags: blog HTML CSS
published: true


---

## kokoa clone-2

---

<!-- prettier-ignore-start -->

> ~Friends Part

---

#### 6.11

- 모든 링크의 색깔을 동일하게 만들고, 밑줄을 원하지 않을 때 <br/>
- reset.css (구글링해서 찾아올 수 있다.) 를 이용해서 모든 링크에 a{ color: inherit; text-decoration: none;} 해준다.<br/>
- color는 부모에게서 상속 받아 초기화가 가능하다.<br/>


#### 6.12 

 - _box-sizing: border-box_
 - 문제의 발단은 list를 가지고 있는 nav 태그가 있는데 이 박스 줄을 <br/>
가장 밑으로 내리려고 다음과 같이

```html
position: fixed
bottom: 0 
width: 100%
```

를 했다.

그런데 가장 바깥쪽의 아이콘이 보이지 않았다. 문제는 다음 그림과 같다.

![s1](/assets/images/clone-Images/img1.png){: .align-center width="30%" height="30%"}

- 이 문제를 해결하려면 css에 대한 이해가 필요하다. <br>
  css는 프로그래머가 박스를 만들때 200px 를 주고 padding 50px를 줬다면, 이렇게 된다.
![s2](/assets/images/clone-Images/img2.png){: .align-center width="40%" height="40%"}

- 우리에게 이 모습은 이렇게 보여지나, css는 박스를 200으로 유지하려고 한다.
![s3](/assets/images/clone-Images/img3.png){: .align-center width="40%" height="40%"}

- 그래서 밑에처럼 박스가 늘어나는 것처럼 보인다. 따라서 이것을 잡아주기 위해
![s4](/assets/images/clone-Images/img4.png){: .align-center width="40%" height="40%"}
 
 우리는 박스의 모양을 그대로 유지하겠다 라는 뜻을 가진 box-sizing: border-box
을 이용한다.

<br/>

#### 6.13

- span은 width, height 가 적용이 안된다. 왜 ? span은 inline 타입의 element이기 때문이다.
- 원을 만들고 싶을 땐, width의 반만큼만 적용하자.
- absolute는 가장 가까운 relative 조상에 맞춰 움직인다. 없으면 body까지 올라감

<br/>

#### 6.14, 6.16

- padding 간격 봐주기 / 다른 곳에 쓰이는지도 봐주면서 공통점을 찾고 그에 맞게 css를 생성하자. 
- 재사용 가능할 수 있도록 만들어 주는 것 !
- 공통점 찾기.. 다른 UI에서 공통적으로 쓰이는 Component 만들어준다.

<!-- prettier-ignore-end -->
