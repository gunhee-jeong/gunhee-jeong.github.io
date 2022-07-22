---
layout: single
title: "The Web Developer CSS -> 7장 CSS 선택자"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer CSS] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-04T08:20:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 7장 CSS 선택자
## 1. 전체 요소 선택자
### (1) *
```css
* {

}
```

## 2. selector list
```css
h1, h2 {
  color: magenta;
}
```

태그들을 ,을 사용하여 선택할 수 있다.  

## 3. ID 선택자
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <button>Log In</button>
  <button id="signBtn">Sign Up</button>
</body>
```

```css
#signupBtn {
  background-color: red;
}
```

`id`는 <u>중복될 수 없고</u> <span style="color:blue">고유한 식별자</span>로 사용해야한다.  
또한 id 선택자는 남용하지않는 것이 좋다.  
충분히 다른 선택자들을 사용하여 표현할 수 있으므로, id 선택자를 사용하여 CSS를 남용하는 것은 지양해야한다.  

## 4. class 선택자
```html
<body>
  <h2>I am h2</h2>
  <h2>I am h2</h2>
  <h2>I am h2</h2>

  <button>Button1</button>
  <button id="signupBtn">Button2</button>

  <p>
    Lorem ipsum <span class="tag">dolor</span> sit, amet consectetur adipisicing elit. Distinctio quasi ad, labore molestias similique aliquid repudiandae sed. Illo vitae repellat, laudantium nostrum, reprehenderit quas earum explicabo ex nulla, eos voluptatum?
    Dolorum laudantium sequi alias inventore repellat similique aliquam, voluptate atque incidunt ad, fugit, eligendi odit beatae laboriosam eveniet aliquid perferendis qui. Rem quam aliquid minima ex voluptatibus dolore, vitae neque?
    Optio adipisci, delectus reprehenderit rerum culpa voluptatibus voluptas temporibus fugit ipsa sunt maxime repellat cupiditate aliquid harum voluptates accusamus eveniet tempora exercitationem nostrum iusto. Unde perferendis perspiciatis molestiae eveniet distinctio!
  </p>

  <h1>Hello World</h1>
  <p>Lorem ipsum <span class="tag">dolor</span> sit, amet consectetur adipisicing elit. Officiis illo, nostrum voluptatum sequi magnam quaerat dolorem nam, quam vel optio similique nemo quisquam nesciunt, magni dolor quo sapiente. Atque, nobis.</p>
  <p>Lorem ipsum <span class="tag">dolor</span> sit amet consectetur adipisicing elit. Culpa expedita officiis eius libero aliquid blanditiis sequi maxime recusandae, nemo dignissimos, vitae esse perferendis. Doloribus ratione quod at sunt voluptates pariatur!
  Consequuntur quaerat perspiciatis earum? Vitae atque tempore dolor ad magni temporibus error sed quisquam blanditiis. In quos nihil quibusdam non explicabo. Atque autem est voluptas pariatur veritatis facilis dignissimos nobis.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ab id velit ipsa aut quisquam quam quaerat, reiciendis autem modi neque laudantium molestias distinctio minus, eveniet atque quas facere quae vero.
  Deserunt autem nisi iste quaerat dolore, veritatis quisquam molestias sit eveniet? Quaerat perspiciatis distinctio, illum quo minus amet ad vero repudiandae fugit, voluptatem dolorem optio error nihil neque hic qui.</p>
</body>
```

```css
.tag {
  background-color: blue;
}
```

## 5. 자손 선택자
```css
.tag span {
  background-color: blue;
}
```

## 6. 인접 선택자와 직계 자손 선택자
### (1) 인접 선택자
'+'는 인접 선택자를 사용하는 기호이다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <nav>
    <label for="search">Search</label>
    <input type="text" placeholder="search" id="search">
    <button id="signup">Sign up</button>
  </nav>
  <section class="post">
    <span>Posted by <a href="#345adas">/u/gooner4lyfe</a></span>
    <h2>Happy birthday to the strongest defender/bodyguard in the</h2>
    <button>+Vote</button>
  </section>
</body>
```

