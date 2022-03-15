---
layout: single
title: "Styled Component"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [스타일링] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Global Style & ThemeProvider

`CreateGlobalStyle`과 `ThemeProvider`를 사용하면 전역으로 사용할  
요소들을 쉽게 정의할 수 있다.

```java
import { createGlobalStyle } from 'styled-components';
import reset from 'styled-reset';

const GlobalStyle = createGlobalStyle`
  ${reset}

	// 전역스타일

`;

export default GlobalStyle;
```

```java
import React from "react";
import ReactDOM from "react-dom";
import GlobalStyle from './styles/GlobalStyle';
import { ThemeProvider } from "styled-components";
import Router from "./Router";
import theme from "./styles/theme";

ReactDOM.render(
	<>
    <GlobalStyle />
    <ThemeProvider theme={theme}>
      <Router />
    </ThemeProvider>
	</>,
  document.getElementById("root")
);
```

```java
// theme.js

const theme = {
  background: "#FFFEFC",
  white: "#FFFFFF",
  vermilion: "#ff7425",
  orange: "#FF9900",
  opacityOrange: "rgba(242,153,74,0.5)",
  yellow: "#FFD66C",
  grey: "rgba(196,196,196,0.3)",
  middleGrey: "rgba(65,65,65,0.4)",
  deepGrey: "#828282",
  lightOrange: "rgba(255,195,170,0.3)",
  fontColor: "#2D2B2B",
  fontTitle: "'Alata', sans-serif;",
  fontContent: "'Noto Sans KR', sans-serif;",
};

export default theme;
```

```java
// theme 사용

const Container = styled.div`
  background-color: ${props => props.theme.background}
`;
```

# styled component?

javascript에서 css를 사용할 수 있도록 도와주는 스타일링 프레임워크이다.

## 특징

### component 단위 스타일링

styled components로 생성된 components들을 빌드하면 <u>임의의 클래스명에</u>  
<u>스타일이 적용되어 있는 것</u>을 확인할 수 있다.  
styled components는 `중복되지 않는 특정 class명을 생성`해  
스타일을 적용한다.

### 조건부 스타일링

```java
import React from 'react';
import styled from 'styled-components';

function Items() {
  const StyledDiv = styled.div`
    background-color: black;
    width: 100px;
    height: 100px;
    ${({ login }) => {
      return login ? `display: none` : null;
    }}
  `;

  return (
    <>
      <div>Items</div>
      <StyledDiv login={false}>hello</StyledDiv>
    </>
  );
}

export default Items;

```

styled-components는 `component의 props를 전달받아 사용`하는 것이  
가능하다.  
템플릿 리터럴 내에서 javascript를 사용하는 것과 같은 형식이며,  
내부에서 선언된 함수는 props를 파라미터로 실행된다.

### 확장 스타일링

```java
const Container = styled.div`
    max-width: 600px;
    width: 100%;
    height: 100px;
  `;

  const BlackContainer = styled(Container)`
    background-color: black;
  `;

  const RedContainer = styled(Container)`
    background-color: red;
  `;

  return (
    <>
      <BlackContainer />
      <RedContainer />
    </>
  );
```

styled components는 새로운 component를 선언하는 것 뿐만 아니라  
`기존의 component에 스타일을 추가하는 것도 가능`하다.  
확장 스타일링을 사용하면 <u>중복된 코드 양을 줄이고</u>, <u>분산된 스타일을</u>  
<u>일관적으로 관리할 수 있어 유지보수 비용을 줄일 수</u> 있다.

```java
const MyLink = styled(Link)`
    color: black;
    text-decoration: none;
  `;

  return (
    <Router>
      <MyLink to="/main"> 커스텀 링크 </MyLink>
    </Router>
  );
```

기존 component에 스타일을 추가할 수 있는 기능 덕분에,  
`서드 파티 component와도 호환`이 가능하다.  
예를 들어, 자주 사용하는 React-router-dom의 Link component의  
경우에는 위와 같은 방버으로 스타일을 적용해 사용할 수 있다.

### 중첩 스코프

```java
const StyledDiv = styled.div`
    background-color: black;
    width: 100px;
    height: 100px;
    p {
      color: white;
    }
  `;

  return (
    <>
      <StyledDiv>
        <p>Title</p>
      </StyledDiv>
      <p>content</p>
    </>
  );
```

