---
layout: single
title: "다양한 Document.method"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [dom, create] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# create

## Document.createElement()

## Document.createTextNode()

<span style="color:red">Document.createElement()</span> 메서드는 지정한 tagName의 `HTML 요소를 만들어 반환`한다.

```html
<!-- html -->
<!DOCTYPE html>
<html>
  <head>
    <title>||Working with elements||</title>
  </head>
  <body>
    <div id="div1">위의 텍스트는 동적으로 추가했습니다.</div>
  </body>
</html>
```

```java
// javascript
document.body.onload = addElement;

function addElement () {
  var newDiv = document.createElement("div");
  // and give it some content
  var newContent = document.createTextNode("환영합니다!");
  // add the text node to the newly created div
  newDiv.appendChild(newContent);

  // add the newly created element and its content into the DOM
  var currentDiv = document.getElementById("div1");
  document.body.insertBefore(newDiv, currentDiv);
}
```

- var <span style="color:green">newDiv</span> = document.createElement("div");  
  newDiv에는 createElement("div")를 사용하여

# Document.createTextNode()

# Selector

## getElementById

<span style="color:red">ID를 통해서</span> element를 반환한다. <u>document에 해당 ID의 element가 없다면</u> `null을 반환`한다.

## querySelector

document.<span style="color:red">querySelector()</span>는 <u>제공한 선택자 또는 선택자 뭉치</u>와 일치하는 문서 내 `첫 번째 element를 반환`한다.  
<u>일치하는 element가 없다면 null</u>을 반환한다.

### querySelector와 selectElementById의 비교

```html
<form id="userForm">
  <input id="username" type="text" value="Guilherme" />
</form>
```

위의 HTML 코드에서 username을 선택하여 변수에 할당하고 싶다면,  
getElementById를 사용해서는 이렇게 할 수 있고

```javascript
let username = document.getElementById("username");
```

querySelector를 가지고는 아래와 같이 할 수 있다.

```javascript
let username = document.querySelector("#userForm #username");
```

이렇게 직접 이 2개의 방법을 놓고보면, `querySelector`를 사용하는 방법이 element를 가지고  
오기 위해서 <span style="color:red">더 구체적으로 선택한다</span>는 것을 알 수 있다.

## getElementsByClassName

## getElementsByTagName

## querySelectorAll

```html
<main>
  <input type="text" placeholder="전화번호, 사용자 이름 또는 이메일" />
  <input type="password" placeholder="비밀번호" />
  <button id="login_btn">로그인</button>
</main>
```

```javascript
const inputs = document.querySelectorAll("input");
console.log(inputs); //output == NodeList(2) [input, input]
console.log(inputs[0]); //output == <input type="text" placeholder="전화번호, 사용자 이름 또는 이메일" />
```

이렇게 const input을 console로 확인해보면, <span style="color:red">NodeList라는 이름의 array</span>로 반환된다!  
`array이기 때문에 index를 사용`하여 다시 console.log를 해보면 <u>위의 결과처럼 [0] input의 값이 반환</u>된다!

### querySelectorAll와 selectElementByClassName의 차이

```html
<form id="productForm">
  <input id="productOne" class="product" type="text" value="Product 1" />
  <input id="productTwo" class="product" type="text" value="Product 2" />
  <input id="productThree" class="product" type="text" value="Product 3" />
</form>
```

위의 html을 기준으로, getElementsByClassName을 사용하려면 아래와 같고

```javascript
let products = document.getElementsByClassName("product");
```

querySelectorAll를 사용하려면 아래와 같다.

```javascript
let products = document.querySelectorAll("#productForm .product");
```

`getElementsByClassName`에서는 <u>HTMLCollection</u>이 반환되고,  
`querySelectorAll`에서는 <u>NodeList</u>가 반환된다.  
HTMLCollection은 <span style="color:red">name, id 속성으로도 접근</span>이 가능하지만,  
NodeList는 <span style="color:red">index 번호로만 접근</span>이 가능하다.

<!-- ### 2. Link 넣기

```

유형 1: (설명어를 입력) : [gunhee's coding blog](https://gunhee-jeong.github.io/)
유형 2: (URL 자동연결) : <https://gunhee-jeong.github.io/>
유형 3: (동일 파일 내 '문단으로 이동') : [1. Header로 이동](###-1-header)

```

유형 1: (설명어를 입력) : [gunhee's coding blog](https://gunhee-jeong.github.io/)
유형 2: (URL 자동연결) : <https://gunhee-jeong.github.io/>
유형 3: (동일 파일 내 '문단으로 이동') : [1. Header로 이동](#1-header)
유형 3의 방법

1. 특수문자를 제거
2. 스페이스는 -로 바꾸고
3. 대문자는 소문자로!
   그래서 ### 1. Header -> #1-header

## Link: [google][https://www.google.com/]

### 3. 수평선

```

---

```

---

### 4. 라인 바꾸기

```

스페이스바를 2번 눌러주면 다음칸으로
이동할 수 있어요!

```

---

스페이스바를 2번 눌러주면
다음칸으로 이동할 수 있어요!

### 5. list 만들기

```

1. 1번
2. 2번
3. 3번

- 순서없는 list
  - 순서없는 list
    - 순서없는 list

```

1. 1번
2. 2번
3. 3번

- 순서없는 list
  - 순서없는 list
    - 순서없는 list

---

### 6. font 관련

```

**진하게** -> 볼드
_기울여서_ -> 이탤릭체
~~취소선~~ -> 취소선

<ul>밑줄넣기</ul> -> 밑줄
<span style="color:red">빨간 글씨</span> -> 글자색
이것이 `인라인` 입니다 -> 인라인 코드
```

**진하게** -> 볼드
_기울여서_ -> 이탤릭체
~~취소선~~ -> 취소선
<u>밑줄넣기</u> -> 밑줄
<span style="color:red">빨간 글씨</span>
이것이 `인라인` 입니다 -> 인라인 코드

---

### 7. 인용구문

```
> coding
>
> > JavaScript
> >
> > > 내가 프짱!
```

> coding
>
> > JavaScript
> >
> > > 내가 프짱!

---

### 8. 이미지 삽입

```
유형1: ('사이즈를 조절' -> HTML 태그 사용) : <img src="https://gunhee-jeong.github.io/assets/images/blogLogo.png" width="300" height="200">
유형2: (이미지 삽입 후 -> 링크 걸기)
[![이미지](https://gunhee-jeong.github.io/assets/images/blogLogo/blogLogo.png)](https://gunhee-jeong.github.io/)
```

유형1: ('사이즈를 조절' -> HTML 태그 사용) : <img src="https://gunhee-jeong.github.io/assets/images/blogLogo.png" width="300" height="200">
유형2: (이미지 삽입 후 -> 링크 걸기)
[![이미지](https://gunhee-jeong.github.io/assets/images/blogLogo.png)](https://gunhee-jeong.github.io/)

### 9. 표 만들기

```
||국어|영어|
| :--- | ---: | :--: |
|건희 | 100점 | 100점
|철수 | 100점 | 100점
```

|      |  국어 | 영어  |
| :--- | ----: | :---: |
| 건희 | 100점 | 100점 |
| 철수 | 100점 | 100점 |

> - header를 넣고 싶은 경우 ---을 사용하고 :을 이용하여 정렬에 사용함!

### 10. 토글 만들기

```
<details>
<summary>여기를 누르세요</summary>
<div markdown="1">
숨겨진 내용
</div>
</details>
```

<details>
<summary>여기를 누르세요</summary>
<div markdown="1">
숨겨진 내용
</div>
</details> -->
