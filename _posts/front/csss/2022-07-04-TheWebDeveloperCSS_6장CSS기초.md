---
layout: single
title: "The Web Developer CSS -> 6장 CSS 기초"
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
# 6장 CSS 기초
## 1. 스타일 sheet
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS Intro</title>
  <link rel="stylesheet" href="styles/app.css">
</head>

<body>
</body>
```

stylesheet가 들어가는 자리는 언제나 &lt;head&gt;에 &lt;link&gt;로 연결한다.  

## 2. CSS layout
### (1) display
#### [block]
<img src="https://user-images.githubusercontent.com/87808288/180231807-9f3de22c-67a2-47ca-926b-57ad8e0b8c0c.png" width="100%">  

```css
span.c {
  display: block;
  width: 100px;
  height: 100px;
  padding: 5px;
  border: 1px solid blue;    
  background-color: yellow; 
}
```

display: `block`;에서는 <span style="color:tomato">width와 height를 줄 수</span> 있지만 <span style="color:red">element가 한 줄을 모두 차지</span>하게 된다.  
<u>padding 속성도 넣어줄 수</u> 있다.  
#### [inline]
<img src="https://user-images.githubusercontent.com/87808288/180230117-f63b2af8-282b-4b65-af0a-5e7be1d61f94.png" width="100%">  

```css
span.a {
  display: inline; /* the default for span */
  width: 100px;
  height: 100px;
  padding: 5px;
  border: 1px solid blue;  
  background-color: yellow; 
}
```

display:`inline`;은 &lt;span&gt;의 기본적인 display 속성이다.  

상하좌우에 <span style="color:blue">padding</span>을 주어도 <span style="color:tomato">상하에만 padding이 적용</span>된다.  
또한 <span style="color:red">width</span>와 <span style="color:red">height</span>가 <u>적용되지 않는다</u>.  


#### [inline-block]
<img src="https://user-images.githubusercontent.com/87808288/180242329-d36d1d5a-a96d-443f-8d86-a6092c1b3a51.png" width="100%">  

```css
span.b {
  display: inline-block;
  width: 100px;
  height: 100px;
  padding: 5px;
  border: 1px solid blue;    
  background-color: yellow; 
}
```

display: inline;과 비교하여 차이점은 element의 <span style="color:blue">width</span>와 <span style="color:blue">height</span>를 <u>설정할 수 있다는 것</u>이다.  
또한 `inline-block`을 사용하면 <span style="color:tomato">상하의 margin과 padding을 사용할 수</span> 있지만 inline에서는 사용할 수 없다.  

## 3. 일반 텍스트 속성
### (1) text-align
텍스트의 정렬  

### (2) font-weight
폰트의 굵기  

### (3) text-decoration
텍스트의 밑줄 등을 생성하고 지울 수 있다.  

### (4) line-height
텍스트와 텍스트 사이의 줄을 간격을 조절할 수 있다.  

### (5) font-size
글자 크기를 조절할 수 있다.  

픽셀(px)은 가장 흔히 사용되는 <span style="color:royalblue">절대 단위</span>이다.  
픽셀로 font가 지정되면 어느곳이든 <span style="color:blue">동일한 크기</span>를 유지하게 된다.  

### (6) letter-spacing
```css
div {
  letter-spacing: 1px;
}
```

letter-spacing은 <span style="color:blue">글자 간의 간격을 전체적으로 늘려주는</span> 역할을 한다.  
<img src="https://user-images.githubusercontent.com/87808288/180222324-481e0a67-2e9d-4479-9348-c5b6c77fc8c4.png" width="40%">
<img src="https://user-images.githubusercontent.com/87808288/180222392-18e5efe6-df47-4a00-b53f-80465351271a.png" width="34%">  


## 4. font family

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
