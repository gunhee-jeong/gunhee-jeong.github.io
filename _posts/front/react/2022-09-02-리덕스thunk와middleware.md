---
layout: single
title: "리덕스 thunk 와 middleware"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [리액트 기초] #tag는 여러개 가능함
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
# middleware
`미들웨어`는 <u>dispatch 함수를 결합</u>해서 <span class="teal">새 dispatch 함수를 반환하는 고차함수</span>이다. action을 로깅하거나, 라우팅과 같은 부수 효과를 일으키거나, 비동기 API 호출을 일련의 동기 action으로 바꾸는데 유용하다.

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