```css
input + button {
  background-color: pink;
}
```

위의 `input + button`를 사용하면 <u>input의 형제 태그</u>인 <span style="color:blue">button의 색상만 변경</span>된다.  
아래의 CSS 코드로는, 코드에 있는 모든 &lt;h2&gt;의 형제인 &lt;button&gt;의 색상과 폰트 크기가 변경된다.  

```css
h2 + button {
  font-size: 20px;
  background-color: magenta;
}
```

### (2) 직계 자손 선택자
아래의 html을 살펴보면 <u>&lt;nav&gt; 안에는 &lt;li&gt;가 존재</u>하고 <span style="color:royalblue">그 안에 각각 &lt;a&gt;가 존재</span>한다.  
그런데 여기서 <u>&lt;nav&gt;와 형제 관계인 가장 아래의 &lt;a&gt;만 선택하고 싶다면</u> '<span style="color:tomato">></span>' 즉, <span style="color:red">직계 자손 선택자</span>를 사용하면 된다.  

```html
<footer>
  <nav>
    <ul>
      <li>
        <a herf="#home">Home</a>
      </li>
      <li>
        <a herf="#about">About</a>
      </li>
      <li>
        <a herf="#contact">Contact</a>
      </li>
      <li>
        <a herf="#puppies">Puppies</a>
      </li>
    </ul>
  </nav>
  <a href="#license">hello hello</a>
</footer>
```

```css
footer > a {
  color: red;
}
```

## 7. 속성 선택자
아래의 html에는 2개의 &lt;input&gt;가 존재한다.  
그중에서도 type속성이 password인 &lt;input&gt;만을 선택하고자 한다.  
이럴 경우 속성 선택자를 사용할 수 있다.  

```html
<body>
  <nav>
    <label for="search">Search</label>
    <input type="text" placeholder="search" id="search">
    <input type="password" placeholder="password">
    <button id="signup">Sign up</button>
  </nav>
</body>
```

```css
input[password] {
  color: yellow;
}
```

아래의 html에서는 &lt;ul&gt; 안에 4개의 &lt;a&gt;가 존재한다.  
그중에서 가장 마지막에 content로 "google"을 포함하고 있는 &lt;a&gt;만 선택하고자 한다.  

```html
<footer>
  <nav>
    <ul>
      <li>
        <a herf="#home">Home</a>
      </li>
      <li>
        <a herf="#about">About</a>
      </li>
      <li>
        <a herf="#contact">Contact</a>
      </li>
      <li>
        <a herf="google.com">Google</a>
      </li>
    </ul>
  </nav>
  <a href="#license">hello hello</a>
</footer>
```

```css
a[href*="google"] {
  color:magenta;
}

a[href$="google"] {
  color:magenta;
}
```

위 CSS 코드에서 "*="는 &lt;a&gt; 안의 어디든을 의미하고,  
"$="는 ".org"로 끝나는 것들을 검색하게 된다.  

## 8. 유사 클래스(가상 선택자)
### (1) hover
`hover`는 커서를 해당 태그 위에 두었을 경우를 잡아낼 수 있는 유사 클래스이다.  

```css
button:hover {
  background-color: red;
  color:white;
}
```

### (2) active
아래의 코드에는 "hover"와 "active"가 설정되어 있다.  
커서를 버튼 위에 두면 -> hover로 설정한 css가 작동하고  
커서로 버튼을 클릭하면 -> active로 설정한 css가 동작한다.  

```css
button:hover {
  background-color: red;
  color:white;
}

button:active {
  backgroun-color: green;
}
```

### (3) nth-of-type()
```html
<main>
  <h1>Popular Posts</h1>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
</main>
```

