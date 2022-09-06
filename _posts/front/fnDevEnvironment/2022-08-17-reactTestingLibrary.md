---
layout: single
title: "React-Testing-Library"
# categories: Git
categories:
  - feDevEnvironment # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [jest] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-08-16T23:00:00+09:00
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
</style>

# React-Testing-Library
(DaleSeo) : [React Testing Library 사용법](https://www.daleseo.com/react-testing-library/)  
(npm Now Packing Magic) : [@testing-library/jest-dom](https://www.npmjs.com/package/@testing-library/jest-dom)  

## 1장 소개
`React Testing Library`는 <u>행위 주도 테스트</u> 방법론이 주목받으며 함께 성장한 라이브러리이다. 이는 행위 주도는 기존의 <span class="teal">구현 주도 테스트(Implementation Driven Test)의 단점을 보완</span>하기 위한 방법론이다.

```html
<h2 class="title">제목</h2>
```

기존의 구현 주도에서는 위의 html에서 <u>h2라는 태그가 사용</u>되었고 <u>title이라는 class가 사용되었는지 여부</u> 등을 테스트하였다. 그런데 실질적으로 사용자는 h2 태그의 사용과 title이라는 클래스 네임의 존재도 모르고 <u>관심도 없다</u>. 따라서 현재 사용자에게 <span class="crimson">어떤 컨텐츠가 보이고</span>, 사용자가 어떤 이벤트를 발생시켰을 때의 <span class="crimson">화면 변화 등을 테스트</span>하는 것을 초점을 맞추고 있다.

### 1. @testing-library/jest-dom
@testing-library/jest-dom은 jest의 matcher들을 확장하여 테스트의 의도를 명확하게 표현할 수 있다.  

### 2. fireEvent
테스팅에서 DOM 이벤트를 편리하게 발생시켜주는 메서드이다.  
click, change 등의 이벤트를 발생시킬 수 있다.  

## 2장 주요 API
React Testing Library에는 DOM에 컴포넌트를 렌더링해주는 render() 함수와 특정 이벤트를 발생시켜주는 fireEvent 객체, 그리고 DOM에서 특정 영역을 선택하기 위한 다양한 쿼리 함수가 존재한다.

<span class="crimson">render() 함수</span>는 React Testing Library에서 제공하는 <u>모든 쿼리 함수</u>와 <u>기타 유틸리티 함수</u>를 담고 있는 <span class="mediumblue">객체를 반환</span>하게 된다. 따라서 자바스크립트의 문법인 <span class="teal">Destructuring 문법</span>을 사용하여 render 함수가 리턴한 객체로부터 원하는 쿼리 함수를 얻을 수 있다. 그리고 렌더링 된 DOM 요소(container)를 반환한다.

```jsx
import { render } from '@testing-library/react';

const Button = () => (
  <button>Click Me!</button>
);

const { getByText, container } = render(<Button />);
```

### 1. Query
렌더링 된 DOM 노드에 접근하여 엘리먼트를 가져오는 메서드이다. 예시로 <u>getAllByRole 메서드</u>를 살펴보자면, get(<span class="teal">쿼리 타입</span>) -> All(<span class="teal">타켓의 개수</span>) -> ByRole(<span class="teal">타겟 유형</span>)으로 세션을 나눌 수 있다.

#### (1) 쿼리 타입
- get: 동기적으로 처리되며 타겟을 찾지 못하면 에러를 발생
- find: 비동기적으로 처리되며 타겟을 칮지 못하면 에러를 발생
- query: 동기적으로 처리되며 타겟을 찾지 못하면 null을 반환

#### (2) 타겟의 개수
<u>다수의 엘리먼트가 탐색</u>되는 상황에서는 All을 사용하여 탐색할 수 있다.

#### (3) 타겟 유형
##### [ByRole]
공식문서에서 <span class="teal">getByRole</span>을 권장한다고 해서 테스트를 위해 <u>role을 선언하지 않아도 된다</u>. 기본적으로 <span class="mediumblue">몇몇 HTMl 시맨틱 태그는 이미 implict role을 가지고</span> 있기 때문이다. 해당 role과 <span class="teal">두 번째 인자로 들어가는 옵션 객체</span>를 통해 찾고자 하는 <u>타입을 좀더 명확하게</u> 할 수 있다. 만약 implict role을 파악하기 어렵다면 아래의 이미지의 방법으로 사용 가능한 role을 제안받을 수도 있다.

```jsx
// Counter.js
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const decrement = () => setCount(count - 1);

  const increment = () => setCount(count + 1);

  return (
    <>
      <div>{count}</div>
      <button onClick={decrement}>-</button>
      <button onClick={increment}>+</button>
    </>
  );
};

export default Counter;
```

```jsx
import { render, screen } from '@testing-library/react';

import Counter from './Counter';

describe('Counter test', () => {
  it('should render Counter', () => {
    render(<Counter />);

    // 두 쿼리 모두 같은 element 탐색(문자열 대신 정규식 탐색도 가능)
    screen.getByRole('button', { name: '+' });
    screen.getByText('+');
  });
});
```

<img src="https://user-images.githubusercontent.com/87808288/187027970-7f8f5004-abe5-4633-91bf-809adab49613.png" width="90%">

- ByLabelText
- ByPlaceholderText
- ByText
- ByDisplayValue
- ByAltText
- ByTitle
- ByTestId

### 2. 정적 컴포넌트 테스팅 실습
```jsx
// NotFound.js
import React from "react";

function NotFound({ path }) {
  return (
    <>
      <h2>Page Not Found</h2>
      <p>해당 페이지({path})를 찾을 수 없습니다.</p>
      <img
        alt="404"
        src="https://media.giphy.com/media/14uQ3cOFteDaU/giphy.gif"
      />
    </>
  );
}
```

위의 `NotFound 컴포넌트`는 기본적으로 <u>정적인 텍스트와 이미지로만 구성</u>되어 있다.  
아래는 NotFound 컴포넌트 검증을 위한 NotFound.test.js이다.  

```jsx
// NotFound.test.js
import React from "react";
import { render } from "@testing-library/react";
import NotFound from "./NotFound";

describe("<NotFound />", () => {
  it("renders header", () => {
    const { getByText } = render(<NotFound path="/abc" />);
    const header = getByText("Page Not Found");
    expect(header).toBeInTheDocument();
  });
});
```

render 함수에서 얻은 `getByText`는  
화면에서 검색할 <u>Page Not Found</u>를 인수로 넘기고 이를 담고 있는 태그는 <span class="olive">h2 엘리먼트를 얻게</span> 된다.  
마지막으로 <span class="darkorange">jest-dom</span>의 <span class="crimson">toBeInTheDocument()</span> matcher 함수를 이용하여  
해당 &lt;h2&gt; 태그가 화면에 존재하는지 검증하게 된다.  

### 3. 동적 컴포넌트 테스팅 실습
```jsx
// LoginForm.js
import React, { useState } from "react";

function LoginForm({ onSubmit }) {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  return (
    <>
      <h2>Login</h2>
      <form onSubmit={onSubmit}>
        <label>
          이메일
          <input
            type="email"
            placeholder="user@test.com"
            value={email}
            onChange={({ target: { value } }) => setEmail(value)}
          />
        </label>
        <label>
          비밀번호
          <input
            type="password"
            value={password}
            onChange={({ target: { value } }) => setPassword(value)}
          />
        </label>
        <button disabled={!email || !password}>로그인</button>
      </form>
    </>
  );
}
```

위의 `LoginForm 컴포넌트`는 이메일과 비밀번호 입력란과 버튼으로 구성된 <span class="royalblue">로그인 폼</span>, 컴포넌트이다.  

```jsx
// LoginForm.test.js
import React from "react";
import { render, fireEvent } from "@testing-library/react";
import LoginForm from "./LoginForm";

describe("<LoginForm />", () => {
  it("enables button when both email and password are entered", () => {
    const { getByText, getByLabelText } = render(
      <LoginForm onSubmit={() => null} />
    );

    const button = getByText("로그인");
    const email = getByLabelText("이메일");
    const password = getByLabelText("비밀번호");

    expect(button).toBeDisabled();

    fireEvent.change(email, { target: { value: "user@test.com" } });
    fireEvent.change(password, { target: { value: "Test1234" } });

    expect(button).toBeEnabled();
  });
});
```

`로그인 버튼`은 <span class="olive">getByText()</span> 쿼리 함수를 통해 선택가능하고  
`이메일과 비밀번호 입력칸`은 <span class="olive">getByLabelText()</span> 쿼리 함수로 선택 가능하다.  

그리고 <span class="darkorange">jest-dom</span>의 <span class="crimson">toBeDisabled</span>()와 <span class="crimson">toBeEnabled</span>() matcher 함수를 통해  
로그인 <span class="olive">버튼의 활성화 여부</span>를 이벤트 발생 전후로 검증하게 된다.  

# 3장 jest-dom
(github) : [testing-library/ jest-dom](https://github.com/testing-library/jest-dom#tohavetextcontent)

## 1. Custom matchers
### toHaveTextContent
toHaveTextContent를 통해 <u>주어진 노드</u>에 <span class="teal">text content가 있는지</span> 확인할 수 있다. 이것은 요소뿐만 아니라 텍스트 노드와 fragment도 지원한다.

문자열 인수가 전달되면 노드 내용과 부분적으로 대소문자를 구분하는 일치를 수행한다.

```html
<span data-testid="text-content">Text Content</span>
```

```jsx
const element = getByTestId('text-content')

expect(element).toHaveTextContent('Content')
expect(element).toHaveTextContent(/^Text Content$/) // to match the whole content
expect(element).toHaveTextContent(/content$/i) // to use case-insensitive match
expect(element).not.toHaveTextContent('content')
```

<!-- ⓵ ⓶ ⓷ ⓸ ⓹ ⓺ ⓻ ⓼ ⓽ ⓾ -->

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
</div>
</details> -->
