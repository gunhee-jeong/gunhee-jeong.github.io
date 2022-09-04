---
layout: single
title: "리덕스 thunk 와 미들웨어(middleware)"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [리액트 기초, 미들웨어] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-09-02T13:50:00+09:00
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

.teal {
  color: teal;
  font-weight: bold;
}

.forestgreen {
  color: foresgreen;
  font-weight: bold;
}
</style>

# 리덕스 thunk와 middleware
(화해 블로그)) : [Redux Toolkit은 정말 천덕꾸러기일까?](http://blog.hwahae.co.kr/all/tech/tech-tech/6946/)

# middleware
<u>소프트웨어 공학적 관점</u>에서의 `미들웨어`는 <span class="teal">운영 체제와 응용 소프트웨어 중간에서 조정과 중개</span>의 역할을 수행하는 소프트웨어라 할 수 있다.

`리덕스 미들웨어`는 <u>dispatch된 액션</u>이 <span class="teal">리듀서에 도달하기 전</span> 중간 영역에서 <span class="mediumblue">사용자의 목적에 맞게 기능을 확장할 수 있도록 도와주는</span> 역할을 한다. 예를 들어 미들웨어로 redux-logger를 추가하면 액션이 디스패치될 때마다 개발자 도구 콘솔에 로그가 찍히는 것을 생각해 볼 수 있다. 로그를 출력하는 과정이 중간에 추가된 것이다. 이처럼 개발자는 <span class="teal">자신의 필요에 따라 미들웨어를 작성</span>하여 원하는 목적을 달성할 수 있게 된다.

<img src="https://user-images.githubusercontent.com/87808288/188295814-3153a43e-f38e-4236-8aa7-57d8eb58503c.png" width="70%">  

리덕스에 임의의 기능을 넣어 확장하는 방법으로는 미들웨어를 추천한다. 미들웨어의 중요한 기능 중 하나는 조합이 가능하다는 점이다. redux-thunk는 액션 생산자가 디스패치 함수를 통해 제어를 역전할 수 있게 한다. 액션 생산자는 dipatch를 인수로 받아 비동기적으로 호출할 수 있다. 이런 함수들을 thunk라고 부른다.

# 리덕스 thunk
`redux-thunk`는 리덕스를 사용하는 어플리케이션에서 <span class="crimson">비동기 작업</span>을 처리할 때 가장 기본적으로 사용되는 방법으로 redux-thunk 라는 <span class="mediumblue">미들웨어</span>를 사용하는 것이다. 

## thunk 란?
thunk는 <u>특정 작업을 나중에 하도록</u> 미루기 위해 <span class="teal">함수형태로 감싸는 것</span>을 말한다. 

```bash
npm i redux-thunk
```

```jsx
// store.js
import { applyMiddleware, legacy_createStore as createStore } from 'redux';

import thunk from 'redux-thunk'; //

import reducer from './reducer';

const store = createStore(reducer, applyMiddleware(thunk)); //

export default store;
```

```jsx
// actions.jsx
import { fetchCategories } from './services/api';

// action creator
export function changeRestaurantFiled({ name, value }) {
  return {
    type: 'changeRestaurantFiled',
    payload: {
      name,
      value,
    },
  };
}

export function setRestaurants(restaurants) {
  return {
    type: 'setRestaurants',
    payload: {
      restaurants,
    },
  };
}

export function addRestaurant() {
  return {
    type: 'addRestaurant',
  };
}

export function loadRestaurants() {
  return async (dispatch) => {
    // TODO: fetch......
    const restaurants = [];
    dispatch(setRestaurants(restaurants));
  };
}

export function setCategories(categories) {
  return {
    type: 'setCategories',
    payload: {
      categories,
    },
  };
}

export function loadCategories() {
  return async (dispatch) => {
    const categories = await fetchCategories();
    dispatch(setCategories(categories));
  };
}
```


<!-- ① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨-->

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
