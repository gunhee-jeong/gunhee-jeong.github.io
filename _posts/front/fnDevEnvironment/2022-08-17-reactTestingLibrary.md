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

(DaleSeo) : [React Testing Library 사용법](https://www.daleseo.com/react-testing-library/)  

# 1장 소개
`React Testing Library`는 <span class="tomato">행위 주도 테스트</span> 방법론이 주목받으며 함께 성장한 라이브러리이다.  
이는 행위 주도는 기존의 <u>구현 주도 테스트(Implementation Driven Test)의 단점을 보완</u>하기 위한 방법론이다.  

```html
<h2 class="title">제목</h2>
```

기존의 <span class="blue">구현 주도</span>에서는 위의 html에서 <u>h2라는 태그가 사용</u>되었고  
<u>title이라는 class가 사용되었는지 여부</u> 등을 테스트하였다.  
그런데 실질적으로 사용자는 h2 태그의 사용과 title이라는 클래스 네임의 존재도 모르고 <span class="tomato">관심도 없다</span>.  
따라서 현재 사용자에게 <span class="red">어떤 컨텐츠가 보이고</span>,  
사용자가 어떤 이벤트를 발생시켰을 때의 <span class="red">화면 변화 등을 테스트</span>하는 것을 초점을 맞추고 있다.  

# 2장 주요 API
React Testing Library에는 크기 DOM에 컴포넌트를 렌더링해주는 `render() 함수`와  
특정 이벤트를 발생시켜주는 `fireEvent 객체`, 그리고 DOM에서 특정 영역을 선택하기 위한 다양한 `쿼리 함수`가 존재한다.  

`render() 함수`는 React Testing Library에서 제공하는 모든 쿼리 함수와  
기타 유틸리티 함수를 담고 있는 <span class="blue">객체를 반환</span>하게 된다.  
따라서 자바스크립트의 문법인 <span class="royalblue">Destructuring 문법</span>을 사용하여  
render 함수가 리턴한 객체로부터 <u>원하는 쿼리 함수를</u> 얻을 수 있다.  

```jsx
import { render, fireEvent } from "@testing-library/react";

const { getByText, getByLabelText, getByPlaceholderText } = render(
  <YourComponent />
);
```

## 1. Queries
### (1) 정적 컴포넌트 테스팅
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
화면에서 검색할 <u>Page Not Found</u>를 인수로 넘기고 이를 담고 있는 태그는 <span class="blue">h2 엘리먼트를 얻게</span> 된다.  
마지막으로 <span class="tomato">jest-dom</span>의 <span class="red">toBeInTheDocument()</span> matcher 함수를 이용하여  
해당 &lt;h2&gt; 태그가 화면에 존재하는지 검증하게 된다.  

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
