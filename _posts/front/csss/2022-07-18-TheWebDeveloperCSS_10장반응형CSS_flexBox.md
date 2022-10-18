---
layout: single
title: "The Web Developer CSS -> 10장 반응형 CSS 및 Flexbox"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer CSS] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-18T13:30:00+09:00
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

# 10장 반응형 CSS 및 Flexbox
## 1. flex-direction
flex model에는 "Main Axis"와 "Cross Axis"가 존재한다.  

`flex-direction`은 컨테이너 안에서 <span style="color:tomato">main axis</span>의 <span style="color:red">방향</span>을 결정하는 속성이다.  
<img src="https://user-images.githubusercontent.com/87808288/179451036-4a3229b3-9ff7-4161-bddc-ba59b7976d5d.png" width="600">  

## 2. justify content
`justify content`는 <span style="color:tomato">main axis</span>의 <span style="color:red">정렬 방법</span>을 결정하는 속성이다.   
<img src="https://user-images.githubusercontent.com/87808288/179453269-a33cd00f-7260-47dc-b701-83c423fed018.png" width="400">  

### (1) space-between
<u>space-between</u>은 <span style="color:tomato">바깥쪽의 여백을 없애고</span> <span style="color:blue">요소 사이에만 여백</span>을 만든다.  

### (2) space-around
space-around를 사용하면 <u>&lt;div&gt;의 양쪽 끝에 절반씩 여백</u>이 생긴다.  
따라서 <span style="color:blue">전체가 균등하지 않게</span> 된다.  
끝쪽의 <u>&lt;div&gt;의 여백이 5px</u>이라면 <span style="color:tomato">두 &lt;div&gt;가 만나는 곳의 여백은 5px + 5px</span>이므로 균등하게 나누어지지 않게 된다.  

### (3) space-evenly
space-around와 비슷해보이지만 <u>차이점이 있다</u>.  
space-around는 element의 한쪽 마다 여백이 생겨 요소와 요소 사이의 공간은 양 끝의 2배의 공간이 생긴다.  
하지만 `space-evenly`는 <u>요소와 요소 사이</u> 그리고 <u>양 끝의 여백</u>이 <span style="color:tomato">모두 같다</span>.  

## 3. flex wrap
main-axis가 `수평`일 때는 <span style="color:tomato">새로운 행을 만들어 요소를 정렬</span>하고  
main-axis가 `수직`일 때는 <span style="color:tomato">새로운 열을 만들어 요소를 정렬</span>하는 속성이다.  
<img src="https://user-images.githubusercontent.com/87808288/179458492-798d46e8-d2e8-4d37-b2cb-28053e095b7f.png" width="550">  

### (1) wrap-reverse
<u>cross axis의 방향</u>이 <span style="color:blue">위에서 아래</span>로 였다면 -> <span style="color:tomato">아래에서 위로</span> 바꾸게 된다.  

## 4. align-items
`align-items`는 <span style="color:red">cross axis의 방향</span>과 <span style="color:tomato">아이템을 정렬</span>하게 된다.  
<img src="https://user-images.githubusercontent.com/87808288/179459849-4f982e6f-acde-462d-9a7e-2bdbffa53733.png" width="750">  

### (1) flex-end
<u>align-items</u>에서 `flex-end`는 <span style="color:royalblue">cross axis의 방향</span>을 <span style="color:blue">위에서 아래로</span>에서 -> <span style="color:blue">아래에서 위로</span> 바꾸게 된다.  

### (2) baseline
align-items를 `baseline`으로 설정하면 <span style="color:tomato">텍스트의 기준선에 맞춰 정렬</span>하게 된다.  
각 <span style="color:blue">element의 글자를 잇는 밑줄</span>을 긋는다고 할 수 있다.  

## 5. align content
<img src="https://user-images.githubusercontent.com/87808288/179644916-e233776a-d0d6-4149-bc7b-9cb2ffaaa1d0.png" width="700">  
<u>행이나 열이</u> <span style="color:tomato">여러 개</span>일 때 <span style="color:blue">cross axis를 기준으로 정렬</span>한다.  
align content는 여러 행, 여러 열이 있을 때에만 사용하는 정렬 방법이다.  
즉 wrap이나 wrap-reverse가 적용되어있는 경우에 사용할 수 있다.  

<u>main axis가 수직</u>으로 되어있을 때 `align-content`는 <span style="color:tomato">열 사이의 공간을 조정</span>하게 된다.  
반대로 <u>수평을 주축으로 한다면</u> cross axis는 수직이므로 `aling-content`는 <span style="color:tomato">행 사이의 공간을 조정</span>한다.  

## 6. align self
align-self는 align-items와 비슷하지만  
<span style="color:blue">단일 요소에 사용</span>하거나 플렉스 컨테이너에서 두 개 요소에 개별로 사용한다.  

cross-axis를 기준으로 배열된 단일 요소의 위치를 바꿀 수 있다.  
flex container에서 한 element만 옮길 때 이 방법을 사용할 수 있다.  

```css
div:nth-of-type(3) {
  align-self: flex-end;
}
```

