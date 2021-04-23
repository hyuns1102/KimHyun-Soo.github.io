---
title: "kokoa clone-3"
categories: htmlcss
tags: blog HTML CSS
published: false

---

## kokoa clone-3

---

<!-- prettier-ignore-start -->

> chats, find, More, Setting, chat Part

---

#### 6.19 ~ 6.20

Chats screen

- 한 화면에서만 쓰는 것이 아니라 다른 화면에서 쓴다면 User Component 폴더로 만들어 재사용하기 쉽게 하자.
- 다음과 같이 폴더로 분리해서 사용할 수 있도록 한다.
- 폴더로 분리 후에는 항상 @import 해줄 것!

![s1](/assets/images/clone-Images/img5.png)

#### 6. 21 ~ 6. 24

Find screen

- header 를 재사용해서 작성했다.

- 알림점 만들기

  - 재사용 방법을 이용해 톱니바퀴 위 작은 점을 만들기 위해
    badge에 badge-nonumb 라는 클래스를 만들어 여러 곳에서 쓰일 수 있도록 만들었다.
    가장 중요한 것이 position을 잘 활용해야 하는데 <br/>
    position: absolute의 경우, 조상 중에 relative가 있을 때 그 위치를 기준으로 움직인다. 아니면body부터 시작을 한다. <br/>
    따라서 cog와 나란히 형제 관계에 위치시켜서 그 위 조상인 span에 relative를 위치시켰다.
    <br/>
- 같은 변수가 반복될 때는 :root에서 동일 변수(variable) 를 이용하자.<br/>
  ex) border: 1px solid rgba(0,0,0,0.2) (같은 코드 재사용 가능한 줄이기)

- HTML 코드에선 대문자를 나타내려고 해도, 우선 소문자로만 작성한다. <br/>
  대문자는 디자인적인 요소이기 때문에, CSS 파일에서 작성해줘야 한다. <br/>
  text-transform: uppercase; 대문자로 만들기.

- 자주 쓰이는 조합 :

  ```css
  .class {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  ```

- 사진 위에 span 올리기 등, 상대적 위치 정해주고 싶을 때는, <br/>
  **relative father & absolute child** 기억하기

#### 6.25 ~ 6.26

More Screen

- icon-rows라는 클래스를 만들어서icon을 모두 정렬하고 같은 스타일을 쓸 수 있도록 만들어준다.

- row들을 정렬하면서 아이템을 하나씩 추가할 때, 반응형 웹 페이지 내에서도 행이 자연스럽게 바뀌고 또는, 한 줄에 원하는 정도의 요소들이 추가되면 자동으로 다음 행으로 옮기는 법은<br/> **flex-wrap: wrap**을 이용한다.

Settings Screen

- 문제 : <br/>
status-bar에 position:fixed를 했는데 왜 겹쳐서 나왔을까? <br/>
position:fixed되면 상대성이 사라져, 독립된 개체로 보게 된다.
<br/>

- 해결 : 위치 조정은 어떻게 해야할까? 처음부터 맞춰야하나? <br/>

  1. fake-status-bar를 줘서 위치를 고정시켰다.<br/>
  2. body에 padding top을 준다.
  3. position: sticky <br/>
   fixed와 relative의 특성을 모두 가지고 있다. 그런데 internet explorer 에서는 안된다. 근데 sticky를 하면 약간 떨림증상(?) 이런게 있다..

<br/>
- 문제 : <br/>
status-bar 와 chat-header 가 모두 fixed될 때, 위치가 겹치는 경우가 생긴다.
<br/>
- 조정 방법 : z-index 를 이용하자. 
fixed or absolute position에서 쓸 수 있다.
<br/><br/>

#### 6.32

- 말풍선과 시간 박스의 순서를 변경하고 싶을 때?
  border-top-left-radius

- order는 오직 flex children에서만 적용된다.
  or flex-direction : row-revese

> #### tip
>
>- 빠르게 tag, class, child 만들기 <br/>
  [tag name].[classname] > (child)[tag name].[classname]
>- row의 정렬 <br/>
  **flex-wrap: wrap**
>
>- 사진 위 span 올리기 <br/>
**relative father & absolute child**
>
>- 정렬 조합
    ```css
    .class {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    ```

<!-- prettier-ignore-end -->
