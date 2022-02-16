---
title: "JavaScript-1"
categories: JavaScript
tags: blog JavaScript
published: true

---

## Javascript

---

> Basic, Array, DOM(Object), if-else, classList

---

### 1. Basic

> Javascript 는 프로그래밍 언어이다. <br> 
>
> Javascript의 스크립트 언어는 ECMA Script를 토대로 만들어진다. <br>
>
> Javascript의 한 line은 Expression이라고 하는 데 이것은 instruction 하나를 나타낸다. <br>
>
> 변수(variable)는 생성(create) -> 초기화(initialize) -> 사용(Use) 의 과정을 거친다. <br>
>
> execute top to bottom <br>
>
> 변수명을 지정할 땐, lowerOfWeek 처럼 앞글자는 lower case 다음 띄어쓰기 하는 곳부터는 UpperCase로 쓴다.
> __Camel Case__
> 
> let / const : let은  변할 수 있고, const는 상수를 의미한다. <br>
> var 은 그냥 쓰지 말자. const, let이 있는한!
> 
> const what = " anything "	  :   String <br>
> const what = 4		  :   Number <br>
> const what = true	  :   boolean <br>

### 2. 자바스크립트는 어떻게 데이터를 저장할까?

- Array : It's a way to store data on a list format
  ex)
  ```javascript
  const woman = [["hi", "this", "is"], "my", "name"];
  ```

- Object : It's a way to store information on a key-value format
  ex)
  ```javascript
  const woman = {
     name: "hyun",
     age: 28,
     object: {
       name: "Kimchi",
       age: 25
     }
   };
  ```

  ex)
  ```javascript
  const calculator = {
    plus: function(a, b){
      return a+b;
    },
    minus: function(a, b){
      return a - b;
    },
    sqrt: function(a, b){
      return Math.sqrt(a,b);
    }
  }

  const plus = calculator.plus(5, 5);
  const minus = calculator.minus(5, 5);
  const sqrt = calculator.sqrt(4, 2);

  console.log(plus);
  console.log(minus);
  console.log(sqrt);
  ```

### 3. 큰 따옴표 "", 작은 따옴표 '', 백틱 ``

  큰 따옴표 “ “ ,작은 따옴표 ‘ ‘ : 같은 용도로 쓰인다. <br>
  백틱 ` `                      : 백틱은 안에 변수를 사용할 수 있다.<br>
   ex) ` ${name} `  --> name이라는 변수 안에 저장된 값이 출력된다.<br>

### 4. DOM

__Document Object Module : <br> Document는 html에 있는 element들을 객체로 가져온다.__

ex)
```javascript
const title1 = document.getElementById(“title”); // id = title
const title1 = document.querySelector("#title"); // id = "title"
const title1 = documnet.querySelector(".title"); // class = "title"
```
위의 예시처런
html에 있는 id = "title" 을 가져와서 .js파일에서 title1이라는 객체로 등록한다.
이 안에 여러 method를 이용해서 html에 기능을 만들어 준다.

<u>document.queryselector()</u> <br>
정의 : queryselector는 특정 name이나 id를 제한하지 않고 css선택자를 사용하여 요소를 찾을 수 있다. 
document 전에체서 일치하는 element를 가져온다. 

### 5. event

javascript 내에는 event 함수가 존재한다. <br>
event가 일어난 것을 듣기 위해 __addEventListener__ 라는 함수를 쓴다.
이 함수를 통해 event가 발생했을 때 다음 호출 함수를 지정할 수 있다.

ex)
```javascript
const titleStatus = document.querySelector("h2");
const superEventHandler = {
  mouseRight: function () {
    titleStatus.innerHTML = "That was a right click!";
  }
};
function init() {
  window.addEventListener("contextmenu", superEventHandler.mouseRight);
  // superEventHandler 객체 내에 mouseRight 변수 내에 function 사용
}
init();
```

### 6. if - else

> == 과 === 은 다르다. <br>
> ==  : 변수 값을 기반으로 유형 비교 <br>
> === : 변수 값과 자료형으로 유형 비교 (엄격한 비교) <br>

> && : 그리고 <br>
> ||   : 또는 <br>
> <= , >=, <, > <br>
> 이중 연산자는 안됨 &&를 이용하자... <br>
> ex) 8 < width < 9  -->  8 < with && width < 9 <br>

### 7. if - else, ClassList

className : 태그의 클래스 이름을 가져온다. <br>
classList : class의 이름을 메소드를 통해 다양하게 조정할 수 있다. <br>
 ex) classList.add, classList.remove, classList.contains, classList.toggle

null은 문자열 취급

```javascript
// 방법1
function click() {
  const name = h2.className;
  if (name !== CLASSNAME) {
    h2.classList.add(CLASSNAME);
  } else {
    h2.classList.remove(CLASSNAME);
  }
}
// 방법2
function click() {
  const name = h2.classList.contains(CLASSNAME);
  if (!name) {
    h2.classList.add(CLASSNAME);
  } else {
    h2.classList.remove(CLASSNAME);
  }
}
// 방법3
function click() {
  h2.classList.toggle(CLASSNAME);
}
function init() {
  h2.addEventListener("click", click);
}
init();
```

### Point

> animation: hideSplashScreen 1s ease-in-out __forwards__;
>
> will-change: transform;
>
> animation-delay : animation을 잠깐 멈춤.
>
> focus-within : 클래스 내부에 focus를 받은 후에 다른 클래스 동작
