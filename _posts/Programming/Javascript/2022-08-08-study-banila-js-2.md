---
layout: post
title: "[study] 바닐라 자바스크립트 2장"
date: 2022-08-08 01:41 +0900
categories: [Programming, Javascript]
tags: [javascript, 공부]
---

## ２. WELCOME TO JAVASCRIPT
- 다시보기
    2.0 , 2.6

- 다시 안봐도 될것
  - 2.1 2.2

### ２.1 Basic Data Types

가장 기본적인 데이터 타입: 문자(string), 숫자(integer, float) 존재  

### ２.2 Variables
> 어떻게 값을 variable에 저장하고 사용하는지를 배운다.

`console.log(4545);` : 괄호 안의 것을 console에 log(또는 print) 하는 것  

자바스크립트에서의 변수명 짓는 관례: camelCase (ex: `const veryLongVariableName = 3`)  
<-> 파이썬에서의 변수명 짓는 관례: snake_case (ex: `very_long_variable_name = 3`)  

### ２.3 const and let

자바스크립트에는 변수를 만드는 방법이 2가지 존재함: let, const  
- `const`: 상수, 값을 변경 불가능
- `let`: 변할 수 있는 변수

> 기본적으로 `const`를 사용하고, 만약 변수를 업데이트하고 싶다면 `let`을 씀

<br/>
`var`은 절대 사용하지 말 것


### ２.4 Booleans
`true`, `false` 두개 존재

```javascript
const amIFat = false;
console.log(amIFat);
```

##### 그 외 false 와 헷갈릴만한 data type들
```javascript
const amIFat = null; // 값이 null이고, null은 아무것도 없음을 의미

let something; // 변수는 존재하나 값이 들어가지 않음
console.log(something); // undefined

```
- `null`: 값이 "비어있음"을 표현하기 위해 사용, 절대 자연적으로 발생하지 않음. variable안에 어떤 것이 없다는 것을 확실히 하기 위해 사용함. 
- `false`: false라는 값이 들어 있음
- `undefined`: 변수에 값을 부여하지 않은 상태 

### ２.5 Arrays

```javascript
const nonsense = [1, 2, "hello", false, null, true, undefined];

const daysOfWeek = ["mon", "tue", "wed", "thu", "fri", "sat"];
console.log(daysOfWeek);


// Get Item from Array
console.log(daysOfWeek[5]); // sat

daysOfWeek[1] = "MON"; // 값 업데이트

// Add one more day to the array
daysOfWeek.push("sun");
console.log(daysOfWeek);
```

### ２.6 Objects
배열은 같은 종류(type)들을 저장할 때 사용함 (ex: 한 주의 요일들을 저장)  
object은 연관되어 있는 property 들을 그룹으로 묶어서 저장해야 할 떄 사용함  
```javascript
const playerName = "nico";
const playerPoints = 121212;

  
const player = {
    name: "nico", // property
    points: 10,
    fat: true,
}

  
console.log(player);

  
/* 값 조회 */
console.log(player.name);
console.log(player["name"]); // 위와 같은 결과

/* 값 수정 */
player.fat = false; // const 안의 값을 업데이트 하는 것은 문제 없음
// player = false // const 전체를 업데이트할 때 에러 발생
player.points = player.points + 15;
console.log(player);

/* 값 추가 */
player.lastName = "potato"
console.log(player);
```

### ２.7 Functions part One
```javascript
function sayHello() {
    console.log("Hello my name is C!");
}

sayHello(); // 함수 실행
```
### ２.8 Functions part Two
> function에 argument 전달하는 법을 배운다.

```javascript
function sayHello(nameOfPerson, age) { // function이 데이터를 받는 방법
    console.log("Hello my name is " + nameOfPerson + " and I'm " + age);
}

sayHello("nico", 10); // 데이터를 function 안으로 보냄
```

```javascript
function plus(a, b) { // argument의 이름은 마음대로 지어도됨
    console.log(a + b);
    // 변수 a, b는 이 function 블록 내부에서만 존재함

}
// console.log (a + b); // function 블럭 외부에서 접근할 시 에러 발생

  
plus(); // NaN (Not a Number), argument를 전달하지 않아도 실행은 됨
plus(8, 60); // a에 8이 들어가고 b에 60이 들어감 (변수 전달 순서가 중요)

  
function divide(a, b) {
    console.log(a / b);
}
divide(98, 20);
```

```javascript
function minusFive(potato) {
	console.log(potato - 5);
}

minusFive(5, 10, 12, 34); // 5
```
위 function이 오직 첫 번째 argument만 받지만, 많은 argument를 보내도 문제가 되지 않음.  

```javascript
function sayHello() {
}

const player = {
    name: "nico",
    // object 내부에 function 선언할 땐 외부에서 선언할 때와 모양이 살짝 다름
    sayHello: function(otherPersonName) {
        console.log("hello! " + otherPersonName);
    },
};

console.log(player.name);
player.sayHello("lynn");
```

