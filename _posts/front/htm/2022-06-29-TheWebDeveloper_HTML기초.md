---
layout: single
title: "The Web Developer -> HTML 기초"
# categories: Git
categories:
  - HTML # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer, 태그, tag] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-06-28T09:40:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1장 HTML 기초

# HTML의 정의와 기능

- HTML은 웹 페이지를 만들기 위한 언어
- HTML을 사용하여 `웹 페이지의 구조`를 잡을 수 있다.
- 이미지, 텍스트, 비디오, 버튼 등 웹 사이트에 보여줄 내용을 구성하고 있다.

# HTML tag

HTML 파일에 필요한 최소한의 tag는 다음과 같다.

```html
<html></html>
<head></head>
<body></body>
```

## tag의 구성

HTML에서 이미지나 text를 그리려면 그에 맞는 <span style="color:red">tag</span>를 사용하여야한다.  
tag는 기본적으로 `<>`로 감싸져서 사용된다.  
<u>tag는 시작하면 꼭 끝맺음을</u> 하여야하는데, `시작과 동시에 종료되는 tag들도` 존재한다.

```bash
<img> <br>
```

## tag의 attribute(속성)

```html
<div class="title">시작!</div>
<a href="https://naver.com">네이버로 이동</a>
<img src="./me.png" alt="내사진" />
```

<img src="https://user-images.githubusercontent.com/87808288/152677335-5d01e2bf-0327-4d6f-ba00-a34c18b3888a.png" width="450" height="200">

`attribute`는 <u>시작 tag에 위치</u>하고, <u>한 tag에 여러 attribute를 지정</u>할 수 있다.

## tag의 element(요소)

<img src="https://user-images.githubusercontent.com/87808288/152675115-dfa6c37f-4064-45b1-bb85-6a3b291e3d0b.png" width="200" height="200">

`tag로 시작하여 tag로 끝나는 하나`를 <span style="color:red">element</span>라고 정의하고, 이를 <span style="color:red">node</span>라고도 부른다.

- <u>element = node</u> > content

# 1장 HTML의 기초
## 1. 태그
### (1) p 태그
p 태그를 사용하여 앞 단락과 뒷 단락을 명확히 구분해줄 수 있다.  
p 태그를 사용하면 단락과 단락 사이에 공간이 추가되는데, 이 공간은 블록 레벨 요소라고 한다.  
이는 한 블록의 공간을 모두 차지하게 된다.  
이렇게 한 블록을 차지하면 -> 다음 단락은 다음 줄부터 나오도록 강제하게 된다.  

### (2) 제목 태그
h1 태그와 h2 태그가 없다면 h3 태그는 존재할 수 없다.  

```html
<h1>대한민국</h1>
<h2>서울</h2>
<h3>강동구</h3>
```

### (3) 타이틀 태그
```html
<!DOCTYPE html>
<html>
    <head>
      <title>hellow world</title>
    </head>
</html>
```

DOCTYPE html 태그는 html 파일임을 알려주는 역할을 한다.  

title 태그는 웹페이지의 타이틀을 설정해준다.  
페이지가 아닌 브라우저에 뜨는 정보인 것이다.  

### (4) body 태그
문서의 모든 내용을 담고 있는 요소이다.  

<u>기본적인 html 태그의 구성</u>을 불러오고 싶다면 <span style="color:red">! + Tab</span>을 입력하면 된다.  
그러면 기본적으로 <span style="color:royalblue">DOCTYPE 부터 body 태그까지 자동으로 생성</span>시켜준다.  

### (5) 목록 요소
```html
<body>
  <ul>
    <li>Silkie</li>
    <li>Polish</li>
    <li>Easter Egger</li>
    <li>Rhode Island Red</li>
  </ul>

  <ol>
    <li>Silkie</li>
    <li>Polish</li>
    <li>Easter Egger</li>
    <li>Rhode Island Red</li>
  </ol>
</body>
```

```html
<body>
  <ul>
    <li>Bantam
      <ul>
        <li>Silkie</li>
        <li>Polish</li>
      </ul>
    </li>
    <li>standard
      <ul>
        <li>Easter Egger</li>
        <li>Rhode Island Red</li>
      </ul>
    </li>
  </ul>
</body>
```

### (6) 앵커 태그
HTML의 속성이란 태그에 부여할 수 있는 작은 정보를 의미한다.  

```html
<body>
  <a href="목적지site주소"></a>
</body>
```

## 2. 이미지
이미지 태그는 열고 닫는 태그가 없는 요소이다.  
이미지 태그의 열고 닫는 태그가 없는 것은 생각해보면 당연한 것이다.  
왜냐하면 위의 다양한 요소들은 사실 모두 텍스트들로 채워져 있었다.  
하지만 이미지 태그는 이미지가 있는 URL만을 제공하는 것이 목적이기 때문에 위의 태그들이 없어도 되는 것이다.  

```html
<body>
  <img src="pictures/stevie_chicks.jpg" alt="My pet chicken, Stevie">
</body>
```

pictures 폴더 안에 들어있는 "stevie_chicks.jpg" 이미지 파일을 img 태그를 사용하여 화면에 나타냈다.  



<!-- <span style="color:royalblue"> -->

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
