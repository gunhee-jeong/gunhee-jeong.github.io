---
layout: single
title: "리액트 useContext"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Context API] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-10-07T15:30:00+09:00
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

<img src="https://user-images.githubusercontent.com/87808288/194484587-bc19966c-993f-4a75-9fb3-c3e68df54b25.png" width="60%">  
위의 이미지와 같이 일반적으로 자식 컴포넌트에게 data 를 전달하기 위해서는 Prop Drilling 을 사용하게 된다. 하지만 이러한 방법의 큰 문제는 A 컴포넌트와 B 컴포넌트는 데이터가 필요하지 않음에도 data 를 거쳐가야한다는 것이다.(A, B, D 는 해당 data 를 몰라도 되지만 Prop Drilling 에서는 모두 data 를 알게 된다.)

<img src="https://user-images.githubusercontent.com/87808288/194490710-fc2ceb4c-db57-48f9-9d98-7e31bdd2f631.png" width="60%">  
context 를 사용하면 위의 이미지와 같이 자식 컴포넌트 중에서 data 가 필요한 컴포넌트는 직접 data 를 받아볼 수 있게 된다.

하지만 Context 를 사용하면 컴포넌트를 재사용하기 어려워질 수 있다. 때문에 Prop drilling 을 피하기 위한 목적이라면 Compnent Composition(컴포넌트 합성)을 먼저 고려해야한다.

```bash
/src/componets
          ├── Content.jsx
          ├── Footer.jsx
          ├── Header.jsx
          └── Page.jsx
      App.jsx
      App.css
      index.jsx
      context
          └── ThemeContext.jsx
```

<img src="https://user-images.githubusercontent.com/87808288/194495750-1292030b-1bb8-4a93-b66a-3fc1eaf224b2.png" width="40%">

# 🔴 Prop Drilling

```jsx
// App.jsx
import { useState } from "react";

import "./App.css";

import Page from "./component/Page";

export default function App() {
  const [isDark, setIsDark] = useState(false);

  return (
    <Page isDark={isDark} setIsDark={setIsDark} />
  );
}
```

```jsx
// Page.jsx
import Content from "./Content";
import Footer from "./Footer";
import Header from "./Header";

export default function Page({ isDark, setIsDark }) {
  return (
    <div className="Page">
      <Header isDark={isDark} />
      <Content isDark={isDark} />
      <Footer isDark={isDark} />
    </div>
  );
}
```

```jsx
// Header.jsx
export default function Header({ isDark }) {
  return (
    <header
      className="Page"
      style={ {
        backgroundColor: isDark ? "black" : "lightgray",
        color: isDark ? "white" : "black",
      } }
    >
      <h1>Welcome 홍길동!</h1>
    </header>
  );
}
```

```jsx
// Content.jsx
export default function Content({ isDark }) {
  return (
    <div
      className="content"
      style={ {
        backgroundColor: isDark ? "black" : "white",
        color: isDark ? "white" : "black",
      } }
    >
      <p>좋은 하루 되세요</p>
    </div>
  );
}
```

```jsx
// Footer.jsx
export default function Footer({ isDark, setIsDark }) {
  function toggleTheme() {
    setIsDark(!isDark);
  }

  return (
    <footer
      className="footer"
      style={ {
        backgroundColor: isDark ? "black" : "lightgray",
      } }
    >
      <button className="button" onClick={toggleTheme}>
        Dark Mode
      </button>
    </footer>
  );
}
```

# 🔴 Context
```jsx
// ThemeContext.jsx
import { createContext } from 'react';

export const ThemeContext = createContext(null);
```

위의 `ThemeContext.jsx` 에는 <span class="crimson">createContext</span> 를 사용하여 context 를 생성하게 된다. 그러면 이 기존의 코드들에서 사용하던 props 를 사용하지 않고도 ThemeContext 를 사용하여 data 가 필요한 컴포넌트들에서 바로 사용할 수 있게 된다. 변화되는 코드들은 아래와 같다.

```jsx
// App.jsx
import { useState } from "react";

import "./App.css";

import Page from "./component/Page";

import { ThemeContext } from './context/ThemeContext';

export default function App() {
  const [isDark, setIsDark] = useState(false);

  return (
    <ThemeContext.Provider value={ { isDark, setIsDark } }>
      <Page />
    </ThemeContext.Provider>
  );
}
```

이렇게 위의 코드와 같이 <span class="mediumblue">ThemeContext.Provider</span> 에서 감싸는 모든 하위 컴포넌트에서는 우리가 <span class="forestgreen">value</span> 에 넣어준 <u>isDark</u> 와 <u>setIsDark</u> 를 사용할 수 있게 된다.

```jsx
// Page.jsx
import Content from "./Content";
import Footer from "./Footer";
import Header from "./Header";

export default function Page() {
  return (
    <div className="Page">
      <Header />
      <Content />
      <Footer />
    </div>
  );
}
```

위의 Page 컴포넌트는 App 컴포넌트에서 선언된 state(isDark) 를 실질적으로 사용하지 않고 그 자식 컴포넌트들에게 내려주는 역할만을 하는 컴포넌트였다. 그래서 Page 컴포넌트는 App 컴포넌트의 state 의 존재를 몰라도 되므로 위의 코드와 같이 정리해줄 수 있는 것이다.

```jsx
// Header.jsx
import React, { useContext } from 'react';

import ThemeContext from '../context/ThemeContext';

export default function Header() {
  const { isDark } = useContext(ThemeContext);

  return (
    <header
      className="Page"
      style={ {
        backgroundColor: isDark ? "black" : "lightgray",
        color: isDark ? "white" : "black",
      } }
    >
      <h1>Welcome 홍길동!</h1>
    </header>
  );
}
```

위의 컴포넌트에서는 <span class="mediumblue">useContext(ThemeContext);</span> 를 사용하여 ThemeContext 에서 value 를 가져와 사용하게 된다. 만약 <u>App 컴포넌트에서 ThemeContext.Provider 를 사용하지 않았다면</u> Context 컴포넌트에서 선언한 <span class="forestgreen">초기값인 null</span> 이 사용된다.

```jsx
// Content.jsx
import React, { useContext } from 'react';

import ThemeContext from '../context/ThemeContext';

export default function Content() {
  const { isDark } = useContext(ThemeContext);

  return (
    <div
      className="content"
      style={ {
        backgroundColor: isDark ? "black" : "white",
        color: isDark ? "white" : "black",
      } }
    >
      <p>좋은 하루 되세요</p>
    </div>
  );
}
```

```jsx
// Footer.jsx
import React, { useContext } from 'react';

import ThemeContext from '../context/ThemeContext';

export default function Footer() {
  const { isDark, setIsDark } = useContext(ThemeContext);

  function toggleTheme() {
    setIsDark(!isDark);
  }

  return (
    <footer
      className="footer"
      style={ {
        backgroundColor: isDark ? "black" : "lightgray",
      } }
    >
      <button className="button" onClick={toggleTheme}>
        Dark Mode
      </button>
    </footer>
  );
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
 -->