### (1) stretch
### (2) center
### (3) start
### (4) end

## 7. flex sizing
### (1) flex-basis
요소가 한 줄로 늘어서 있을 때 flex-basis가 너비의 기준이 된다.  
flex-basis는 main axis인 가로에 걸쳐있기 때문이다.  
flex-basis는 요소가 배치될 때의 최초 크기이다.  
main axis의 방향에 따라 width이기도 하고 height이기도 하다.  

<img src="https://user-images.githubusercontent.com/87808288/179656704-043c3a49-6b9d-457a-a666-234a6a103faa.png" width="500">  

```css
item1 {
  background: #ef9a9a;
  flex-basis: 60%;
}

item2 {
  background: #ce93d8;
  flex-basis: 30%;
}

item3 {
  background: #90caf9;
  flex-basis: 10%;
}
```

### (2) flex-grow
`flex-grow`는 <span style="color:blue">공간이 남아 있을 때</span>, 요소가 <span style="color:tomato">그 공간을 얼마나 차지할지</span> 정하게 된다.  
flex-grow와 flex-shrink는 단위가 없다.  

<img src="https://user-images.githubusercontent.com/87808288/179657635-d4fa7489-0b00-4d53-ba29-b81099315e4c.png" width="600">  

```css
#container {
  background-color: #003049;
  width: 90%;
  height: 500px;
  margin: 0 auto;
  border: 5px solid #003049;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

#container div {
  width: 100px;
  height: 100px;
}
```

<img src="https://user-images.githubusercontent.com/87808288/179657864-5f151300-ad2f-4871-ad06-05662074e29b.png" width="600">  

```css
#container {
  background-color: #003049;
  width: 90%;
  height: 500px;
  margin: 0 auto;
  border: 5px solid #003049;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

#container div {
  width: 100px;
  height: 100px;
}

#container div:nth-of-type(1) {
  flex-grow: 1;
}
```

위의 이미지와 같이 div:nth-of-type(1)을 사용하여 flex-grow를 사용하면  
첫 번째 &lt;div&gt;의 크기를 늘려 화면을 꽉 채울 수 있게 된다.  

<img src="https://user-images.githubusercontent.com/87808288/179658206-c44f25fb-f568-4618-b8cc-8997bde935e4.png" width="600">  

```css
#container {
  background-color: #003049;
  width: 90%;
  height: 500px;
  margin: 0 auto;
  border: 5px solid #003049;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

#container div {
  width: 100px;
  height: 100px;
  flex-grow: 1;
}
```

<u>모든 &lt;div&gt;에게 flex-grow를 1</u>을 설정하면 공간을 <span style="color:tomato">균등하게 차지하게</span> 된다.  
창을 줄이더라도 <u>비율은 유지된다</u>.  

하지만 이렇게 무한정으로 늘어나는 것도 좋은 것은 아니다.  
그래서 <span style="color:red">최대 넓이</span>와 <span style="color:red">최소 넓이</span>를 설정할 수 있다.  

```css
#container {
  background-color: #003049;
  width: 90%;
  height: 500px;
  margin: 0 auto;
  border: 5px solid #003049;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

#container div {
  width: 100px;
  height: 100px;
  max-width: 200px;
  min-width: 100px;
  flex-grow: 1;
}
```

<img src="https://user-images.githubusercontent.com/87808288/179659259-21cd3b85-7813-4074-8112-859865cdea6e.png" width="500">  

```css
#container {
  background-color: #003049;
  width: 90%;
  height: 500px;
  margin: 0 auto;
  border: 5px solid #003049;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

#container div {
  width: 100px;
  height: 100px;
}

#container div:nth-of-type(1) {
  flex-grow: 1;
}

#container div:nth-of-type(5) {
  flex-grow: 2;
}
```

flex-grow는 다른 element에 여러 숫자를 부여할 수 있다.  
첫 번째 div에는 1을 부여하고 두 번째 div에는 2를 부여하면  
위의 이미지와 같이 1 : 2의 비율로 나타내지는 것을 볼 수 있다.  

### (3) flex-shrink
flex-shrink의 값이 크다면, 화면이 줄어들 때 더 빠른 속도로 크기가 줄어들게 된다.  

## 8. flex shorthand
flex라는 속기법이 있다.  
flex는 위의 3가지 방법을 한 번에 표기하는 방법이다.  

```css
main .sidebar {
  background-color: purple;
  /* flex-grow, shrink, basis */
  flex: 1 2 300px;
  border: 2px solid white;
}
```

# 🔴 midea queries
midea queries를 사용하다보면 `view port`라는 것을 알아야한다. view port는 컴퓨터 그래픽에 있는 polygonal 영역을 말한다. 이는 브라우저에서 <span class="crimson">우리가 보고 있는 문서</span>나 윈도우 화면을 통해서 보고 있는 문서를 말한다. 즉 <u>화면 전체를 말하는 것이 아니라</u> <span class="mediumblue">브라우저의 width</span>를 말한다는 것이다.

```css
@media (min-width: 800px) {
  h1 {
    color:purple;
  }
}
```

