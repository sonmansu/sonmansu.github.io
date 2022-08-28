---
layout: post
title: "[study] 바닐라 자바스크립트 4장"
date: 2022-08-11 16:43 +0900
categories: [Programming, JavaScript]
tags: [javascript, 공부]
---

### 4.0 Input Values

```html
<body>
    <div id="login-form">
        <input type="text" placeholder="What is your name?">
        <button>Log In</button>
    </div>
    <script src="app.js"></script>
</body>
```
-index.html

```j-
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");
const loginButton = loginForm.querySelector("button");

function onLoginBtnClick() {
    // console.dir(loginInput); // input의 내용을 가져오는 property를 찾아보기 위해 출력
    console.log(loginInput.value);
    console.log("click!!");
}
loginButton.addEventListener("click", onLoginBtnClick);
```
-app.js

### 4.1 Form Submission
유효한 username이 입력됐는지 체크해보자.

```j-
function onLoginBtnClick() {
    const username = loginInput.value;
    if(username === "") { // 비어있는 경우
        alert("Please write your name");
    } else if (username.length > 15) {
        alert("Your name is too long.");
    }
}
```

위와 같이 JS로 유효성을 확인할 수도 있지만, 브라우저 자체의 기능을 사용할 수도 있다. 그리고 이미 가지고 있는 기능들을 사용하는 게 좋다.  

HTML파일에서 input에 아래와 같은 속성을 추가로 입력한다.  
`required`: 필수 입력 항목으로 만들어줌  
`maxlength="15"`: 최대 길이를 지정  

그리고 input의 유효성 검사를 작동시키기 위해서는, input이 form안에 있어야 한다. div를 form으로 수정해주자.

```html
<body>
    <form id="login-form">
        <input 
            required 
            maxlength="15" 
            type="text" 
            placeholder="What is your name?"
        />
        <button>Log In</button>
    </form>
    <script src="app.js"></script>
</body>
```

그리고 JS에서는 간단히 username만 출력하자.
```j-
function onLoginBtnClick() {
    const username = loginInput.value;
    console.log(username);
}
```

웹페이지를 새로고침하고 확인하자.  
아무것도 입력하지 않은 체로 Log In버튼을 누르면 아래와 같은 창이 뜬다.

그리고 15자 이상으로 입력이 되지 않는 걸 확인할 수 있다.
![](/images/2022-08-11-study-banila-js-4/img-220811-173013.png)

<br/>
<br/>
현재 문제는, name 입력 후 Log In을 클릭하면 URL에 `?`가 따라 붙고,  페이지가 새로고침 돼서 값이 사라져버린다.  
![](/images/2022-08-11-study-banila-js-4/img-220811-173220.png)

이렇게 되는 이유는 form이 submit되고 있기 떄문이다.  
\<form> 안에 있는 \<button> 또는 \<input type="submit"> 을 클릭하면 내가 작성한 form이 submit된다. 또는 엔터를 누르면 자동으로 submit 된다. (input이 더 존재하지 않는다면 )

<br/>
우리는 HTML의 도움을 활용하기 위해 (required, maxlength 등..) \<input>을 \<form>안에 위치시켰다. 그리고 \<input>을\<form>안에 넣었을 경우 엔터를 누를 때마다 form은 자동적으로 submit되고 있고, form이 submit될 때마다 페이지가 새로고침 된다.   
그러나 우리는 웹사이트 전체를 매번 새로고침 하고 싶지 않다.  

### 4.2 Events

현재 form이 submit되는 것에 관심이 있다.  submit은 엔터를 누르거나 버튼을 클릭할 때 발생한다.  
submit이라는 event가 발생하는 걸 아예 막거나, 중간에 개입해보기 위해 submit event를 listen하자.  
```j-
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");

function onLoginSubmit() {
    const username = loginInput.value;
    console.log(username);
}

loginForm.addEventListener("submit", onLoginSubmit);
```
-app.js

<br/>
<br/>
아래 코드는 누군가 form을 submit하면 JS가 onLoginSubmit 함수를 호출하도록 하고 있다.
```j-
loginForm.addEventListener("submit", onLoginSubmit);
```
이때, JS는 해당 함수를 `onLoginSubmit()`로 호출하지 않고, 함수의 첫 번째 argument로, 발생한 event에 대한 정보를 담은 object을 전달한다.  

모든 EventListener function의 첫 번째 argument는 항상 지금 막 벌어진 일들에 대한 정보가 된다.  
해당 정보를 출력해보자. argument의 이름은 tomato로 짓던, info로 짓던 상관 없다.  (보통 event라고 작성하는게 관행이다)

