---
title: "* kokoa clone-1"
categories: CSS
tags: blog CSS
published: false
---

## kokoa clone-1

---

<!-- prettier-ignore-start -->

> 지금까지 배웠던 것을 바탕으로 kokoa clone을 만든다.
> Clone post는 정말 필요한 것들만 필기를 했다.
> ~log-in Part

---

#### 6.1

- .gitignore 내에 github에 올리고 싶지 않는 파일추가.

#### 6.2

- BEM 방법론 <br/>
  : Block Element Modifier ex) block, block**navigation, block**navigation--navi-text

#### 6.3

- 레이아웃을 분리해서 div (non semetic) form header 등 ( sementic )으로 나눠준다.
- script는 항상 body를 닫기전에 오게하자.

  ++ 추가로 css를 link해주는 곳은 head로 하자.

#### 6.4

in CSS <br/>
body : font family <br/>
**CSS 가장 상단에 @import 해준다** <br/>
font는 많이 추가하지 말자.. 웹페이지가 무거워지게 된다. <br/>

```html
@import
url("https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,400;1,600&display=swap");
```

CSS hack !(기술)

이상하지만 잘 작동된다. <br/>

css hack (justify-content : space-between 대신 사용이 가능하다. )

- 레시피 같이 어디든 쓸 수 있다. 이상하지만 작동한다.
- 1 상위 박스 : justify-content: center; -중앙으로 몰림
- 2 내부 박스 범위 : width: 33%; -왼쪽으로 몰려서 범위 벌어짐, 왼쪽 위치할 박스는 왼쪽에 붙어서 정렬됨
- 3 중앙에 위치할 박스 : display: flex; justify-content: center; -중앙에 위치할 박스만 중앙에 위치함
- 4 오른쪽에 정렬할 박스 : _display_: flex; _justify-content_: flex-end; _align-items_: center; -오른쪽에 붙어서 정렬됨

#### 6.5 ~ Log-in finish

- id 보단 class 활용 추구한다. 하지만 명확히 하나인 부분만 있으면 id도 나쁘진 않다. <br/>
  한정적으로 쓸 수 있는게 특징이라 불편할 뿐이다! <br/>
- form 에서 action method go 는 다른 html로 연결할 때 쓴다. <br/>

```html
<form class="login-form" action="friends.html" method="get"></form>
```

- method 에는 get과 post가 있는데... <br/>

  - get 방식은 주소 표시줄에 입력한 내용이 나타나며 256byte~4096byte까지의 데이터만을 서버로 전송할 수 있다.<br/>
    주소 표시줄에 입력한 내용이 노출되기 때문에 보안상의 문제가 민감한 경우에는 사용하지 않는다.<br/>
    주소줄에는 ?name=value&name=value 형태로 나타난다.

  - post 방식은 입력된 내용의 크기에 제한을 받지 않고 입력한 내용이 노출되지 않기 때문에 회원가입, 로그인 시 등에 많이 사용된다.

#### log-in 파트 마무리

\*\*\* css정리를 할때 import는 폴더별, 파일별 순서대로 맞춰서 만들자. 작동이 안될 수 있다.
아래는 내 코드 내에서 css를 각 꾸미는 부분 별로 정리를 해놨다. <br/>
이렇게 style.css 를 중심으로 다른 component와 screen 부분으로 나눠서 정리를 해야
나중에 볼 때 편하다.

```html
@import
url("https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,400;1,600&display=swap");
@import "reset.css"; @import "variable.css"; /* Components */ @import
"components/status-bar.css"; @import "components/nav-bar.css"; /* Screens */
@import "screens/login.css"; body { font-family: "Open Sans", sans-serif; }
```

  <!-- prettier-ignore-end -->