```css
.post:nth-of-type(3){
  background-color: blue;
}
```

위의 css 코드는 3번째 .post의 색상만을 blue로 설정해준다.  
그러나 매 3번 째마다로 이를 설정하고 싶다면 아래의 코드처럼 'n'을 추가해주면 된다.  

```css
.post:nth-of-type(3n){
  background-color: blue;
}
```

## 9. 가상 선택자 Pseudo class
### (1) last-child
`last-child`는 <u>형제 요소 그룹 중</u> <span style="color:tomato">마지막 요소</span>를 선택한다.  

web 버전에서는 문제가 되지 않다가  
mobile 환경에서는 column으로 변경되면서 <u>가장 마지막 element</u>이 <span style="color:royalblue">border를 제거</span>할 때 자주 사용된다.  

## 10. 가상 요소 Pseudo Elements
### (1) ::first-letter
&lt;section&gt; 안에 모든 &lt;h2&gt; 안의 요소 중 첫 글자를 선택하고자 한다.  

```html
<main>
  <h1>Popular Posts</h1>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
  <section class="post">
    <span>Posted by <a href="#213adas">/u/not_funny</a></span>
    <h2>Lol Look at this gagaga <span class="tag">funny</span></h2>
    <button>+Vote</button>
    <hr>
  </section>
</main>
```

```css
h2::first-letter {
  font-size: 40px;
}
```

### (2) ::first-line
::first-line은 해당 태그의 한 줄 라인을 선택하게 해준다.  

```html
<p>
Lorem ipsum dolor sit amet consectetur adipisicing elit. Necessitatibus ipsa corporis nemo quibusdam eveniet tempora totam doloribus beatae expedita dignissimos unde iure, neque libero, eos, iusto saepe nisi labore impedit.
Saepe, cupiditate aspernatur ipsa facere quidem dicta, a laboriosam culpa expedita enim error explicabo, vitae nemo asperiores. Quae earum saepe eum repudiandae. Obcaecati facere delectus illo quo eligendi cum sit.
Nam, voluptates sint veritatis, sed laboriosam nobis est id aperiam maiores omnis explicabo delectus quis suscipit eius. Recusandae nihil qui sapiente unde esse modi maxime, amet reiciendis in! Velit, tenetur.
Ipsa deleniti hic expedita excepturi blanditiis maiores totam fugiat nisi perferendis? Fuga eum voluptate adipisci dolorem, facilis accusantium laboriosam sunt, amet repellat numquam necessitatibus veniam ut quae quasi, suscipit ab?
Dolor fugiat doloremque aliquam nostrum esse commodi, maxime provident dicta? Amet illo magnam, vel ab impedit ullam consequatur eos veniam rem enim dignissimos incidunt iure dolore totam, ex voluptatum sapiente.
Doloremque necessitatibus rem libero animi ducimus consequuntur harum pariatur corporis placeat error impedit qui nam eligendi veniam cum, nobis dolore, eaque eum beatae similique porro earum. Minus quas at debitis.
Delectus, pariatur quod aliquam, sunt explicabo ullam maiores inventore reiciendis reprehenderit ea ipsum nobis accusantium soluta vitae fugit dicta voluptatem. Commodi, suscipit reprehenderit. Aliquam nesciunt laborum maiores qui, quisquam deleniti.
Cupiditate aperiam veritatis earum quasi sint dolorum perspiciatis repudiandae. Nesciunt, culpa libero! Accusantium, repellendus fugiat non nemo deserunt quisquam ipsum saepe distinctio error laboriosam architecto autem qui tempora, eius dolores?
Numquam possimus minus eveniet perferendis reprehenderit quas impedit. Velit ducimus odit, dicta dolores unde ut pariatur dolorum, ea totam voluptas voluptate minus. Quam expedita esse, quisquam optio asperiores delectus minima.
Veritatis fugiat, nihil minus delectus aliquam repellendus ipsum vitae excepturi quis totam et in tempore voluptatibus quos exercitationem sint! Minima et vitae accusamus eaque quod explicabo nam dolorum eligendi animi.
</p>
```

