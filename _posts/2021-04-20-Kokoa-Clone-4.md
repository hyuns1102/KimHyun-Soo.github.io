---
title: "kokoa clone-4"
categories: HTML/CSS
tags: blog HTML CSS
published: false

---

## kokoa clone-4

---

<!-- prettier-ignore-start -->

> chat, Splash, Navi-Ani Part

---

#### 6.33 

Chat Screen - reply bar

- column 내에 "input 창" + "이모티, 플러스 창"이 들어갔을 때, 박스의 크기를 화면에 맞추기 위해 
  전체적인 column의 width값을 파악해서 분할을 한 뒤에 안쪽 column을 분할한다.

- position : relative와 absolute 이용해서 박스 안에 박스를 위치시킬 때, 조정하기 

#### 6.34 ~ 6.35

Splash Screen

- 웹을 실행헀을 때 보이는 가장 첫 화면이다.
- splash 화면을 다 만든 후에 animation을 이용하면, Keyframe의 특성상 다시 돌아오게 된다. ( from ~ to ~ )
  forwards 라는 특성을 animation 뒤에 붙이면 다시 돌아오진 않는다.<br/>
```css
  style{
    animation: hideSplashScreen 1s ease-in-out forwards;
  }
  ```
  
- 문제는 마지막 key frame을 억해서 html 상에는 element가 아직 남아있다.
  - visibility : hidden  이를 쓰면 클릭은 할 수 있다. 하지만 눈에만 보이지 않을 뿐 사라지진 않는다. 
    답은? JavaScript를 쓴다.!
    animation-delay : animation을 잠깐 멈추게 한다.

#### 6.36 ~ 6.37

Navigation Bar - Animation

- 동전 굴리기
- 내비게이션 바 아래에서 올라오게 만들기
- 톱니바퀴 굴리기 
- 하트 뛰게 하기  -> 흔들릴때..? 
  ```css
  will-change: transform;
  ```

#### 6.38

Chat screen

- Fade-In 기법 사용하기.

   ```css
   @keyframes fadeIn {
     from {
       transform: translateY(30px);
       opacity: 0;
     }
     to {
       transform: none;
       opacity: 1;
     }
   }
   ```

- chat 내에 reply바에서 Input에 focus가 됐을 때,

  focus-within : 
  원하는 클래스 내부에 focus를 받은 후에 다른 클래스를 동작시키고 싶을 때
  ```css
  .reply:focus-within .reply__column:first-child {
    opacity: 0;
  } 
  ```

- 문제: 애니메이션을 했는데 왜  이 button 이 자꾸 밑에서 멈칫 거리다가 사라지는 현상을 볼 수 있었다.
  이 현상을 사라지게 하기 위해, 코드를 살펴봤지만 아무것도 못 찾았다.
  해결: width 값이 바뀔 때, 위치가 변경되는 것을 보고 position에 문제가 있는 것을 봤다. 
  (한 30분은 쳐다본듯.. )
  absolute position을 정해주면 relative position에 대해 위치를 지정해주자. top:0px right:0px 

++ chat 화면 내에 채팅원들, 채팅바 fade In 가능하게 만듬

#### tip

> animation: hideSplashScreen 1s ease-in-out __forwards__;
>
> will-change: transform;
>
> animation-delay : animation을 잠깐 멈춤.
>
> focus-within : 클래스 내부에 focus를 받은 후에 다른 클래스 동작
<!-- prettier-ignore-end -->