### ２.9 Recap
### ２.11 Returns
앞으론 어떤 작업을 처리하고 그 작업의 결과를 return 하기 위해 function을 사용할 것임  
```javascript
const age = 96;

function calculateKrAge(ageOfForeigner) {
    return ageOfForeigner + 2;
}

const krAge = calculateKrAge(age);
console.log(krAge);
```

### ２.13 Conditionals

prompt()는 사용자에게 창을 띄울 수 있는 함수이다.
```javascript
const age = prompt("How old are you?");

console.log(age);
```

<br/>

실행시켜보면 페이지가 계속 로딩하는 것처럼 보이고, console에는 아무것도 출력되지 않는다.
![](../../../images/2022-08-08-study-banila-js/img-220810-031417-767.png)

이 페이지는 javascript를 일시정지 시키고 있는 것이다.

```javascript
const age = prompt("How old are you?"); // <---javascript가 여기서 멈춰있다

console.log(age);
```

prompt function을 더 이상 사용하지 않는 이유는 자바스크립트 코드의 실행을 멈추게 하기 때문이다.  
추가로 CSS를 적용시킬 수가 없다.  
이는 아주아주 오래된 방법이다.  

요즘에는 대부분이 HTML, CSS로 만든 자신만의 창을 사용한다.  


<br/>
<br/>
변수의 type을 보려면 `typeof` 키워드를 사용한다.
```javascript
const age = prompt("How old are you?"); // <---javascript가 여기서 멈춰있다

console.log(age);
console.log(typeof age); // string
```

`parseInt()` 함수로 string을 number로 변환한다.  
숫자가 아닌 문자를 입력하면 NaN(Not A Number)이 출력된다
```javascript
console.log(typeof "15", typeof parseInt("15")); // string number
```

```javascript
const age = prompt("How old are you?"); // <---javascript가 여기서 멈춰있다

console.log(age, parseInt(age));
```

### ２.14 Conditionals part Two
`insNaN()`: NaN인지 검사하는 함수, boolean을 return한다.
![](../../../images/2022-08-08-study-banila-js/img-220810-033908-920.png)

문자를 입력할 경우 Not A Number이므로 true가 반환된다.  

<br/>
조건문을 배워보자.
```javascript
if(condition) {
    // condition === true 일 경우 실행되는 코드 블럭
} else {
    // condition === false 일 경우 실행되는 코드 블럭
}
```
condition(조건) 자리에는 boolean(true 또는 false)이 들어가야 한다.  
isNaN()함수가 boolean을 반환하므로 condition 자리에 넣어보자.  

```javascript
const age = parseInt(prompt("How old are you?"));

if(isNaN(age)) {
    console.log("Please write a number")
} // else문은 optional
```

### ２.15 Conditionals part Three
else if로 더 많은 conditon을 체크해보자.  

`&&`(AND 연산자): 두 조건이 모두 true여야 true가 된다  
`||`(OR 연산자): 두 조건 중 하나만 true여도 true가 된다  
```javascript
const age = parseInt(prompt("How old are you?"));

if(isNaN(age) || age < 0) {
    console.log("Please write a real positive number");
} else if(age < 18) {
    console.log("You are too young.");
} else if(age >= 18 && age <= 50) { // AND 연산자
    console.log("You can drink");
} else if(age > 50 && age <= 80) {
    console.log("You should exercise");
} else if(age > 80) {
    console.log("You can do whatever you want.");
}
```

### ２.16 Recap
특별한 나이 100살인 경우를 따로 조사해보자.  

```javascript
const age = parseInt(prompt("How old are you?"));

if(isNaN(age) || age < 0) {
    console.log("Please write a real positive number");
} else if(age < 18) {
    console.log("You are too young.");
} else if(age >= 18 && age <= 50) { // AND 연산자
    console.log("You can drink");
} else if(age > 50 && age <= 80) {
    console.log("You should exercise");
} else if(age > 80) {
    console.log("You can do whatever you want.");
} else if(age === 100) { // 이 조건은 절대 실행되지 않는다
    console.log("wow you are wise");
}
```
위와 같이 작성하면 age가 80이상이기만 하면 12번째 줄이 실행되고 끝나기 때문에  
age가 100인지 체크하는 13번째 줄은 실행되지 않는다.  
적는 순서에 관해 잘 생각해 보아야 한다.  age가 100인지를 먼저 체크하도록 하자.

```javascript
const age = parseInt(prompt("How old are you?"));

if(isNaN(age) || age < 0) {
    console.log("Please write a real positive number");
} else if(age < 18) {
    console.log("You are too young.");
} else if(age >= 18 && age <= 50) { // AND 연산자
    console.log("You can drink");
} else if(age > 50 && age <= 80) {
    console.log("You should exercise");
} else if(age === 100) { // 이 조건은 절대 실행되지 않는다
    console.log("wow you are wise");
} else if(age > 80) {
    console.log("You can do whatever you want.");
}
```
