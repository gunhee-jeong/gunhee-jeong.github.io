---
layout: single
title: "Text Style"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [text style, text-align, indent] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# text-align

<u>box 안의 content</u>를 <span style="color:red">text-align</span>을 사용하여 `center`, `left`, `right` 등으로 이동시킬 수 있다.

```html
<body>
  <section>
    <div class="one">11111</div>
    <div class="two">22222</div>
    <div class="three">33333</div>
  </section>
</body>
```

```css
div {
  width: 80px;
  height: 80px;
  background: red;
  margin: 10px;
}

.one {
  text-align: center;
}

.two {
  text-align: left;
}

.three {
  text-align: right;
}
```

<img src="https://user-images.githubusercontent.com/87808288/152684265-6730b4b9-58f0-485d-820c-e90fd17bbf84.png" width="70" height="130">

`inline-element`인 <span style="color:red">span</span>은 **text-align: right;**로 지정하여도  
<u>text 영역 만큼을 차지하고 있기 때문에 정렬되지 않는다</u>.

<img src="https://user-images.githubusercontent.com/87808288/152684753-fe92ef81-babc-42eb-a885-e0c94c653372.png" width="250" height="100">  
- 위의 사진에서 보이는 바와 같이, <span style="color:red">span</span>은 `inline-element`이기 때문에   
<u>text 영역만큼을 차지하므로 정렬되지 않았다</u>.

# indent

text-indent를 사용하여 CSS로 `들여쓰기`할 수 있다.  
HTML 코드에서 스페이스와 엔터를 아무리 추가하여도, 실제 결과 화면에는 적용되지 않는다.

```css
.js-description {
  text-indent: 50px;
}
```

문장 사이사이에 스페이스를 추가하고 싶다면, `&nbsp;`를 넣어주면 된다.

```html
<p>스페이스 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;넣는 예제</p>
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
