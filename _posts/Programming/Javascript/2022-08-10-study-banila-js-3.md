---
layout: post
title: "[study] 바닐라 자바스크립트 3장"
date: 2022-08-10 19:41 +0900
categories: [Programming, Javascript]
tags: [javascript, 공부]
---

- 다시볼것: 3.0, 3.1
  
### ３.0 The Document Object

### ３.1 HTML in Javascript
> HTML 코드와 HTML element를 Javascript로 접근하는 방법을 배워보자.

console창에 다음을 입력해보자.
```javascript
document.getElementById("title")
```
![](/images/2022-08-10-study-banila-js-3/img-220810-200721-385.png)

JavaScript로 id = "title"을 가진 \<h1> 태그를 가져온다.  
이를 console창에 하지말고 app.js 파일에서 호출해보자.  

![](/images/2022-08-10-study-banila-js-3/img-220810-200839-175.png)
괄호 안에는 element의 id를 써야하는데, 보다시피 string이어야 한다.


```javascript
const title = document.getElementById("title");

console.log(title);
```
{: file="app.js" }

![](/images/2022-08-10-study-banila-js-3/img-220810-201206.png)

console.log() 대신, element를 더 자세하게 보여주는 console.dir()을 사용해보자.
```javascript
const title = document.getElementById("title");

console.dir(title);
```
{: file="app.js" }
![](/images/2022-08-10-study-banila-js-3/img-220810-201336.png)

h1태그 하나에서 가져올 수 있는 것들이 이렇게나 많다.  
여기서 특별히 중요한 것은 textContent 같은 것이다  
![](/images/2022-08-10-study-banila-js-3/img-220810-201500.png)

이 모든 것들은 HTML에 표현될 수 있다.  
예를 들어 autofocus: false를 알아보자.  
![](/images/2022-08-10-study-banila-js-3/img-220810-201643.png)

```html
<body>
    <h1 autofocus id="title">Grab me!</h1>
    <script src="app.js"></script>
</body>
```
{: file="index.html" }  
\<h1> 태그 내부에 `autofocus` 를 추가하면 된다.  
웹페이지를 새로고침해보면 autofocus가 true로 바뀐걸 확인할 수 있다.  

![](/images/2022-08-10-study-banila-js-3/img-220810-225109.png)


### ３.2 Searching For Elements
getElementById() 함수를 이전시간에 배웠다. 하지만 니꼬는 이 함수를 자주 쓰지 않는다. 그래서 이번엔 class 명을 사용하는 방법을 배워보자.  


```html
<body>
    <h1 class="hello">Grab me!</h1>
    <h1 class="hello">Grab me!</h1>
    <h1 class="hello">Grab me!</h1>
    <h1 class="hello">Grab me!</h1>
    <script src="app.js"></script>
</body>
```
{: file="index.html" }  

```javascript
const hellos = document.getElementsByClassName("hello");

console.log(hellos);
```
{: file="app.js" }

h1이 들어있는 배열이 출력된다.  
![](/images/2022-08-10-study-banila-js-3/img-220810-231349.png)



<br/>

```html
<body>
    <div class="hello">
        <h1>Grab me!</h1>
    </div>
    <script src="app.js"></script>
</body>
```
{: file="index.html" }

위와 같이 된 경우 h1 태그를 가져와보자

```javascript
const title = document.getElementsByTagName("h1");

console.log(title);
```  
{: file="app.js" }

h1이 하나만 들어있는 array가 나왔다.  
![](/images/2022-08-10-study-banila-js-3/img-220810-231917.png)


<br/>
<br/>
니꼬 기준에서 element를 가지고 오는 가장 멋진 방법은  
`querySelector`과 `querySelectorAll`이라고 한다.  
querySelector는 element를 CSS 방식으로 검색할 수 있다.  

아래는 CSS selector를 사용해 hello라는 class를 찾고, 그 안에 있는 h1을 가져오는 명령어이다.
```javascript
const title = document.querySelector(".hello h1")

console.log(title);
```
{: file="app.js" }

