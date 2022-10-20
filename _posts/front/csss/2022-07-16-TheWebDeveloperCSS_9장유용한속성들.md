---
layout: single
title: "The Web Developer CSS -> 9장 CSS 유용한 속성들"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer CSS] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-16T09:30:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.crimson {
  color: crimson;
  font-weight: bold;
}

.mediumblue {
  color: mediumblue;
  font-weight: bold;
}

.forestgreen {
  color: forestgreen;
  font-weight: bold;
}

.black {
  color: black;
  font-weight: bold;
}
</style>

# The Web Developer CSS -> 9장 CSS 유용한 속성들
# 🔴 CSS 박스 모델
## 🟠 Opacity and Alpha Channel
### 🟡 Alpha Channel
`alpha channel`은 색상이 비치는 정도, 즉 <span style="color:red">투명도</span>를 결정하게 된다.  
alpha channel은 <u>0에서 1사이의 값</u>이다. -> <span style="color:blue">1은 불투명</span>을 <span style="color:blue">0은 완전한 투명</span>을 의미한다.    

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <section>
    <div id="rgba"></div>
  </section>
</body>
```

```css
section {
  width: 500px;
  height: 500px;
  background-color: magenta;
}

#rgba {
  width: 50%;
  height: 50%;
  background-color: white;
}

#rgba {
  width: 50%;
  height: 50%;
  background-color: rgba(255, 255, 255, 1);
}
```

<img src="https://user-images.githubusercontent.com/87808288/179327820-ef20d55a-b260-4fe2-9d1e-66bd4cbcade2.png" width="400">  
위의 그림과 같이 background-color: rgba(255, 255, 255, 1); 에서 1은 불투명을 의미한다.  

### 🟡 Opacity
<u>alpha channel과 opacity 사이에는 큰 차이점</u>이 있는데  
`opacity`에서는 버튼이나 font 들도 불투명도에 영향을 미친다는 점이다.  
<span style="color:tomato">전체 요소들이 opacity 속성에 영향을</span> 받게 된다.  
alpha channel에서는 font 등은 영향을 받지 않았지만, opacity에서는 font와 태그들도 모두 영향을 받는다.  
<img src="https://user-images.githubusercontent.com/87808288/179327955-8e294465-f366-49e0-9915-ab47d83241d6.png" width="400">  

## 🟠 위치 속성
### 🟡 static
### 🟡 relative
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <h1>Position Property</h1>
  <section id="static">
    <h2>Static</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
  <section id="relative">
    <h2>relative</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
</body>
```

```css
div {
  width: 100px;
  height: 100px;
  background-color: yellowgreen;
  border: 2px solid black;
  margin: 10px;
  display: inline-block;
}

#middle {
  background-color: aquamarine;
}

#relative #middle {
position: relative;
top: 100px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/179328519-74230bd0-9f6b-49a5-b330-02fed7fb08ee.png" width="300">  
`relative`는 위의 이미지와 같이 <span class="crimson">원래의 위치</span>에서 <span class="mediumblue">상대적인 위치로 이동</span>하게 된다.

### 🟡 absolute
  <img src="https://user-images.githubusercontent.com/87808288/179328853-ee966c76-0ae1-4aea-8b43-139226871c6e.png" width="300">

```css
#absolute #middle {
  background-color: red;
  position: absolute;
}
```

위의 이미지와 같이 absolute 를 사용할 박스의 색상을 red 로 지정했다.

아래의 이미지에서는, <u>absolute 속성</u>을 사용하자 aquamarine 색상의 div위로 <span class="forestgreen">middle div(absolute red 박스)가 올라가 있는</span> 것을 확인할 수 있다. (middle div 아래에 aquamarine이 깔려있다.)

```css
div {
  width: 100px;
  height: 100px;
  background-color: yellowgreen;
  border: 2px solid black;
  margin: 10px;
  display: inline-block;
}

#middle {
  background-color: aquamarine;
}

#relative #middle {
position: relative;
top: 100px;
}

#absolute #middle {
  background-color: red;
  position: absolute;
  top: 50px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/179328979-197cbc2b-795e-46bf-a7e0-98abdd5e1f18.png" width="300">  
