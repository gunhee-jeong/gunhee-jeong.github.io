---
layout: single
title: "The Web Developer CSS -> 8장 CSS 박스 모델"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer CSS] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-08T20:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 8장 CSS 박스 모델
## 1. 가로와 세로
width & height
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="app.css">
</head>
<body>
    <div id="one">
      Nesciunt dolorum, reprehenderit ipsum, officiis quo laboriosam temporibus architecto repellendus amet sapiente dignissimos sunt laborum quisquam mollitia explicabo cum, perspiciatis saepe ullam voluptas quod aperiam ut harum? Quaerat, dolore et?
    </div>
    <div id="two">
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorum, quo! Praesentium veritatis nisi voluptatem. Quam quia rem incidunt labore unde. Fugit repudiandae odit error exercitationem hic ipsa ex tempora nesciunt!
    </div>
    <div id="three">
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorum, quo! Praesentium veritatis nisi voluptatem. Quam quia rem incidunt labore unde. Fugit repudiandae odit error exercitationem hic ipsa ex tempora nesciunt!
    </div>
</body>
</html>
```

```css
div {
  width: 300px;
  height: 300px;
}
```

width와 height 속성을 사용하여 &lt;div&gt;의 가로와 세로의 크기를 지정할 수 있고  
이렇게 지정한 박스의 크기는 content 박스이다.  

## 2. 테두리와 모서리
```css
div {
  width: 300px;
  height: 300px;
}

#one {
  background-color: aqua;
  border-style: solid;
  border-color: black;
  border-width: 5px;
  box-sizing: border-box;
}

#two {
  background-color: aquamarine;
  border: 4px solid black;
  /* border-radius: 10px; */
  border-radius: 10%;
}

#three {
  background-color: bisque;
}
```

<img src="https://user-images.githubusercontent.com/87808288/178088465-f79e0b85-67f9-4aee-8730-50c421b5477c.png" width="300">  

`#one`은 "<span style="color:red">box-sizing: border-box</span>"로 설정되어 있고  
#two는 box-sizing이 따로 설정되어있지 않다.  
그래서 위의 이미지를 보면 -> #one은 width와 height가 300px 인데,  
이 크기가 <span style="color:tomato">border의 테두리까지 포함된 300px로 설정</span>되어있고  
<u>#two는 box-sizing이 따로 설정되어있지 않기</u> 때문에  
<span style="color:royalblue">border width가 4px</span>로 설정됨에 따라 <span style="color:blue">width 300px + border 4px(양쪽은 8px)</span>  
<span style="color:tomato">총 width == 308px</span>로 설정되어 300px로 설정되었던 값이 변하게 되었다.  

## 3. padding(패딩)
패딩이란 content 박스와 border 사이의 공간을 padding이라고 표현한다.  
개발자 모드에서 "초록색"으로 표현되는 박스 공간이 padding이다.  

이렇게 padding은 텍스트의 크기는 그래도 두고, 요소 크기 자체를 기울 때 사용한다.  

padding에도 속기법이 적용된다.  

```html
<button>pad Me!</button>
```

```css
button {
  /* 사방에 padding이 10px 설정된다. */
  padding: 10px; 
  
  /* 5px은 vertical, 10px은 horizontal에 적용된다. */
  padding: 5px 10px;

  /* 왼쪽부터 top right bottom lefr */
  padding: 5px 1px 0 2px;
}
```

<u>vertical에는 padding을 주지 않고</u>, horizontal에만 padding을 주고 싶다면  
<span style="color:green">padding: 0 10px;</span> 이렇게 설정할 수도 있다.  

## 4. margin(여백)
&lt;button&gt;의 border 간의 간격을 margin이라고 표현한다.  

<u>여러 태그들에는 기본적으로 margin이</u> 들어가 있다.  
따라서 웹을 사용할 때는 기본적으로 여백을 0으로 만들고 시작한다.  

```css
body {
  margin: 0;
}
```

## 5. 디스플레이 속성
```html
<body>
  <h1>나는 h1!</h1>
  <h1>나도 h1!</h1>
  <span>나는 span이야</span>
  <span>나도 span이야</span>
</body>
```