![](/images/2022-08-10-study-banila-js-3/img-220810-232522.png)

<br/>
<br/>


hello h1이 여러개인 경우
```html
<body>
    <div class="hello">
        <h1>Grab me1!</h1>
    </div>
    <div class="hello">
        <h1>Grab me2!</h1>
    </div>
    <div class="hello">
        <h1>Grab me3!</h1>
    </div>
    <script src="app.js"></script>
</body>
```
{: file: "index.html" }

첫 번째것만 나온다.
![](/images/2022-08-10-study-banila-js-3/img-220810-233016.png)

selector안의 조건에 부합하는 모든 element를 갖고오고 싶은 경우 `querySelectorAll` 명령어를 사용한다.
```javascript
const title = document.querySelectorAll(".hello h1")

console.log(title);
```

세 개의 h1이 들어있는 array가 출력된다.
![](/images/2022-08-10-study-banila-js-3/img-220810-233203.png)

<br/>
이 강의의 99%는 querySelector를 이용한다.  
만약에 id를 통해 찾고 싶다고 하더라도, #를 붙이면 querySelector를 활용해서 찾을 수 있다.  

```javascript
const title = document.querySelector("#hello")
const title = document.getElementById("hello")
```
{: file="app.js" }

두 코드는 같은 역할을 한다.  

### ３.3 Events

index.html 파일에서 app.js를 import했기 때문에  
javascript를 통해 HTML의 내용을 가져올 수 있는 것이다.  
![](images/2022-08-10-study-banila-js-3/img-220810-234011.png)

import를 하지 않았다면, app.js의 document는 존재할 수도 없었다.
![](images/2022-08-10-study-banila-js-3/img-220810-234138.png)

포인트는, HTML이 app.js를 load하기 때문에 존재하는 것이라는 거다.    
그 다음에 browser가 우리가 document에 접근할 수 있게 해준다.  

---

click event를 listen하고, 이 click event가 발생하면 특정 function이 동작하도록 해보자.  

function을 실행시키고 싶으면 함수명 옆에 ()괄호를 붙여야 했었다.  
하지만 지금은 함수를 곧바로 실행시키고 싶은 것이 아니다.  
function을 javascript에 넘겨주고, 유저가 title을 click할 경우 javascript가 대신 실행시키길 바라는 것이다.   
내가 직접 실행시키지 않고(괄호를 붙이지 않고), javascript에 function name만을 넘겨준다. 

```javascript
const title = document.querySelector(".hello h1")

function handleTitleClick() {
    console.log("title was clicked!");
}

title.addEventListener("click", handleTitleClick) 
// 어떤 event를 listen할지 지정, 해당 event가 발생했을때 어떤 함수를 실행할지 지정
```
{: file="app.js" }

h1 태그 부분을 클릭하면 콘솔 창에 문자가 출력되는 것을 볼 수 있다.
![](/images/2022-08-10-study-banila-js-3/img-220810-235433.png)

### ３.4 Events part Two

listen하고 싶은 event를 찾는 가장 좋은 방법:
`찾고 싶은 element의 이름 + html element mdn` 으로 구글에 검색한다.

`Web APIs` 라는 문장이 포함된 링크를 찾는다. (이게 javascript 관점에서 쓴 글이다)
![](/images/2022-08-10-study-banila-js-3/img-220811-010221.png)

HTMLHeadingElement는 HTMLElement이기 때문에 HTMLElement를 클릭한다
![](/images/2022-08-10-study-banila-js-3/img-220811-010331.png)

스크롤을 내려보면 Events 들을 볼 수 있다.
![](/images/2022-08-10-study-banila-js-3/img-220811-010513.png)


<br/>
또는 console.dir()로 element를 console에 출력시켜서 볼 수 있다.

```javascript
const title = document.querySelector(".hello h1")

console.dir(title);
```
{: file="app.js" }

많은 property들을 볼 수 있는데, 이름 앞에 on이 붙어 있는 것이 event listener이다.  
이 event를 사용할 때는 onmousedown 대신 mousedown으로 사용한다.  
![](/images/2022-08-10-study-banila-js-3/img-220811-010709.png)