<u>top: 50px;</u>을 주면 이렇게 원래의 위치에서 상대적으로 이동하는 것이 아닌 <span class="forestgreen">예상치 못한 곳에 위치하고</span> 있다. `absolute`를 사용하면 요소가 문서의 <span class="mediumblue">일반적인 흐름에서 제거</span>되어 <span class="crimson">가장 가까이 있는 조상 요소를 기준으로 이동</span>하게 된다. <u>문서에서 제거되어 이동</u>하기 때문에 red div의 <span class="mediumblue">빈자리를 yellowgreen div가 차지</span>하는 것을 확인할 수 있다.

<u>조상 요소들에 posotion이 지정되어 있지 않다면</u> <span class="crimson">&lt;body&gt;를 기준으로 이동</span>하는데 이때 <span class="mediumblue">조상 요소의 위치를 기준</span>으로 위쪽(top), 아래쪽(bottom), 왼쪽(left), 오른쪽(right)에서 얼마큼 이동할 것인지 결정하게 된다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <h1>Position Property</h1>
  <section id="static">
    <h2>Static</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
  <section id="relative">
    <h2>relative</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
  <section id="absolute">
    <h2>absolute</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
</body>
```

```css
div {
  width: 100px;
  height: 100px;
  background-color: yellowgreen;
  border: 2px solid black;
  margin: 10px;
  display: inline-block;
}

#middle {
  background-color: aquamarine;
}

#relative #middle {
position: relative;
top: 100px;
}

#absolute #middle {
  background-color: red;
  position: absolute;
  top: 50px;
}

#absolute {
  position: relative;
}

#absolute #middle {
  background-color: red;
  position: absolute;
  top: 50px;
  left: 50px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/179333770-e875708d-39ff-4ef6-91d0-a2d87720c998.png" width="300">  
위의 코드처럼 #absolute 라는 <span class="crimson">조상 요소에서 position</span> 이 지정되어있다면 <span class="mediumblue">해당 조상 요소를 기준으로 이동</span>하게 된다.

### 🟡 fixed
fixed 로 지정되면 기본적으로 그 자리를 계속해서 유지한다. fixed 또한 <span class="forestgreen">일반적인 문서 흐름에서 제거</span>되고 <span class="mediumblue">공간도 차지하지 않으며 초기 컨테이닝 블록의 상대적 위치를 갖게 된다.  
<img src="https://user-images.githubusercontent.com/87808288/179335598-633d4905-2d2c-44de-8890-3957beb64d9c.png" width="300">
<img src="https://user-images.githubusercontent.com/87808288/179335632-e73b745e-d7a1-4490-876f-7a68c06f95b3.png" width="280">  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <h1>Position Property</h1>
  <section id="static">
    <h2>Static</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
  <section id="relative">
    <h2>relative</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
  <section id="absolute">
    <h2>absolute</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
  <section id="fixed">
    <h2>fixed</h2>
    <div></div>
    <div id="middle"></div>
    <div></div>
  </section>
</body>
```

```css
div {
  width: 100px;
  height: 100px;
  background-color: yellowgreen;
  border: 2px solid black;
  margin: 10px;
  display: inline-block;
}

#middle {
  background-color: aquamarine;
}

#relative #middle {
position: relative;
top: 100px;
}

#absolute {
  position: relative;
}

#absolute #middle {
  background-color: red;
  position: absolute;
  top: 50px;
  left: 50px;
}

#fixed #middle {
  position: fixed;
  background-color: blue;
  top: 0px;
  left: 0px;
}
```

<!-- ```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
</body>
``` -->

### (5) sticky
sticky는 fixed와 비슷하게 생겼는데  
스크롤을 시작할 때는 고정되지 않은 상태이지만  
개발자가 설정한 위치에 도달하면 그 위치에 머물게 된다.  

# 🔴 transition
`transition 속성`을 이용하면 <u>:hover일 때</u> 도형등이 바뀌는 것을 <span class="crimson">서서히 바뀌도록 설정</span>할 수 있다. transition을 사용하면 :hover일 때 빠르게 변하지만 transition을 사용하면 애니메이션처럼 움직임을 줄 수 있다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <h1>transiction</h1>
  <div class="circle"></div>
</body>
```

```css
.circle {
  width: 300px;
  height: 300px;
  background-color: magenta;
}

.circle:hover {
  background-color: cyan;
  border-radius: 50%;
  transition: 1s;
}
```

