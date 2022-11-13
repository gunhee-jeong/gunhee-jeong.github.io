---
layout: single
title: "minimal mistakes 블로그 환경설정"
# categories: Git
categories:
  - Tool # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [blog, 블로그] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
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

# git blog 환경설정
```bash
🗂 _data
🗂 _includes
🗂 _layouts
......
_config.yml
        # ├── AbmKMg9BFeVUuJ7lsQ1w8
        # ├── chunks                 // 여러 페이지에서 공통으로 사용되는 번들 파일
        # │       └──  pages         // 각 페이지의 번들 파일
        # ├── runtime                // 웹팩과 next의 런타임과 관련된 번들 파일
        # ├── css                    // 애플리케이션의 모든 페이지에 대한 글로벌 CSS 파일
        # └── media                  // 정적으로 가져온 이미지 next/image가 여기에 해시 및 복사
```

# 🔴 config.yml
## 🟠 blog title 설정  
## 🟠 blog logo image  
## 🟠 blog bio 수정
## 🟠 blog main 페이지의 최근 포스트 노출 개수 설정 -> `paginate`

# 🔴 category(blog 상단의 Home Category Search)
## 🟠 tag 박스 color
```bash
🗂 _data
🗂 _includes
🗂 _layouts
🗂 _pages
🗂 _posts
🗂 _sass
 └── 🗂 minimal-mistakes
      ├── 🗂 skins
      └── 🗂 vendor
           └── _page.scss
_config.yml
```
_page.scss 파일에서 .page\_\_taxonomy-item-tag {(line 333)

## 상단 category 클릭시, 메인화면 글자 색상

- sass > \_page.scss  
  .taxonomy\_\_index a(line 437)

# 🔴 posting
## 🟠 Posting 좌측 메뉴바 만들기
```bash
🗂 _data
🗂 _includes
🗂 _layouts
🗂 _pages
 ├── 🗂 categories
 ├── 404.md
 ├── category-archive.md
 ├── serch.md
 └── tag-archive.md
🗂 _posts
🗂 _sass
_config.yml
```
/_pages/categories 에서 새로 추가할 이름으로 파일을 생성한다.

```java
title: "Programmers 1단계" //좌측 메뉴바에 보이게 될 메뉴의 이름
layout: archive
permalink: categories/programmers1 //pages 폴더 -> categories 폴더 -> 에서 만든 파일의 이름
author_profile: true
sidebar_main: true

% assign posts = site.categories.Programmers1 % //-> post 글 작성시 categories에서 사용하게 될 메뉴 이름
```
includes 폴더 -> <u>nav_list_main 파일</u>로 이동하여 `위의 메뉴 이름을 추가`한다.  

## 본문 페이지

- ``코드블록  
  \_sass -> \_base.scss -> line 541~542

# 🔴 블로그 CSS 설정
```bash
🗂 _data
🗂 _includes
🗂 _layouts
🗂 _pages
🗂 _posts
🗂 _sass
└── 🗂 minimal-mistakes
    └── 🗂 skins
    └── 🗂 vendor
        ├── _reset.scss
        ├── _base.scss
        ├── _syntax.scss
        └── _page.scss
```

## 🟠 제목, 링크, 강조색
sass 디렉터리 안에 skins에 들어가 자신이 선택한 스킨의 scss 파일로 들어간다.

강조색은 $primary-color를 변경하면 된다.

## 🟠 글자 크기 변경
_reset.scss에 들어가서 아래의 코드와 같이 변경할 수 있다. 아래의 코드를 해석해보면, 폰 화면에서는 14px, 태블릿이나 pc 화면에서는 16px로 보이도록 설정했다.

```jsx
html {
  /* apply a natural box layout model to all elements */
  box-sizing: border-box;
  background-color: $background-color;
  font-size: 14px;

  @include breakpoint($medium) {
    font-size: 16px;
  }

  @include breakpoint($large) {
    font-size: 16px;
  }

  @include breakpoint($x-large) {
    font-size: 16px;
  }

  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
}
```

## 🟠 인라인 코드 강조 색상 변경
_base.scss에서 아래의 코드와 같이 내용을 변경하자.

```jsx
p > code,
a > code,
li > code,
figcaption > code,
td > code {
  padding-top: 0.1rem;
  padding-bottom: 0.1rem;
  font-size: 0.8em;
  // background: $code-background-color;
  background: DarkSlateGray;
  // color: $primary-color;
  color: LightGray;
  border-radius: $border-radius;
```

## 🟠 코드 블록 색상 변경하기
_syntax.scss에서 아래와 같이 코드를 변경하자.

```jsx
div.highlighter-rouge,
figure.highlight {
  position: relative;
  margin-bottom: 1em;
  // background: $base00;
  background: #2D2D2D;
  color: $base05;
  font-family: $monospace;
  font-size: $type-size-6;
  line-height: 1.8;
  border-radius: $border-radius;
```

## 🟠 최근 포스트 list
### 🟡 page taxonomy
_page.scss의 .page__taxonomy-item-tag와 .page__taxonomy-item-category에서 CSS를 수정할 수 있다.

## 🟠 toc_menu
toc_menu는 블로그의 목차를 요약해준다. 나의 경우는 nover를 주석 처리하여 효과를 없애주는 작업을 했다.
```jsx
.toc__menu {
  margin: 0;
  padding: 0;
  width: 100%;
  list-style: none;
  font-size: $type-size-6; //toc 모바일 화면에서 소제목 font 크기

  @include breakpoint($large) {
    font-size: $type-size-6; //toc 전체화면에서 소제목 font 크기
  }

  a {
    display: block;
    padding: 0.25rem 0.75rem;
    color: $muted-text-color;
    font-weight: bold;
    line-height: 1.5;
    border-bottom: 1px solid $border-color;

    // &:hover {
    //   color: $text-color;
    // }
  }
```


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