---

마우스에 관련된 이벤트 리스너를 몇 개 더 추가해보자.
```javascript
const title = document.querySelector(".hello h1")

function handleTitleClick() {
    title.style.color = "blue";
}

function handleMouseEnter() {
    title.innerText = "Mouse is here!";
}

function handleMouseLeave() {
    title.innerText = "Mouse is gone!";
}

title.addEventListener("click", handleTitleClick);
title.addEventListener("mouseenter", handleMouseEnter);
title.addEventListener("mouseleave", handleMouseLeave);
```
{: file="app.js" }

### ３.5 More Events

event를 사용하는 데에는 기본적으로 두 가지 방법이 있다.
```javascript
title.addEventListener("click", handleTitleClick); // 1. 
title.onclick = handleTitleClick; // 2.
```
둘 다 같은 동작을 한다.  

니꼬가 addEventListener를 더 선호하는 이유는 나중에 removeEventListener를 통해 eventListener를 제거할 수 있기 때문이다.

---

window의 event를 listen 해보자.

https://developer.mozilla.org/ko/docs/Web/API/Window#%EC%9D%B4%EB%B2%A4%ED%8A%B8

위 링크에서 window에 대한 event를 볼 수 있다.  

![](/images/2022-08-10-study-banila-js-3/img-220811-012523.png)

니꼬는 resize 이벤트를 좋아한다고 한다. 이 event를 listen 해보자.  

<br/>
<br/>
JS에서 document가 기본적으로 제공되듯이, window도 기본적으로 제공된다.  

```javascript
function handleWindowResize() {
    document.body.style.backgroundColor = "tomato";
}

window.addEventListener("resize", handleWindowResize);
```
{: file="app.js" }

<br/>

document의 body를 출력해볼 수 있다.  
document의 body, head, title 이런 것들은 중요하기 때문에 이렇게 출력해볼 수 있다.  
대신 나머지 element들은 (div, h1.. 등등) querySelector나 getElementById등으로 찾아와야 한다.
![](/images/2022-08-10-study-banila-js-3/img-220811-013055.png)

---

이번엔 clipboard events의 copy event를 listen해보자.
![](/images/2022-08-10-study-banila-js-3/img-220811-013309.png)

```javascript
function handleWindowCopy() {
    alert("copier!");
}
window.addEventListener("copy", handleWindowCopy);
```
{: file="app.js" }

새로고침 후 ctrl + c 를 눌러보면 alert창이 뜨는 걸 볼 수 있다.
![](/images/2022-08-10-study-banila-js-3/img-220811-013448.png)

---

이번엔 wifi에 관련된 event를 써보자.  
![](/images/2022-08-10-study-banila-js-3/img-220811-013608.png)

```javascript
function handleWindowOffline() {
    alert("SOS no WIFI");
}
function handleWindowOnline() {
    alert("ALL GOOD");
}
window.addEventListener("offline", handleWindowOffline);
window.addEventListener("online", handleWindowOnline);
```
{: file="app.js" }

(난 왜 안되지..?)

### ３.6 CSS in Javascript

```javascript
const h1 = document.querySelector(".hello h1")

function handleTitleClick() {
    if (h1.style.color === "blue") {
        h1.style.color = "tomato";
    } else {
        h1.style.color = "blue";
    }
}

h1.onclick = handleTitleClick;
```
{: file="app.js" }

클릭할 때 마다 색깔이 바뀌는 위 코드를 개선해보자.

```javascript
const h1 = document.querySelector(".hello h1")

function handleTitleClick() {
    const currentColor = h1.style.color;
    let newColor;
    if (currentColor === "blue") {
        newColor = "tomato";
    } else {
        newColor = "blue";
    }
    h1.style.color = newColor;
}

h1.onclick = handleTitleClick;
```
{: file="app.js" }

하지만 element의 style을 JS에서 변경하는 건 별로 좋지 않다.  

