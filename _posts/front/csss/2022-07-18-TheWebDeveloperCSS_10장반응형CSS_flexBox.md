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
<u>행이나 열이</u> <span style="color:tomato">여러 개</span>일 때 <span style="color:blue">cross axis를 기준으로 정렬</span>한다.  
align content는 여러 행, 여러 열이 있을 때에만 사용하는 정렬 방법이다.  

<u>main axis가 수직</u>으로 되어있을 때 `align-content`는 <span style="color:tomato">열 사이의 공간을 조정</span>하게 된다.  
반대로 <u>수평을 주축으로 한다면</u> cross axis는 수직이므로 `aling-content`는 <span style="color:tomato">행 사이의 공간을 조정</span>한다.  

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