위의 코드에서 media queries는 width가 800px 이상이면 &lt;h1&gt;의 color를 보라색으로 바꾸도록 설정했다.  

```css
@media (min-width: 600px) and (max-width: 800px) {
  h1 {
    color:purple;
  }
}
```

위의 CSS 코드는 600px 이상이고 800px 이하일 때 &lt;h1&gt;의 color를 보라색으로 바꾸게 된다.  

```css
@media (max-width: 500px) {
  h1 {
    color:red;
  }
}

@media (max-width: 1000px) {
  h1 {
    color:orange;
  }
}
```

위의 코드를 저장하고 실행해보면 <u>브라우저가 300px일 때도 color는 orange</u>이다. 왜냐하면 media queries의 <span class="mediumblue">조건문의 순서</span>에서 max-width가 1000px이기 때문이다.

```css
@media (max-width: 1000px) {
  h1 {
    color:orange;
  }
}

@media (max-width: 500px) {
  h1 {
    color:red;
  }
}
```

위의 코드와 같이 max-width: 500px이 코드의 가장 아래에 있으면 화면의 width가 최대 500px까지는 red color이고 500px이 넘고 1000px 이하에서는 orange color로 나온다.

이렇게 CSS 코드를 <u>역방향으로 사용하지 않기 위해</u>서는 아래의 코드와 같이 <span class="mediumblue">min-width</span>를 사용할 수 있다.

```css
h1 {
  color:red;
}

@media (min-width: 500px) {
  h1 {
    color:orange;
  }
}

@media (min-width: 1000px) {
  h1 {
    color:yellow;
  }
}

@media (min-width: 1500px) {
  h1 {
    color:green;
  }
}
```

아래의 코드와 같이 orientation을 설정하여 가로 모드를 지원할 수도 있다.  

```css
@media(orientation: landscape) {
  body {
    background-color: magenta;
  }
}
```

## 10. 반응형 내비게이션 바 만들기
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>flex-basis, grow, shrink</title>
  <link rel="stylesheet" href="app.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@600&display=swap" rel="stylesheet">
</head>

<body>
  <nav>
    <a href="#home">Home</a>
    <ul>
      <li>
        <a href="#Home">Learn More</a>
      </li>
      <li>
        <a href="#Home">About</a>
      </li>
      <li>
        <a href="#Home">Contact</a>
      </li>
    </ul>
    <a href="#signup">Sign Up</a>
  </nav>
  <h1>Media Queries</h1>
</body>
```

```css
body {
  font-family: 'Open Sans', sans-serif;
}

h1 {
  font-size: 6em;
  text-align: center;
}

nav {
  font-size: 1.5em;
  display: flex;
  justify-content: space-between;
}

ul, li {
  display: inline;
  margin: 0;
  padding: 0;
}

ul {
  border: 1px solid black;
  flex: 1;
  max-width: 50%;
  display: flex;
  justify-content: space-evenly;
}
```

CSS 코드의 <span style="color:green">ul {}</span>에서 <span style="color:green">flex: 1</span>을 사용하면 -> flex-grow를 1로 사용한다는 것이다.  
`grow`는 <span style="color:tomato">공간이 남아 있을 때</span>, 요소가 <u>그 공간을 얼마나 차지할지 정하게</u> 된다.  
그렇게 ul 태그는 남은 공간을 다 사용하게 되고, 아래의 이미지와 같이 보이게 된다.  
<img src="https://user-images.githubusercontent.com/87808288/179898245-25fa0fd4-6ab1-4aaa-8311-c0da2f6a5cd9.png" width="100%">  
<span style="color:green">max-width: 50%</span>를 지정하면 <span style="color:blue">ul 태그는 1의 공간에서 50%를 차지</span>하여 아래의 이미지와 같이 공간을 할당하게 된다.  
<img src="https://user-images.githubusercontent.com/87808288/179897542-15c04940-f5bf-414c-9327-1ca03e28f064.png" width="100%">  

```css
@media(max-width: 768px) {
  h1 {
    color: red;
    font-size: 4em;
  }
  
  nav, nav ul {
    flex-direction: column;
    align-items: center;
  }
} *
```

그리고 위의 CSS 코드를 추가하면  
브라우저가 <u>0px에서 max-width가 768px</u> 까지는 <span style="color:green">color:red</span>,  
&lt;nav&gt;와 &lt;ul&gt;는 flex-direction이 column과 align-items: center로 설정한다.  
<img src="https://user-images.githubusercontent.com/87808288/179899152-feefe6a4-bb52-4b82-878b-832c4b195f1d.png" width="50%">  

위의 CSS 코드가 아닌 아래의 CSS 코드를 사용하면

```css
@media(max-width: 768px) {
  body {
    width: 768px;
  }

  h1 {
    color: red;
    font-size: 4em;
  }
}
```

브라우저가 0 ~ 768px일 때 화면이 더 이상 줄어들지 않고  
고정될 수 있도록 설정할 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/179899658-d8ca91e8-cf27-45ae-8550-340e21f24c47.png" width="70%">  

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
