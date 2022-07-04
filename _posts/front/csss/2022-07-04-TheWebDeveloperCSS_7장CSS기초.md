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

위의 input + button를 사용하면 input의 형제 태그인 button의 색상만 변경된다.  

아래의 CSS 코드로는, 코드에 있는 모든 &lt;h2&gt;의 형제인 &lt;button&gt;의 색상과 폰트 크기가 변경된다.  

```css
h2 + button {
  font-size: 20px;
  background-color: magenta;
}
```


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
