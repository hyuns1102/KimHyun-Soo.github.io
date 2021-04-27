---
title: "JavaScript-3"
categories: JavaScript
tags: blog JavaScript
published: true

---

## Javascript - TodoList 1

---

> localstorage, event, stringfy, filter

---

### Flow

- 새로 고침이나, 웹에 재접속시 stroage에 있는 값을 읽어오기 위해 load를 해준다. **(loadedToDo)**
  - 각 값을 paint 해준다. **(paintToDo)**

- 입력 값에 값을 쓴 후, submit event **(handleSubmit)**
  - 값을 paint 해준다. **(paintToDo)**
      - button event **(deleteToDo)**
        - button 생성 및 event 처리를 해준다.
        - html list remove, object에 filter해서 push
        - object save
      -  각 값을 object에 push 한다.
  - 저장한 object save한다. **(saveToDo)**



### loadedToDo, saveToDo

- Saving the User Name user computer에 작은 localstorage를 만드는 것이다. <br> 웹에서 "F12"에 local Storage 내 - file://에 확인가능!

![s1](/assets/images/js-Images/img1.png) <br>

- localStorage.setItem / localStorage.getItem 으로 localStorage 조정 가능 <br>
(Url을 기준으로 움직인다.)

### handleSubmit

- form 태그 내에 input을 둬야 enter가 활성화 된다. <br> why? form은 데이터를 웹사이트에 전송해준다.
ex ) input, label

- event의 기본 동작은 동작을 실행하면 계속 위로 가서 프로그램을 재실행(새로고침)하게 된다.
이것을 막아주기 위해 event.preventDefault 를 해준다.

### painToDo

- localstorage에는 javascript 데이터를 저장 불가
string으로 저장하려고 한다. <br> 
-> JSON.stringify <br> 
localstorage에 있는 string을 javascript 데이터로 바꿔 출력해야 한다. <br> 
->JSON.parse <br> 
JSON (JavaScript Object Notation) -> JavaScript가 데이터를 다룰 수 있도록 도와주는 유틸리티 <br> 

- parsedToDos.forEach (function (Todo) ) : parsedToDos  array안에 있는 값들을 각각 Todo 변수 안에 넣어 function을 실행한다.


### deleteToDo

- filter 는 <br>
```javascript
 const cleanToDos = toDos.filter(function filterFn(toDo)
 { return toDo.id !== parseInt(li.id); });
```
  return에 맞는 조건들의 값만 찾아준다.

### point: 

>event.preventDefault : event 시 refresh 되는 것을 막아준다.<br>
>
>Element 생성? document.createElement / innerText / appendchild<br>
>
>list 생성? array 이용해서 object에 push 해준다.<br>
>
>LocalStorage 데이터? <br>
>
>javascript 데이터는 JSON.stringfy를 통해 string >데이터로 바꿔준다. <br>
>
>localstroage데이터는 JSON.parse를 통해 javascript 데이터로 >바꿔준다.<br>