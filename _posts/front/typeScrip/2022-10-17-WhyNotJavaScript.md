---
layout: single
title: "Why not JavaScript"
# categories: Git
categories:
  - TypeScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [노마드코더] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-10-17T17:30:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.red {
  color: crimson;
}

.blue {
  color: mediumblue;
}

.green {
  color: forestgreen;
}
</style>

# Why not JavaScript
타입스크립트의 <span class="red">타입 안정성</span>으로 많은 이점을 가질 수 있게 된다. 코드 등에 버그를 매우 많이 줄일 수 있게 된다. 타입 안정성은 타입스크립트가 제공하는 가장 큰 장점이다.

기본적으로 자바스크립트라는 언어는 굉장히 <span class="green">유연한 언어</span>이다. 자바스크립트는 <u>에러를 보여주지 않으려고</u> 많은 노력을 하는 언어이다.

```jsx
console.log([1, 2, 3, 4] + false); // '1, 2, 3, 4false'
```

개발자가 위의 코드와 같이 작성하면 자바스크립트는 그냥 <u>string 으로 바꾸며 에러는 발생시키지 않는다</u>. 다른 언어들은 이런 것들을 기본적으로 허용하지 않는다.

```jsx
function divide(a, b) {
  return a / b;
}

divide(2, 3); // 0.6666.....
```

우리가 일반적으로 생각하는 divide 함수의 사용방법은 위의 코드와 같이 숫자를 인수로 넣어서 사용하는 것이다. 그러나 <span class="green">사용자</span>가 아래의 코드와 같이 divide 함수를 사용할 수도 있다.

```jsx
divide("xxxxxx"); // NaN
```

사용자가 위의 코드와 같이 divide 함수를 사용해도 <u>자바스크립트는 에러를 발생시키지 않는다</u>. divide 함수는 기본적으로 인수를 2개 받아야 하는 함수인데도 불구하고 위의 코드와 같이 실행해도 <span class="blue">자바스크립트는 에러를 발생시키지 않고 함수를 실행</span>시킨다. <span class="green">이런 점들은 편해보일 수 있지만</span> 이런 부분들이 쌓이다보면 예상치 못한 문제들이 한번에 쏟아져 나오는 경우가 생기게 된다.

자바스크립트의 가장 큰 단점은 <span class="red">런타입 에러</span>이다.(런타임 에러는 코드가 실행되는 동안 발생하는 에러를 말한다.)

```jsx
const gunhee = { name: 'gunhee' };

gunhee.hello(); // Uncaught TypeError
```

위의 코드와 같이 <u>코드가 실행되기 전에 이미 에러를 확인할 수 있는 것이 가장 좋은 방법</u>이다. 그러나 위의 `Uncaught TypeError` 는 <span class="blue">사용자가 컴퓨터에서 코드를 실행할 때 나타나는 에러</span>이다. 좋은 프로그래밍 언어라면 gunhee 라는 객체를 분석하여 hello 함수가 있는지 없는지 확인할 수 있어야 한다.

<!-- <span style="color:mediumblue"> -->

<!-- ① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨-->

<!-- 메소드 위에 변수 선언, 메소드  안에 메소드, 메소드 끝나고 리턴 -->

<!-- ### 2. Link 넣기

```

유형 1: (설명어를 입력) : [gunhee's coding blog](https://gunhee-jeong.github. io/)
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
<span style="color:crimson">빨간 글씨</span> -> 글자색
이것이 `인라인` 입니다 -> 인라인 코드
```

**진하게** -> 볼드
_기울여서_ -> 이탤릭체
~~취소선~~ -> 취소선
<u>밑줄넣기</u> -> 밑줄
<span style="color:crimson">빨간 글씨</span>
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
</details> -->
