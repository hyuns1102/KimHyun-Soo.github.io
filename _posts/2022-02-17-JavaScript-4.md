---
title: "JavaScript-Basic Grammer"
categories: JavaScript
tags: blog JavaScript
published: true
---


# Grammer (for Test)

## Install

**node.js (LTS) 설치 필수!**

vscode 확장 프로그램에서 code runner 설치 후,  
실행 시, ctrl+alt+'N' 으로 실행  

or

터미널 창에 node + 실행파일명.js

## Basic

> Javascript 는 프로그래밍 언어이다. <br> 
>
> Javascript의 스크립트 언어는 ECMA Script를 토대로 만들어진다. <br>
>
> Javascript의 한 line은 Expression이라고 하는 데 이것은 instruction 하나를 나타낸다. <br>
>
> 변수(variable)는 생성(create) -> 초기화(initialize) -> 사용(Use) 의 과정을 거친다. <br>

## Variable

let / const : let은  변할 수 있고, const는 상수를 의미한다.  
var 은 그냥 쓰지 말자. const, let이 있는한!  

> var로 선언 시, 동일 선언 가능 -> 에러x, 재할당 가능  
> let로 선언 시, 동일 선언 불가능-> 에러0, 재할당 가능   
> const로 선언 시, 동일 선언 불가능-> 에러0, 재할당 불가능 

```javascript
const what = " anything "	  :   String  
const what = 4		  :   Number  
const what = true	  :   boolean  
```

## Array

자바스크립트에서는 `Array` 객체로 배열을 다룸.  
객체 생성하는 것보다는.. 파이썬처럼 간단하게 생성해도 괜찮을 듯  

`let arr = []`

파이썬이랑 거의 비슷한 느낌, 필수 문법 정리

```javascript
let arr = ['사과', '바나나'];
let arr_1 = []

// 값 그대로 가져오기
for (i of arr){
    arr_1.push(i)
}

console.log("*".repeat(20))

// 뒤에 추가
arr_1.push("오렌지");
console.log(arr_1)
console.log("*".repeat(10))

// 뒤에 삭제
arr_1.pop();
console.log(arr_1)
console.log("*".repeat(10))

// 앞에 추가
arr_1.unshift("딸기")
console.log(arr_1)
console.log("*".repeat(10))

// 앞에 삭제
arr_1.shift()
console.log(arr_1)
console.log("*".repeat(10))

// forEach (enumerate와 비슷)
arr.forEach(function(item, index){
    console.log(item, index)
})

console.log("*".repeat(20))

let vegetables = ['양배추', '순무', '무', '당근']

let pos = 0
let n = 2

//해당 항목 제거 - pos: 시작 위치, n: 개수
let remove_vege = vegetables.splice(pos, n)
console.log(remove_vege)
console.log(vegetables)

console.log("*".repeat(20))
console.log("*".repeat(20))

// 얕은 복사
let vegetables_copy = vegetables
vegetables[0] = "토끼"
console.log(vegetables)
console.log(vegetables_copy)
vegetables[0] = "순무"

// 깊은 복사 (slice 활용)
vegetables_copy = vegetables.slice()
vegetables[0] = "토끼"
console.log(vegetables)
console.log(vegetables_copy)
```

## for문

동일한 결과를 보여주는 3가지 방법  

```
arr = [0,1,2,3]
```

1. 일반

    ```javascript
    for (var i=0; i <= arr.length; i++){
      console.log(arr[i])
    }

    // 0,1,2,3
    ```

2. of

    ```javascript
    for (var i of arr){
      console.log(i)
    }

    // 0,1,2,3
    ```

3. in

    ```javascript
    for (var i in arr){
      console.log(arr[i])
    }

    // 0,1,2,3
    ```


## hash map

1. Array 이용

    ```javascript
    let array = ['one', 'two', 'three', 'four']
    let hash = []

    array.forEach((entry, index) => hash[entry]=index)
    // 아래와 같은 뜻
    // array.forEach(function(entry, index){
    //   hash[entry]=index
    // })
    console.log(hash) // [ one: 0, two: 1, three: 2, four: 3 ]
    ```

2. Map 이용

    ```javascript
    let array = ['one', 'two', 'three', 'four']
    let map_t = new Map()

    array.forEach(function(item, index){
        map_t.set(item, index)
    })
    console.log(map_t)
    // Map(4) { 'one' => 0, 'two' => 1, 'three' => 2, 'four' => 3 }
    ```

## "=>" 화살표 함수

굉장히 많은 뜻이 담겨있음.  
여기서는 매개변수를 활용한 **콜백함수 만들기** (파이썬 lambda 같은 기능) 로 생각하자.  

[MDN Javascript](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)


## String

1. String to int

    ```javascript
    N = '2'
    arr = ['1', '2', '3', '4']

    console.log(parseInt(N)) // 2
    console.log(Number(N)) // 2
    console.log(arr.map(x => Number(x))) // [ 1, 2, 3, 4 ]
    // 안해도 숫자는 자동 형변환
    ```



2. int to String

    ```javascript
    N = 2
    arr = [0, 1, 2, 3]

    console.log(N.toString()) // '2'
    console.log(String(N)) // '2'
    console.log(arr.map(x => String(x))) // [ '0', '1', '2', '3' ]
    ```

3. join, split

    ```javascript
    int_array = [-0,-1,-2,-3]
    int_array = [0,1,2,3]

    join_array = int_array.join('') // 0123 (string)
    split_array = join_array.split('') // [ '0', '1', '2', '3' ] (Array)
    ```