---
layout: single
title: "The Web Developer CSS -> 11장 가격표 만들기 프로젝트"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer CSS] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-20T13:50:00+09:00
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

# 11장 가격표 만들기 프로젝트

## 1. web
<img src="https://user-images.githubusercontent.com/87808288/180206073-101a755d-2de0-4781-8902-fd18042960fc.png" width="100%">  

## 2. mobile
<img src="https://user-images.githubusercontent.com/87808288/180193822-ef6a72a7-7e3f-4daf-af78-5dec1140aa0c.png" width="50%">  

# 🔴 code
## 🟠 HTML code
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="app.css">
  <title>Document</title>
</head>

<body>
  <div class="panel">
    <div class="pricing-plan">
      <img src="icons/icon1.png" alt="" class="pricing-img">
      <h2 class="pricing-header">Personal</h2>
      <ul class="pricing-features">
        <li class="pricing-features-item">Custom domains</li>
        <li class="pricing-features-item">Sleeps after 30 mins of inactivity</li>
      </ul>
      <span class="pricing-price">Free</span>
      <a href="#/" class="pricing-button">Sign up</a>
    </div>

    <div class="pricing-plan">
      <img src="icons/icon2.png" alt="" class="pricing-img">
      <h2 class="pricing-header">Small team</h2>
      <ul class="pricing-features">
        <li class="pricing-features-item">Never sleeps</li>
        <li class="pricing-features-item">Multiple workers for more powerful apps</li>
      </ul>
      <span class="pricing-price">$150</span>
      <a href="#/" class="pricing-button is-featured">Free trial</a>
    </div>

    <div class="pricing-plan">
      <img src="icons/icon3.png" alt="" class="pricing-img">
      <h2 class="pricing-header">Enterprise</h2>
      <ul class="pricing-features">
        <li class="pricing-features-item">Dedicated</li>
        <li class="pricing-features-item">Simple horizontal scalability</li>
      </ul>
      <span class="pricing-price">$400</span>
      <a href="#/" class="pricing-button">Free trial</a>
    </div>
  </div>
</body>
```

`.pricing-plan`이라는 <span style="color:royalblue">&lt;div&gt;</span> 안의 element들로 <span style="color:blue">시맨틱</span>한 사용을 위해 <u>h2, ul, li, span, a 태그</u>들을 사용했다.  

그리고 .pricing-plan 안의 <u>버튼으로 사용한 &lt;a&gt;</u>는 <span style="color:royalblue">가운데 버튼</span>은 기본적으로 <span style="color:blue">불이 들어와있는 형태로</span> 만들기 위해  
<span style="color:royalblue">다른 a 태그</span>들의 className(<u>class="pricing"</u>)과는 다르게  
<span style="color:green">class="pricing-button is-featured"</span>으로 className을 만들었다.  

## 🟠 CSS code
### 🟡 reset css
```css
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}

article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}

body {
	line-height: 1;
}

ol, ul {
	list-style: none;
}

blockquote, q {
	quotes: none;
}

blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}

table {
	border-collapse: collapse;
	border-spacing: 0;
}

/* 코드 시작 */
html {
  box-sizing: border-box;
  font-family: 'Open Sans', sans-serif;
}

body {
  background-color: #60a9ff;
  display: flex;
  justify-content: center;
  align-items: center;
  /* body는 최소  */
  min-height: 100vh;
}

.panel {
  background-color: ivory;
  border-radius: 10px;
  padding: 15px 25px;
  width: 100%;
  /* .panel의 최대 width를 나타냄  0~930px*/
  max-width: 930px;
  display: flex;
  flex-direction: column;
  text-align: center;
  text-transform: uppercase;
}

.pricing-plan {
  border-bottom: 1px solid #e1f1ff;
}

/* 이 선택자 정리하기! */
.pricing-plan:last-child {
  border-bottom: none;
}

.pricing-img {
  margin-bottom: 25px;
  max-width: 100%;
}

.pricing-header {
  color:#888;
  font-weight: 600;
  letter-spacing: 1px;
}

.pricing-features {
  /* 위 좌우 아 */
  margin: 50px 0 25px;
  color: #016ff9;
}

.pricing-features-item {
  font-weight: 600;
  letter-spacing: 1px;
  font-size: 12px;
  line-height: 1.5;
  padding: 15px 0;
  border-top: 1px solid #e1f1ff;
}

.pricing-features-item:last-child {
  border-bottom: 1px solid #e1f1ff;
}

.pricing-price {
  color: #016ff9;
  /* span은 inline 속성이지만 block 속성으로 변경함 */
  display: block;
  font-size: 32px;
  font-size: 700;
}

/* 좌우 버튼 기본 설정 */
.pricing-button { 
  border: 1px solid #9dd1ff;
  border-radius: 10px;
  color: #348efe;
  /* block, inline, inline-block 차이 */
  display: inline-block;
  padding: 15px 35px;
  text-decoration: none;
  margin: 25px 0;
  /* 버튼 누르면 눌러짐 효과 블로그 정리하기 */
  transition: background-color 200ms ease-in-out;
}

.pricing-button:hover, .pricing-button:focus {
  background-color: #e1f1ff;
}

/* 가운데 버튼 기본 설정 */
.pricing-button.is-featured {
  background-color: #48aaff;
  color: white;
}

.pricing-button.is-featured:hover, .pricing-button.is-featured:focus{
  background-color: #269aff;
  color: white;
}