### ３.7 CSS in Javascript part Two
style 작업에 적합한 도구는 CSS이다.  
JS에는 색깔 이름을 사용하지 않을 거고 style이름도 적지 않을 거다.  
style은 CSS 파일에 적자.  

아래 코드는 h1 태그를 파란색으로 만든다.
```css
body {
    background-color: beige;
}

h1 {
    color: blue;
}
```
{: file="style.css" }

아래에 active 클래스 생성하자. 이 클래스를 어떤 element에 지정해주면 tomato 색이 될 것이다.
```css
.active {
    color: tomato;
}
```

JS에서 h1에 active class를 전달해주자.
```javascript
const h1 = document.querySelector(".hello h1")

function handleTitleClick() {
    h1.className = "active";
}

h1.onclick = handleTitleClick;
```
{: file="app.js" }
이제 JS가 CSS에게 직접 대화하지 않게 되었다.  
JS는 HTML을 변경한다. 

클릭시 active class가 된다.  
![](/images/2022-08-10-study-banila-js-3/img-220811-031018.png)

<br/>
<br/>
다시 클릭하면 class 를 없앰으로써 아까와 같은 동작을 구현해보자.

```javascript
const h1 = document.querySelector(".hello h1")

function handleTitleClick() {
    if(h1.className == "active") {
        h1.className = ""; // className을 비움
    } else {
        h1.className = "active";
    }
}

h1.onclick = handleTitleClick;
```
{: file="app.js" }


h1에 굉장히 멋진 transition을 추가해보자.
```css
body {
    background-color: beige;
}

h1 {
    color: blue;
    transition: color .5s ease-in-out;
}

.active {
    color: tomato;
}
```
{: file="style.css" }


<br/>
JS 코드를 개선해보자.  
현재 "active"란 string을 두 번 사용하고 있다. 이는 error의 소지를 갖고 있다.  
clickedClass라는 constant를 생성해주자. string을 변수에 저장하는 건 아주 유용하다.  

```javascript
const h1 = document.querySelector(".hello h1")

function handleTitleClick() {
    const clickedClass = "active";
    if(h1.className == clickedClass) {
        h1.className = ""; // className을 비움
    } else {
        h1.className = clickedClass;
    }
}

h1.onclick = handleTitleClick;
```
{: file="app.js" }


<br/>
<br/>
<br/>
현재 JS 코드에 버그의 소지가 하나 더 있다.
만약 h1 태그에 class가 이미 적용돼있었다면? (ex: font를 적용해놓은 class)  

<br/>
현재 JS 코드는 class name을 교체(replace)해버리기 때문에 적용해놓은 class가 사라진다.  
우리는 기존에 있던 class name을 유지해야 한다. 

### ３.8 CSS in Javascript part Three
class name을 바꾸는 다른 방법을 배워보자: classList를 사용하는 방법이다.  

https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList  
classList에 적용할 수 있는 method들은 위 주소에서 확인할 수 있다.
```javascript
const h1 = document.querySelector(".hello h1")

function handleTitleClick() {
    const clickedClass = "active";
    if(h1.classList.contains(clickedClass)) { // clickedClass가 포함돼있는지 확인
        h1.classList.remove(clickedClass);
    } else {
        h1.classList.add(clickedClass);
    }
}

h1.onclick = handleTitleClick;
```
{: file="app.js" }

<br>

위 코드 대신 더 간단한 toggle()함수를 써보자.  
toggle()은 class name이 존재하는지 확인하고, 존재한다면 class name을 제거한다. 존재하지 않는다면 class name을 추가한다.

```javascript
const h1 = document.querySelector(".hello h1")

function handleTitleClick() {
    // const clickedClass = "active";
    // if(h1.classList.contains(clickedClass)) { // clickedClass가 포함돼있는지 확인
    //     h1.classList.remove(clickedClass);
    // } else {
    //     h1.classList.add(clickedClass);
    // }
    h1.classList.toggle("active");
}

h1.onclick = handleTitleClick;
```
{: file="app.js" }
단 한 줄의 코드로 이전의 코드를 대체할 수 있다.