더 나아가 위의 코드는 :hover 일 때 -> 색상과 radius가 모두 1초 안에 서서히 바뀌지만  
아래의 코드처럼<span style="color:blue">transition을 추가로 더 설정</span>하여 <u>background-color 등 만 1초 동안 서서히 바뀌도록</u> 설정할 수 있다.  

```css
.circle {
  width: 300px;
  height: 300px;
  background-color: magenta;
  transition: background-color 3s;
}

.circle:hover {
  background-color: cyan;
  border-radius: 50%;
}
```

그리고 아래의 코드처럼 <span style="color:blue">transition 시작 시간을 지연시킬 수도</span> 있다.  

```css
.circle {
  width: 300px;
  height: 300px;
  background-color: magenta;
  transition: background-color 3s 1s;
}

.circle:hover {
  background-color: cyan;
  border-radius: 50%;
}
```

### (1) timing
&lt;div&gt;의 <u>움직임은 제각각</u>이지만 <span style="color:blue">끝나는 시점은 모두 동일</span>하다.  
왜냐하면 <span style="color:green">transition: margin-left 3s;</span>이 설정되어 있기 때문이다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <section>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </section>
</body>
```

```css
section div {
  height: 100px;
  width: 100px;
  background-color: turquoise;
  margin: 20px 0;
  transition: margin-left 3s;
}

section:hover div{
  margin-left: 500px;
}

div:nth-of-type(1) {
  transition-timing-function: ease-in;
}
div:nth-of-type(2) {
  transition-timing-function: ease-out;
}
div:nth-of-type(3) {
  transition-timing-function: cubic-bezier(0.7, 0, 0.84, 0);
}
div:nth-of-type(4) {
  transition-timing-function: cubic-bezier(0.85, 0, 0.15, 1);
}
```

ease-in을 보면 천천히 시작하지만 가속도가 붙고,  
ease-out은 빠르게 시작하지만 점점 속도가 느려진다.  

## 4. transform
transform으로는 사물을 회전시키거나 왜곡 등의 효과를 줄 수 있다.  


### (1) rotate
```css
section:first-of-type h1:nth-of-type(1) {
  transform-origin: bottom right;
  transform: rotate(45deg);
}
```

오른쪽 아래를 기준으로 45도 회전시킬 수 있다.  

### (2) scale
요소의 크기를 변화시킬 때 사용한다.  

```css
section:first-of-type h1:nth-of-type(2) {
  transform: scale(0.5);
}
```

위의 코드는 전체 크기가 절반으로 줄어들게 된다.  

```css
section:first-of-type h1:nth-of-type(2) {
  transform: scale(2, 1);
}
```

위의 코드는 높이는 동일하지만(1), 넓이는 두배가 된다.  

```css
section:first-of-type h1:nth-of-type(2) {
  transform: scaleY(2);
}
```

이렇게 scaleY로 표현하면 높이가 2배가 된다.  

### (3) translate
```css
section:first-of-type h1:nth-of-type(3) {
  transform: translateX(200px);
}
```

translateX를 사용하면 가로축 오른쪽으로 200px 이동시킬 수 있다.  

```css
section:first-of-type h1:nth-of-type(4) {
  transform: translateX(-200px);
}
```

translateX를 사용하고 그 값으로 음수가 들어가면 왼쪽으로 이동시킨다.  

### (4) skew
skew는 요소를 2차원 평면상에서 기울이는 기능이다.  

```css
section:nth-of-type(2) h1:nth-of-type(1) {
  transform: skew(30deg);
}
```

transform의 여러 속성을 한번에 표기할 수도 있는데  

```css
section:nth-of-type(2) h1:nth-of-type(2) {
  transform: rotate(20deg) scale(1.3);
}
```

## 5. background

## 6. google font

구글 폰트는 무료이다.  
google font로 이동하여 사용하고자 하는 글꼴을 클릭하여 이동하면 font-weight를 선택해야한다.  
그후에 임베딩하여 나오는 코드를 복사하여 html 코드에 붙여넣어준다.(head에 넣어준다.)  
그리고 CSS 코드도 수정한다.  

```css
body {
  font-family: Montserrat, sans-serif;
}

h1, h2, h3 {
  font-family: Roboto, sans-serif;
  font-weight: 100;
}
```


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