`SASS의 중첩 스코프` 규칙을 사용할 수 있다.  
덕분에 내부의 모든 component를 styled-components로 생성하지 않아도,  
하위 컴포넌트에게만 적용하고 싶은 스타일을 스코프 형태로 구현할 수 있다.  
(그러나, 모든 SASS 문법이 사용가능하진 않음!)

### 테마 기능

```java
export const lightTheme = {
  background: "#fff",
};

export const darkTheme = {
  background: "#111"
};
```

```java
import { ThemeProvider } from "styled-components";
import { lightTheme, darkTheme } from "./theme.js";

<ThemeProvider theme={userMode ? darkTheme : lightTheme}>
 ...
</ThemeProvider>
```

<u>ThemeProvider 기능</u>을 이용하여 현재 웹의 <u>스타일 테마를 지정</u>할 수 있다.  
React의 경우 ThemeProvider의 하위 컴포넌트들은 <u>props로</u>  
<u>theme을 받으며</u> -> props.theme을 통해 유저가 원하는 웹의 테마를  
지정하게 된다.

# styled component의 활용

```java
import React from 'react';
import styled from 'styled-components';

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: black;
  border-radius: 50%;
`;

function App() {
  return <Circle />;
}

export default App;
```

<img src="https://user-images.githubusercontent.com/87808288/158277951-7e4d6541-7c70-4b04-8224-ffe7e4a50ab6.png" width="300" height="200">  
<u>styled component</u>를 사용하면 -> <u>스타일을 입력함과 동시에</u> 해당 스타일을  
가진 `component를 만들 수` 있다!  
&nbsp; div를 스타일링하고 싶다면 -> styled.div를  
&nbsp; iput을 스타일링하고 싶다면 -> styled.input 으로 사용할 수 있다.

## Circle 컴포넌트에 props를 넘기기

```java
import React from 'react';
import styled from 'styled-components';

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: ${props => props.color || 'black'};
  border-radius: 50%;
`;

function App() {
  return <Circle color="blue" />;
}

export default App;
```

<img src="https://user-images.githubusercontent.com/87808288/158278755-7a9ff449-dd72-40c0-a07b-a227c42bea22.png" width="300" height="200">  
Circle 컴포넌트에서 <u>color props 값을 설정했다면</u> `해당 값으로 배경색`을  
설정하고 <u>그렇지 않다면 검정색으로 배경색</u>을 사용하도록 설정했다.

### 여러 개의 props 넘기기

```java
import React from 'react';
import styled, { css } from 'styled-components';

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: ${props => props.color || 'black'};
  border-radius: 50%;
  ${props =>
    props.huge &&
    css`
      width: 10rem;
      height: 10rem;
    `}
`;

function App() {
  return <Circle color="red" huge />;
}

export default App;
```

<u>여러 줄의 CSS 코드를 조건부로</u> 보여줄 때는 `css를 사용`해야한다.  
&nbsp; css를 불러서 사용해야 스타일 내부에서도 다른 props를 조회할 수 있다.

## 버튼 만들기

```java
//components/ Button.js
import React from 'react';
import styled from 'styled-components';

const StyledButton = styled.button`
  /* 공통 스타일 */
  display: inline-flex;
  outline: none;
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  /* 크기 */
  height: 2.25rem;
  font-size: 1rem;

  /* 색상 */
  background: #228be6;
  &:hover {
    background: #339af0;
  }
  &:active {
    background: #1c7ed6;
  }

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;

function Button({ children, ...rest }) {
  return <StyledButton {...rest}>{children}</StyledButton>;
}

export default Button;
```

```java
//App.js
import React from 'react';
import styled from 'styled-components';
import Button from './components/Button';

const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid black;
  padding: 1rem;
`;

function App() {
  return (
    <AppBlock>
      <Button>BUTTON</Button>
    </AppBlock>
  );
}

export default App;
```

<img src="https://user-images.githubusercontent.com/87808288/158280228-e6aaff07-512e-47a1-9317-e8a043dee353.png" width="300" height="200">

<!-- 메소드 위에 변수 선언, 메소드 안에 메소드, 메소드 끝나고 리턴 -->

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
