---
layout: single
title: "localStorage 와 sessionStorage"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [storage] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-09-24T:00:00+09:00
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
</style>

# localStorage 와 sessionStorage

# 🔴 localStorage 와 sessionStorage
(JAVASCRIPT.INFO) : [localStorage 와 sessionStorage](https://ko.javascript.info/localstorage)

웹 스토리 객체(web storage object)인 `localStorage` 와 `sessionStorage` 는 브라우저 내에 키-값 쌍을 저장할 수 있게 한다.

이 둘을 이용하면 페이지를 새로 고침(sessionStorage) 심지어 브라우저를 다시 실행해도 (localStorage) 데이터가 사라지지 않고 남아있다.

쿠키 이외에도 이러한 방법을 사용하는 이유는 쿠키와 다르게 웹 스토리지 객체는 <u>네트워크 요청 시 서버로 전송되지 않는다</u>. 이러한 특징으로 <span class="forestgreen">쿠키보다 더 많은 자료를 보관</span>할 수 있다. 대부분의 브라우저가 최소 2MB 혹은 그 이상의 웹 스토리지 객체를 저장할 수 있게 해준다.

쿠키와 또 다른 점은 서버가 HTTP 헤더를 통해 스토리지 객체를 조작할 수 없다는 것이다. 웹 스토리지 객체 조작은 모두 자바스크립트 내에서 수행된다.

웹 스토리지 객체는 도메인, 프로토콜, 포트로 정의되는 오리진에 묶여있다. 따라서 프로토콜과 서브 도메인이 다르면 데이터에 접근할 수 없다.

## 🟠 메서드와 프로퍼티
두 스토리지 객체는 동일한 메서드와 프로퍼티를 제공한다.
- setItem(key, value): 키, 값 쌍을 보관한다.
- getItem(key): 키에 해당하는 값을 받아온다.
- removeItem(key): 키와 해당 값을 삭제한다.
- clear(): 모든 것을 삭제한다.

## 🟠 localStorage
`localStorage` 는 오리진이 같은 경우 데이터는 모든 탭과 창에서 공유된다. 또한 <span class="mediumblue">브라우저나 OS가 재시작하더라도 데이터가 파기되지 않는다</span>.

```jsx
localStorage.setItem('test', 1);

alert( localStorage.getItem('test') ); // 1
```

오리진(domain/ port/ protocol)만 같다면 url 경로는 달라도 동일한 결과를 볼 수 있다.

### 🟡 키 순회
localStorage 는 '키'를 사용해 값을 얻고, 설정하고, 삭제할 수 있다.

스토리지 객체는 iterble 객체가 아니다. 대신 배열처럼 다루면 전체 키 값을 얻을 수 있다.

```js
for(let i=0; i<localStorage.length; i++) {
  let key = localStorage.key(i);
  alert(`${key}: ${localStorage.getItem(key)}`);
}
```



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
