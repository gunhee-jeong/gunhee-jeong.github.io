---
layout: single
title: "New JSX Transform"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [리액트 공식 블로그] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-08-10T16:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
(react 공식 블로그) : [What’s Different in the New Transform?](https://ko.reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html#whats-different-in-the-new-transform)  

# 1. What's Different in the New Transform?
<span class="tomato">JSX</span>를 사용할 때,  
컴파일러는 브라우저가 이를 이해할 수 있도록 <span class="royalblue">React 함수를 호출</span>하여 이를 변환했고  
이전 JSX 변환은 <span class="blue">React.createElement() 호출</span>로 바꾸었다.  

```jsx
import React from 'react';

function App() {
  return <h1>Hello World</h1>;
}
```

위의 코드를 아래와 같이 호출하여 사용하였다.  

```jsx
import React from 'react';

function App() {
  return React.createElement('h1', null, 'Hello world');
}
```

하지만 이러한 방식은 <span class="royalblue">완벽하지 않았다</span>.  
JSX는 React.createElement로 컴파일되기 때문에 JSX를 사용하는 경우 React의 스코프 범위 내에 있어야 한다.  

이러한 문제를 해결하기 위해 React 17은 Babel 및  
TypeScript와 같은 컴파일러에서만 사용하도록 설계된 두 개의 새로운 진입점을 React 패키지에 도입했다.  
JSX를 React.createElement로 변환하는 대신  
<span class="blue">새 JSX 변환</span>은 <span class="tomato">자동으로 React 패키지의 새 진입점에서 특수 기능을 가져와 호출</span>한다.  
새 JSX 변환은 아래와 같다.  

```jsx
function App() {
  return <h1>Hello World</h1>;
}
```

```jsx
// Inserted by a compiler (don't import it yourself!)
import {jsx as _jsx} from 'react/jsx-runtime';

function App() {
  return _jsx('h1', { children: 'Hello world' });
}
```

이렇게 <span class="royalblue">JSX를 사용</span>하기 위해 <span class="blue">더이상 React를 가져올 필요가 없어</span>졌다.  
`react/jsx-runtime` 및 `react/jsx-dev0-runtime` 내부의 함수는 <span class="blue">컴파일러 변환에서만 사용</span>해야한다.  

# 2. How to Upgrade to the New JSX Transform
## (1) Manual Babel Setup
```bash
# for npm users
npm update @babel/core @babel/plugin-transform-react-jsx
```

```bash
# for npm users
npm update @babel/core @babel/preset-react
```

```bash
// If you are using @babel/preset-react
{
  "presets": [
    ["@babel/preset-react", {
      "runtime": "automatic"
    }]
  ]
}
```

## (2) Eslint
```bash
{
  // ...
  "rules": {
    // ...
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off"
  }
}
```

<style>
.red {
  color: red;
  font-weight: bold;
}

.tomato {
  color: tomato;
  font-weight: bold;
}

.blue {
  color: blue;
  font-weight: bold;
}

.royalblue {
  color: royalblue;
  font-weight: bold;
}

.forestgreen {
  color: forestgreen;
  font-weight: bold;
}

.darkorange {
  color: darkorange;
  font-weight: bold;
}
</style>

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