```css
p::first-line {
  color:red;
}
```

### (3) ::selection
selection을 사용하면 선택한 태그의 content 마다, 사용자가 설정한 css로 바꾸어준다.  

```html
<p>
Lorem ipsum dolor sit amet consectetur adipisicing elit. Necessitatibus ipsa corporis nemo quibusdam eveniet tempora totam doloribus beatae expedita dignissimos unde iure, neque libero, eos, iusto saepe nisi labore impedit.
Saepe, cupiditate aspernatur ipsa facere quidem dicta, a laboriosam culpa expedita enim error explicabo, vitae nemo asperiores. Quae earum saepe eum repudiandae. Obcaecati facere delectus illo quo eligendi cum sit.
Nam, voluptates sint veritatis, sed laboriosam nobis est id aperiam maiores omnis explicabo delectus quis suscipit eius. Recusandae nihil qui sapiente unde esse modi maxime, amet reiciendis in! Velit, tenetur.
Ipsa deleniti hic expedita excepturi blanditiis maiores totam fugiat nisi perferendis? Fuga eum voluptate adipisci dolorem, facilis accusantium laboriosam sunt, amet repellat numquam necessitatibus veniam ut quae quasi, suscipit ab?
Dolor fugiat doloremque aliquam nostrum esse commodi, maxime provident dicta? Amet illo magnam, vel ab impedit ullam consequatur eos veniam rem enim dignissimos incidunt iure dolore totam, ex voluptatum sapiente.
Doloremque necessitatibus rem libero animi ducimus consequuntur harum pariatur corporis placeat error impedit qui nam eligendi veniam cum, nobis dolore, eaque eum beatae similique porro earum. Minus quas at debitis.
Delectus, pariatur quod aliquam, sunt explicabo ullam maiores inventore reiciendis reprehenderit ea ipsum nobis accusantium soluta vitae fugit dicta voluptatem. Commodi, suscipit reprehenderit. Aliquam nesciunt laborum maiores qui, quisquam deleniti.
Cupiditate aperiam veritatis earum quasi sint dolorum perspiciatis repudiandae. Nesciunt, culpa libero! Accusantium, repellendus fugiat non nemo deserunt quisquam ipsum saepe distinctio error laboriosam architecto autem qui tempora, eius dolores?
Numquam possimus minus eveniet perferendis reprehenderit quas impedit. Velit ducimus odit, dicta dolores unde ut pariatur dolorum, ea totam voluptas voluptate minus. Quam expedita esse, quisquam optio asperiores delectus minima.
Veritatis fugiat, nihil minus delectus aliquam repellendus ipsum vitae excepturi quis totam et in tempore voluptatibus quos exercitationem sint! Minima et vitae accusamus eaque quod explicabo nam dolorum eligendi animi.
</p>
```

```css
p::selection {
  background-color: orange;
}
```

## 11. 우선순위 CSS
주어진 선택자가 구체적일수록 그 우선순위가 높아지게 된다.  
기본적으로 id 선택자(#)가 그 우선순위에 있어서 100점으로 가장 높고
그 이후는 class 선택자(*)이다.  
- ID
- Classes, attributes and pseudo-classes
- Elements and pseudo-elements

## 12. 인라인 스타일과 중요도
인라인 스타일 방식의 CSS는 id 선택자보다도 우선순위가 높다.  
따라서 인라인 스타일 방식의 CSS를 사용하는 것은 바람직하지 못하다.  

## 13. 상속 CSS
CSS 상속이란 구체적인 특성을 지정하지 않은 하위 요소에 상위 항목 특성이 적용되는 것을 말한다.  


<!-- <span style="color:royalblue"> -->

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