```css
h1 {
  background-color: palegoldenrod;
  border: solid 1px black;
}

span {
  background-color: aqua;
  border: solid 1px black;
}
```

<img src="https://user-images.githubusercontent.com/87808288/178093131-957d9de1-8aba-4653-83b2-245819feced7.png" width="500">  
&lt;h1&gt;은 `block` 레벨을 가지기 때문에 <span style="color:royalblue">한 칸을 모두 차지</span>하고 <span style="color:red">공간을 공유하지 않는다</span>.  
&lt;span&gt;은 `inline` 블록이기 때문에 <span style="color:blue">content의 크기 만큼</span>을 차지하며 한 칸을 모두 채우지 않게 된다.  

```css
h1 {
  background-color: palegoldenrod;
  border: solid 1px black;
}

span {
  background-color: aqua;
  border: solid 1px black;
  width: 700px;
}
```

위의 CSS 코드에서 <u>&lt;span&gt; width를 700px로</u> 설정하여도 <span style="color:tomato">&lt;span&gt;의 width는 그대로</span>인 것을 확인할 수 있다.  
그 이유는 <span style="color:red">&lt;span&gt;이 inline 블록</span>이기 때문이다.  

이런 &lt;span&gt;도 padding 속성은 정상적으로 동작한다.  
하지만 세로로는 공간을 차지하지도 않고 내용을 밀어내지도 않는다.  

```css
h1 {
  background-color: palegoldenrod;
  border: solid 1px black;
}

span {
  background-color: aqua;
  border: solid 1px black;
  /* width: 700px; */
  padding: 50px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/178097147-f900c045-14bc-48f7-a9b7-207c0798a6b5.png" width="400">  

이 상테에서 background-color를 제거하면

```css
h1 {
  background-color: palegoldenrod;
  border: solid 1px black;
}

