---
layout: single
title: "The Web Developer -> HTML 시맨틱(Semantics)"
# categories: Git
categories:
  - HTML # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-06-30T12:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 2장 HTML 시맨틱
## 1. HTML5?
DOCTYPE의 역할은 브라우저에 이 문서가 HTML5 구문 또는 HTML5 버전 표준을 쓴다는 것을 알려주는 것이다.  

## 2. 블록 VS 인라인 요소(div와 span)
<img src="https://user-images.githubusercontent.com/87808288/176585915-0e43b85e-ac88-4f14-8b4c-de5e978ad33d.png" width="350">  
기본적으로 `블록 레벨`과 `인라인 레벨`을 가지고 있지만, CSS를 통해서도 이 레벨을 바꿀 수 있다.  

### (1) 블록
h1 태그나 h2 태그와 같은 <span style="color:red">블록</span> 수준의 element는 <span style="color:tomato">한 줄을 모두 차지하게</span> 된다.  
문단도 혼자서 한 줄의 블록을 모두 차지한다.  

#### [div 태그]
<span style="color:red">div 태그</span>는 <u>division(분할)을 의미</u>하는 태그이다.  
div 태그는 <span style="color:tomato">무언가를 잡아</span> 두고, 또는 element를 <span style="color:tomato">그룹화하기 위해서</span> 사용된다.  
div 태그는 블록 레벨을 가지기 때문에 전체의 블록을 차지하고, 위아래의 콘텐츠들을 밀어낸다.  

### (2) 인라인
앵커 태그는 인라인이다.  

#### [span 태그]
span 태그는 인라인 레벨을 가진다.  
span 태그를 사용하면 <u>한 줄에 같이 있는 element들</u> 각각의 <span style="color:tomato">위치를 그대로 두고</span> 여러 스타일 등을 적용시킬 수 있다.  

## 3. 기타 요소들(HR, BR, Sup, Sub)
### (1) HR 태그(Horizontal Rule)
hr 태그에는 내용이나 속성을 부여할 필요가 없다.  

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
  <hr>
</body>
```

hr 태그는 이런식으로 문단 등을 구별할 수 있는 수평의 선을 부여한다.  
그리고 hr 태그의 선은 스타일링도 가능하다.  

### (2) br 태그(Line Breack)
줄을 바꾸는 태그이다.  

```html
<body>
  <p>
    agagjaweginaeiobnv aejrgvaj adfjann ina nsljlvk mlakjsviwjvi sdivna j <br>
    agagjaweginaeiobnv aejrgvaj adfjann ina nsljlvk mlakjsviwjvi sdivna j 
    agagjaweginaeiobnv aejrgvaj adfjann ina nsljlvk mlakjsviwjvi sdivna j 
  </p>
</body>
```

문단에서 문장의 줄을 바꾸고 싶을 때 p 태그들을 여러 개 추가하여 표현할 수도 있겠지만  
그러면 문단을 나누는 의미가 퇴색된다.  
그러므로 p 태그 내부에 br 태그 등을 사용하여 문장의 줄을 바꾸어 표현할 수 있다.  

### (3) sup 태그(위첨자)
sup 태그를 사용하면 위첨자를 만들 수 있다.  

```html
<body>
  <p>
    agagjaweginaeiobnv aejrgvaj adfjann ina nsljlvk mlakjsviwjvi sdivna <sup>[1]</sup>j <br>
    agagjaweginaeiobnv aejrgvaj adfjann ina nsljlvk mlakjsviwjvi sdivna j 
    agagjaweginaeiobnv aejrgvaj adfjann ina nsljlvk mlakjsviwjvi sdivna j 
  </p>
</body>
```

### (4) sub 태그(아래첨자)

## 4. 엔티티 코드
엔티티 코드는 HTML 대신 사용할 수 있는 특별한 코드 또는 시퀀스이다.  

엔티티 코드는 <u>&로 시작하고 ;로 끝나는 특징</u>을 갖는다.  
태그들의 사이에 특정한 기호를 넣고 싶은데 이를 vsCode가 태그가 열려있다고 판단하여 error를 일으키는 경우가 있다.  
그래서 엔티티 코드를 사용해야 하는 순간들이 온다.  

"보다 작은"이라는 기호를 엔티티로 사용하려면 &lt를, "보다 큰"이라는 기호를 엔티티로 사용하면 &rt로 나타낼 수 있다.  

## 5. 시맨틱 마크업 개요
`시맨틱 마크업`을 생성하는 이유는 <span style="color:red">마크업에 의미를 부여</span>하기 위한 것이다.  
<u>개발자들이 함께 코드를 보았을 때</u> -> <span style="color:tomato">무슨 일이 일어나고 있는지 한 눈에</span> 알아볼 수 있게 도와준다.  

## 6. 시맨틱 요소 사용법
### (1) main 태그
### (2) nav 태그
페이지에서 내비게이션 링크를 제공하는 것들을 나타내게 된다.  

### (3) section 태그
### (4) article 태그
&lt;article&gt; 안에도 &lt;footer&gt;가 들어갈 수 있다.  
이런식으로 다양하게 응용할 수 있다.  

### (5) aside 태그
### (6) header 태그
### (7) figure 태그

## 7. 스크린 리더 데모
## 8. Emmet

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