@media (min-width: 900px) {
  .panel {
    flex-direction: row;
  }
  .pricing-plan {
    border-bottom: none;
    border-right: 1px solid #e1f1ff;
    padding: 25px 50px;
  }
  .pricing-plan:last-child {
    border-right: none;
  }
}
```

### 🟡 html
```css
html {
  box-sizing: border-box;
  font-family: 'Open Sans', sans-serif;
}
```

reset css를 작성한 후  
기본적으로 <u>&lt;html&gt;</u>에는 <span style="color:red">box-sizing</span>: border-box; 속성을 추가한다.  

### 🟡 body
```css
body {
  background-color: #60a9ff;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}
```

<span class="mediumblue">body에 기본적인 height를 설정</span>하면 <span class="crimson">자식 element에서 높이를 상대적으로 줄 때 body를 기준으로 사용</span>할 수 있게 된다. 이때 &lt;body&gt;에 `min-height: 100vh;`를 주거나 `heigth: 100%;`를 주고 시작하게 된다.

### 🟡 .panel
```css
.panel {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 930px;
  padding: 15px 25px;
  background-color: ivory;
  border-radius: 10px;
  text-align: center;
  text-transform: uppercase;
}
```

<u>.pricing-plan을 모두 묶고 있는 &lt;div&gt;</u>인 `.panel`은 기본적으로 <u>mobile을 지원</u>하고자 flex-direction: <span style="color:royalblue">column</span>;이다.  
<span style="color:royalblue">width: 100%;</span>로 부모 element인 <u>&lt;body&gt;의 vh100의 100%를 사용</u>하게 된다.  

그런데 밑의 줄의 <span style="color:blue">max-width: 930px;</span>을 사용하면서 조금의 변화가 생긴다.  
.panel의 width가 <span style="color:tomato">최대 930px까지 밖에 늘어나지 않게</span> 설정한 것이다.  
화면의 변화에 맞게 0 ~ 930px까지 최대 width가 늘어나지 않게 된다.  

#### [.pricing-plan:last-child]
```css
.pricing-plan:last-child {
  border-bottom: none;
}
```

이 프로젝트에서는 <u>.pricing-plan에 속하는</u> <span style="color:royalblue">&lt;div&gt;가 총 3개</span> 존재한다.  
web 환경에서는 row로 존재하기 때문에 3개의 &lt;div&gt;의 border-bottom에 줄이 생겨야 하지만  
<u>mobile 환경에서 columne으로 존재</u>하기 때문에  
<span style="color:royalblue">가장 아래의 &lt;div&gt;에는 border가 없어야</span> 한다.  
따라서 <span style="color:tomato">마지막 &lt;div&gt;를 선택</span>하여 <span style="color:green">border-bottom: none;</span> 설정을 하게 된다.  

#### [.pricing-price]
```css
.pricing-price {
  display: block;
  color: #016ff9;
  font-size: 32px;
  font-size: 700;
}
```

<u>.pricing-price</u>은 <span style="color:blue">&lt;span&gt;</span>이다.  
그래서 기본적으로 display: <span style="color:tomato">inline 속성</span>을 가지고 있다.  

하지만 이 프로젝트에서 <u>가격에 해당하는 부분</u>은 <span style="color:tomato">한 줄을 모두 &lt;span&gt;가 차지해야</span>하므로  
<span style="color:red">display:block; 속성으로</span> 변경하게 되었다.  
<img src="https://user-images.githubusercontent.com/87808288/180224313-44753877-8808-4f81-9564-7c29ad43aba7.png" width="40%">
<img src="https://user-images.githubusercontent.com/87808288/180224352-811b0b73-7000-4ae1-856b-da01c8c8bf9e.png" width="35%">  

#### [.pricing-button]
```css
.pricing-button { 
  display: inline-block;
  margin: 25px 0;
  padding: 15px 35px;
  border: 1px solid #9dd1ff;
  border-radius: 10px;
  color: #348efe;
  text-decoration: none;
  transition: background-color 200ms ease-in-out;
}
```

<img src="https://user-images.githubusercontent.com/87808288/180244633-aea51fb8-c5e4-4e22-91fc-f2f88d6605c3.png" width="100%">  

<img src="https://user-images.githubusercontent.com/87808288/180244692-c1b1e819-2000-41e2-8611-f172854878f5.png" width="100%">  
<u>a 태그</u>는 기본적으로 display: <span style="color:royalblue">inline; 속성</span>을 가지기 때문에 <u>상하에만 padding</u>이 들어가고  
width와 height 등의 속성을 추가할 수 없다.  
따라서 <u>padding이 가능</u>하고 <span style="color:tomato">width와 height가 가능</span>한 display: <span style="color:red">inline-block; 속성</span>으로 변경한다.  


<!-- ① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨-->

<!-- ### 2. Link 넣기

```

유형 1: (설명어를 입력) : [gunhee's coding blog](https://gunhee-jeong.github.io/)
유형 2: (URL 자동연결) : <https://gunhee-jeong.github.io/>
유형 3: (동일 파일 내 '문단으로 이동') : [1. Header로 이동](###-1-header)

```

```bash
.next/static
        ├── AbmKMg9BFeVUuJ7lsQ1w8
        ├── chunks                 // 여러 페이지에서 공통으로 사용되는 번들 파일
        │       └──  pages         // 각 페이지의 번들 파일
        ├── runtime                // 웹팩과 next의 런타임과 관련된 번들 파일
        ├── css                    // 애플리케이션의 모든 페이지에 대한 글로벌 CSS 파일
        └── media                  // 정적으로 가져온 이미지 next/image가 여기에 해시 및 복사
```

<details>
<summary class="black">코드</summary>
<div markdown="1">

```jsx
// helloWorld!
const hello = 'hi';
```
</div>
</details>

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