span {
  /* background-color: aqua; */
  border: solid 1px black;
  padding: 50px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/178097243-653ddd16-e31e-4e5e-b294-dab8e22b7004.png" width="400">  
겹치는 것들을 밀어내지 않는다는 것을 알 수 있다.  

```html
<body>
  <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos, quasi! Corporis nihil <span>aliquam</span>, doloremque cumque repellendus similique animi optio commodi quod consectetur excepturi delectus magnam? Eos illo maiores eligendi cum.
    Lorem, ipsum dolor sit amet consectetur adipisicing elit. Vel, fugiat. Totam facilis facere explicabo nemo aperiam labore aliquam tempore? Accusamus blanditiis provident harum ad, error quibusdam temporibus itaque minus neque!
  </p>
</body>
```

```css
span {
  /* background-color: aqua; */
  border: solid 1px black;
  padding: 30px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/178097750-4463ce1f-ccd0-4f19-8aa1-c9103f9866bb.png" width="500">  
이렇게 inline 디스플레이 속성을 가지는 <u>&lt;span&gt;에 padding</u>을 주게되면 <span style="color:royalblue">양옆으로는 50px씩 밀어낸</span> 것을 볼 수 있으나  
<span style="color:blue">세로의 공간은 달라지지 않았다</span>.  

```css
span {
  /* background-color: aqua; */
  border: solid 1px black;
  /* padding: 30px; */
  margin: 30px;
}
```

위의 CSS 코드와 같이 padding이 아닌 `margin`을 주면,  
<span style="color:tomato">span이 차지하는 줄</span>에서 <span style="color:blue">좌우의 margin을 차지</span>하게된다.  
다만 padding과 마찬가지로 margin에서도 <span style="color:red">세로 방향은 무시</span>된다.  
<img src="https://user-images.githubusercontent.com/87808288/178097919-481ecfc8-d3ed-4ce5-af02-541e922b0872.png" width="400">  

`block 디스플레이 속성`을 가지는 &lt;h2&gt;는 inline 속성에서는 적용되지 않던  
<span style="color:blue">width 속성이 적용</span>된다.  

```css
h2 {
  background-color: olivedrab;
  width: 300px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/178098565-f8ef8178-6c1f-4501-bb27-aef51976f1b3.png" width="400">  

그리고 inline 속성에서 적용되지 않던 <span style="color:blue">세로(height)도 적용</span>된다.  
<img src="https://user-images.githubusercontent.com/87808288/178098689-bd9d7dd9-5020-49a6-9b68-519dc3ea1bc5.png" width="400">  

이렇게 block 디스플레이 속성은 한줄의 공간 밖에 영향을 주지 않는 inline 디스플레이 속성과 다른점이 존재한다.  

## 6. CSS 단위
### (1) Absolute
#### []

### (2) Relative
#### [percentages]
`퍼센티지`는 <span style="color:tomato">부모의 특성에 상대적</span>이다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <h1>CSS Units</h1>
  <section>
    <div></div>
  </section>
</body>
```

```css
section {
  background-color: red;
  width: 800px;
  height: 800px;
}

div {
  background-color: blue;
  width: 50%;
  height: 50%;
}
```

CSS 코드의  <u>50% 라는 것의 의미</u>는 <span style="color:red">부모 요소(section) 너비의 50%</span>를 말한다.  
CSS 코드에서 div와 관련된 50%는 변화가 수정사항이 없더라도, <u>div의 부모인 section의 크기가 변한다면</u>  
<span style="color:blue">&lt;div&gt;의 크기는 상대적으로 변하는</span> 것이다.  

```css
section {
  background-color: red;
  width: 800px;
  height: 800px;
}

div {
  background-color: blue;
  width: 50%;
  height: 50%;
}

h1 {
  font-size: 40px;
  line-height: 200%;
}
```

위의 CSS 코드처럼 <span style="color:royalblue">&lt;h1&gt;</span>의 <u>fonts-size를 40px</u>로 지정하고  
그 바로 아래줄에 <u>line-height는 200%</u>로 percentage를 사용했다.  
이럴경우는 <span style="color:blue">line-height는 부모와는 상관이 없다</span>.  
<span style="color:tomato">같은 h1 태그의 font-size 크기의 200%를</span> 말하기 때문이다.  
이렇게 <u>percentage를 사용한다고해서</u> <span style="color:red">무조건 부모 태그에 상대적으로 사용되는 것은 아니다</span>.  

#### [em]
em은 rem과 같이 상대적 단위이며 다른 값에 영향을 받는다.  

<u>글꼴의 크기를 1em</u>으로 설정하면 <span style="color:blue">부모 요소와 똑같은 크기</span>가 된다.  
그러니깐 <span style="color:royalblue">2em</span>은 <u>부모 요소보다 2배 더 큰</u> 것이다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <h1>CSS Units</h1>

  <article>
    <h2>I am h2</h2>
    <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos, quasi! Corporis, doloremque cumque repellendus similiqueanimi optio commodi    quoconsectetur excepturi delectus magnam? Eos illo maiores eligendi cum.
    </p>
  </article>
  <section>
    <div></div>
  </section>
</body>
```

```css
section {
  background-color: red;
  width: 800px;
  height: 800px;
}

div {
  background-color: blue;
  width: 50%;
  height: 50%;
}

article {
  font-size: 30px;
}

h2 {
  font-size: 2em;
}

p {
  font-size: 1em;
}
```

<u>h2 태그의 부모 요소는 article</u>로,  
<u>&lt;article&gt;의 font-size는 30px</u>로 <span style="color:royalblue">h2의 font-size는 2em</span>이기때문에 <span style="color:blue">2배인 60px</span>이 된다.  
&lt;p&gt;도 article 태그가 부모이므로 30px의 font-size를 가지게 된다.  

```css
section {
  background-color: red;
  width: 800px;
  height: 800px;
}

div {
  background-color: blue;
  width: 50%;
  height: 50%;
}

article {
  font-size: 30px;
}

h2 {
  font-size: 2em;
  margin-left: 1em;
}

p {
  font-size: 1em;
}
```

`percentage`에서는 <u>width와 height 속성</u>일 경우에는 <span style="color:tomato">부모에 상대적으로 표현</span>되고  
<u>line-height 속성</u>일 경우에는 <span style="color:red">같은 태그 안의 font-size 크기에 상대적</span>이었다.  
`em`에서도 <u>&lt;article&gt; font-size는 30px</u>로 -> <span style="color:blue">&lt;h2&gt; font-size가 2em</span>이기 때문에 <span style="color:royalblue">2배인 60px</span>이 된다.  
그리고 <span style="color:tomato">추가적으로 margin-left</span>를 <u>1em</u>을 준다면, 여기서 1em은 <u>부모 요소가 아닌</u>  
같은 <span style="color:red">&lt;h2&gt;의 font-size가 60px</span>로 정해졌기 때문에 -> <span style="color:red">이것에 상대적인 1em</span>, 즉 <u>60px로 margin-left가</u> 설정된다.  

#### [rem]
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <h1>CSS Units</h1>

  <article>
    <h2>I am h2</h2>
    <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos, quasi! Corporis, doloremque cumque repellendus similiqueanimi optio commodi    quoconsectetur excepturi delectus magnam? Eos illo maiores eligendi cum.
    </p>
    <ul>
      <li>
        Pasta
        <ul>
          <li>
            Ravioli
            <ul>
              <li>Spinach Ricotta</li>
            </ul>
          </li>
        </ul>
      </li>
      <li>Salad</li>
      <li>Gelato</li>
    </ul>
  </article>
  <section>
    <div></div>
  </section>
</body>
```

```css
section {
  background-color: red;
  width: 800px;
  height: 800px;
}

div {
  background-color: blue;
  width: 50%;
  height: 50%;
}

article {
  font-size: 15px;
}

h2 {
  font-size: 2em;
  margin-left: 1em;
}

p {
  font-size: 1em;
}

ul {
  font-size: 1.5em;
}
```

<u>&lt;article&gt; 안에는 자식 관계로</u> <span style="color:royalblue">&lt;ul&gt;</span>가 들어있고 <span style="color:tomato">&lt;ul&gt;는 중첩</span>되어있다.  
그리고 위의 CSS 코드에서 볼 수 있듯이, <span style="color:royalblue">&lt;ul&gt;의 font-size는 1.5em</span>으로 설정되어있어서  
&lt;ul&gt;의 부모 태그인 article의 font-size가 15px이므로 -> <u>50% 더 커지게</u> 설정되었다.  
<img src="https://user-images.githubusercontent.com/87808288/178713067-bb79d888-c5c5-4585-a67b-ba22a2c7c699.png" width="400">  
그런데 위의 사진과 같이 em의 문제점이 들어나는데 -> &lt;ul&gt;가 &lt;article&gt; 안에 3번 중첩되어있으므로  
<span style="color:red">단계별로 누적</span>되어 <u>font-size가 커지게</u> 된 것이다.  
`em`의 <span style="color:tomato">글꼴 크기는 부모 항목의 글꼴 크기를 기반으로</span> 하기 때문이다.  

`rem`은 <u>글꼴의 크기를 부모 요소의 크기에 따라 바꾸지 않는다</u>.  
<span style="color:red">root HTML 요소의 글씨 크기에 따라 바꾼다</span>는 것이 다른점이다.  
즉, <span style="color:red">문서 전체에서 하나의 글꼴 크기에 비례하여 바뀐다</span>는 것이다.  

```html
<body>
  <h1>CSS Units</h1>

  <article id="rems">
    <h2>I am h2</h2>
    <h3>I am h3</h3>
    <button>Click Me</button>
    <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos, quasi! Corporis, doloremque cumque repellendus similiqueanimi optio commodi    quoconsectetur excepturi delectus magnam? Eos illo maiores eligendi cum.
    </p>
    <ul>
      <li>
        Pasta
        <ul>
          <li>
            Ravioli
            <ul>
              <li>Spinach Ricotta</li>
            </ul>
          </li>
        </ul>
      </li>
      <li>Salad</li>
      <li>Gelato</li>
    </ul>
  </article>
  <section>
    <div></div>
  </section>
</body>
```

```css
html {
  font-size: 10px;
}

#rems h2{
  font-size: 3rem;
}

#rems h3{
  font-size: 2rem;
}

#rems ul{
  font-size: 0.8rem;
}
```

그리고 루트 요소란 &lt;html lang="en"&gt; 바로 이것을 가리킨다.  
rem 단위를 사용하면 &lt;ul&gt;이 중첩되어 있다해도 누적되어서 font-size가 정해지지 않는다.  
루트 요소에 상대적으로 결정될 뿐이다.  

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