`preventDefault` 함수는 어떤 event의 기본 행동이 발생되지 않도록 막는다.  
여기서 기본 행동이란 어떤 function에 대해 브라우저가 기본적으로 수행하는 동작이다. 누군가 form을 submit하면 브라우저는 기본적으로 페이지를 새로고침 하도록 프로그래밍 되어있다. 그 기본 동작을 막고 있는 것이다.  
```j-
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");

function onLoginSubmit(event) {
    event.preventDefault(); // 브라우저의 기본 동작을 막음
    console.log(event);
}

loginForm.addEventListener("submit", onLoginSubmit);
```
-app.js

여기 있는 것들이 방금 실행된 event에 대한 여러 정보들이다.  

![](/images/2022-08-11-study-banila-js-4/img-220811-180907-510.png)

### 4.3 Events part Two
form에 관련한 요소들을 배우자.
```html
<body>
	<a href="https://nomadcoders.co">Go to courses</a>
</body>
```

이전 영상에서 form의 기본 동작은 submit이라는 걸 배웠다.  
링크의 기본 동작은 클릭 시 다른 페이지로 이동하는 것이다. 이 기본 동작을 막아볼 것이다.

```j-
const link = document.querySelector("a");

function handleLinkClick() {
    alert("clicked"); // <--- JS의 동작이 멈춘다
}

link.addEventListener("click", handleLinkClick);
```

웹페이지를 새로고침 후 실행해본다.  
링크를 클릭하면 alert창이 뜬다. 확인 버튼을 눌러서 alert가 없어지면 브라우저의 기본 동작이 실행된다.  

방금 일어난 event에 대한 정보를 담은 object이 EventListener 함수의 첫번째 인자로 주어지게 될 것이다. 해당 argument를 받아서 출력해보자
```j-
const link = document.querySelector("a");

function handleLinkClick(event) {
    console.log(event);
    alert("clicked"); // <--- JS의 동작이 멈춘다
}

link.addEventListener("click", handleLinkClick);
```

아까 전에는 SubmitEvent가 출력됐는데, 이번에는 PointerEvent가 출력됐다. 이는 event의 종류가 다양하기 때문이다.  
(니꼬는 MouseEvent가 뜬다. 이는 브라우저나 OS가 다르기 때문이라고 한다.)
![](/images/2022-08-11-study-banila-js-4/img-220811-190215-876.png)


<br/>
기본 동작을 막고 event 내부를 출력하자.
```j-
const link = document.querySelector("a");

function handleLinkClick(event) {
    event.preventDefault(); // 브라우저의 기본 동작을 막는다.
    console.dir(event);
}

link.addEventListener("click", handleLinkClick);
```

![](/images/2022-08-11-study-banila-js-4/img-220811-190946-257.png)


### 4.4 Getting Username
유저가 이름을 제출하면 form 자체가 사라지도록 할 것이다.  
이를 구현하기 위해선, HTML 요소 자체를 없애는 방법과 CSS를 이용해서 숨기는 방법이 있다.

style.css에 hidden 클래스를 만든다.  
어떤 요소에게든 이 classname을 주면 그 요소를 숨기게 될 거다.
```css
.hidden {
    display: none;
}
```
-style.css

```j-
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");

function onLoginSubmit(event) {
    event.preventDefault(); // 브라우저의 기본 동작을 막음
    const username = loginInput.value;
    loginForm.classList.add("hidden"); // form 요소를 숨김
    console.log(username);
}

loginForm.addEventListener("submit", onLoginSubmit);
```
-app.js

---
완성 코드
```html
<!DOCTYPE html>
<html lang="kr">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Momentum</title>
</head>
<body>
    <form id="login-form">
        <input 
            required 
            maxlength="15" 
            type="text" 
            placeholder="What is your name?"
        />
        <button>Log In</button>
    </form>
    <h1 id="greeting" class="hidden"></h1>
    <script src="app.js"></script>
</body>
</html>
```
-index.html

```j-
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");
const greeting = document.querySelector("#greeting");

const HIDDEN_CLASSNAME = "hidden"; // 일반적으로 string을 저장하는 변수는 대문자로 표기

function onLoginSubmit(event) {
    event.preventDefault(); // 브라우저의 기본 동작을 막음
    loginForm.classList.add(HIDDEN_CLASSNAME); // hihdden class name을 더해서 form 요소를 숨김
    const username = loginInput.value; // 유저의 이름을 변수로 저장
    greeting.innerText = `Hello ${username}`; // "Hello " + username 대신 백틱 사용하는 것이 편함
    greeting.classList.remove(HIDDEN_CLASSNAME);
}

loginForm.addEventListener("submit", onLoginSubmit);
```
-app.js

<br/>
현재 문제는 우리가 유저를 전혀 기억할 수 없다는 것이다.   
새로고침할 때마다 새로 로그인 해줘야 한다.    
새로고침해도 이름이 저장되어있음 좋겠다.  

### 4.5 Saving Username
