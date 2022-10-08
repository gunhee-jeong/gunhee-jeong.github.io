---
layout: single
title: "webpack과 bable 개발환경 구축"
# categories: Git
categories:
  - feDevEnvironment # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [코드숨] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-08-01T17:00:00+09:00
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

# webpack과 bable 개발환경 구축

# 🔴 개발환경 구축

## 🟠 Node.js

(Node.js 공식문서) : <https://nodejs.org/ko/about/>

`Node.js`는 <u>Chrome V8 JavaScript Engine</u>으로 빌드된 JavaScript Runtime Enviroment 이다.

### 🟡 Node.js 설치

(Node.js 다운로드) : <https://nodejs.org/ko/>

<span class="mediumblue">LTS(Long Term Supported)</span> 버전은 장기적으로 안정적인 지원을 보장하므로 LTS 버전을 선택했다. 정상적으로 설치했다면 아래와 같은 결과를 확인할 수 있다.

```bash
node -v # Node.js version 확인
> 12.17.0
```

## 🟠 NPM 프로젝트 만들기

### 🟡 NPM?

(NPM 공식문서) : <https://docs.npmjs.com/about-npm>  
(NPM의 이해) : [김정환님 블로그](https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html)

`NPM(Node Package Manager)`은 <u>Node.js에서 사용할 수 있는 모듈</u>들을 패키지화하여 모아둔 저장소 역할과 <u>패키치 설치 및 관리를 위한 CLI(Command Line Interface)를 제공</u>한다.

<u>NPM 프로젝트</u>를 생성하여 <span class="mediumblue">package.json</span>을 생성하기 위해서는 아래의 2가지의 명령어가 있다.

```bash
npm init # 설정을 직접

npm init -y # 개별 설정 없이 package.json 생성
```

### 🟡 NPM 의존성 추가 및 webpack 설치

(npm Docs) : [package.json](https://docs.npmjs.com/cli/v8/configuring-npm/package-json)

```bash
npm install <name>
# 또는
npm i <name>
```

<span class="crimson">devDependencies</span> 에는 <u>개발 시에만 사용하는 개발용 의존 패키지를 기록</u>한다. 예를 들어 <span class="forestgreen">Eslint는 개발 단계에서만 필요</span>로하고 실제 사용자가 쓰는 제품에서는 필요하지 않다. 그래서 <u>devDependencies 에만 Eslint를 포함</u>시키게 된다. npm instal 명령어에 <u><span class="mediumblue">--save-dev</span>(축약형-D)</u> 옵션을 사용하면 패키지 설치와 함께 <span class="royalblue">package.json</span>의 devDenpendencies 에 설치된 패키지와 버전이 기록된다.

```bash
npm i --save-dev
# 또는
npm i -D
```

우리는 <span class="blue">webpack 까지 설치</span>해야하므로 <span class="royalblue">아래와 같이 작성</span>한다.

```bash
 npm i -D webpack webpack-cli webpack-dev-server
```

위의 명령어를 이용하여 설치하고 나면 아래의 이미지와 같이 `package.json`에 <span class="mediumblue">devDependencies가 생성</span>되고 그 안에 webpack이 들어가 있는 것을 볼 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/183345012-1bc2cc35-348f-41b2-a8ba-883064cd67d9.png" width="55%">

## 🟠 리액트 및 폴더 설정

```bash
npm install react react-dom
```

### 🟡 package.json

```json
{
  // ......
  },
  "scripts": {
    "start": "webpack serve --mode development" // 이 부분을 추가
  },
// ......
}
```

### 🟡 public

#### 🟢 index.html

<details>
<summary class="black">클릭해서 index.html 코드 보기</summary>
<div markdown="1">

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Demo</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="/main.js"></script>
  </body>
</html>
```

</div>
</details>

### 🟡 src

#### 🟢 index.jsx

<details>
<summary class="black">코드</summary>
<div markdown="1">

```jsx
// helloWorld!
const hello = "hi";
```

</div>
</details>

## 🟠 eslint

```bash
npm i -D eslint
```

<img src="https://user-images.githubusercontent.com/87808288/183356419-4dbccf15-da11-484a-86d8-3e4e24290307.png" width="55%">

그리고 eslint의 사용에 관한 설명을 위해 아래의 명령어를 입력한다.

```bash
npx eslint --init
```

<img src="https://user-images.githubusercontent.com/87808288/183357118-2cace5ff-4098-42e6-960e-7e5b75ee054a.png" width="60%">  
명령어 이후 설정을 선택해야하는데  
To check syntax,  find problems, and enforce code style ->  
JavaScript modules(import/ export) ->  
React ->  
TypeScript 사용 여부 등으로 이루어진다.  
<img src="https://user-images.githubusercontent.com/87808288/183358099-c511ca6a-418d-4c74-a8e1-ef346614787d.png" width="60%">

이렇게 설정 후, 자동으로 eslint를 이용해 코드를 수정하기 위해서는 아래의 명령어를 이용할 수 있다.

```bash
npx eslint --fix .
```

### 🟡 eslintrc.js

<details>
<summary class="black">클릭해서 eslintrc.js 코드 보기</summary>
<div markdown="1">

```jsx
module.exports = {
  env: {
    browser: true,
    es2021: true,
    jest: true,
  },
  extends: ["plugin:react/recommended", "airbnb"],
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 12,
    sourceType: "module",
  },
  plugins: ["react"],
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly",
    actor: "readonly",
    Feature: "readonly",
    Scenario: "readonly",
    context: "readonly", // context 사용시 설정
    given: "readonly", // given 사용시 설정
  },
  rules: {
    indent: ["error", 2],
    "no-trailing-spaces": "error",
    curly: "error",
    "brace-style": "error",
    "no-multi-spaces": "error",
    "space-infix-ops": "error",
    "space-unary-ops": "error",
    "no-whitespace-before-property": "error",
    "func-call-spacing": "error",
    "space-before-blocks": "error",
    "keyword-spacing": ["error", { before: true, after: true }],
    "comma-spacing": ["error", { before: false, after: true }],
    "comma-style": ["error", "last"],
    "comma-dangle": ["error", "always-multiline"],
    "space-in-parens": ["error", "never"],
    "block-spacing": "error",
    "array-bracket-spacing": ["error", "never"],
    "object-curly-spacing": ["error", "always"],
    "key-spacing": ["error", { mode: "strict" }],
    "arrow-spacing": ["error", { before: true, after: true }],
    "jsx-a11y/label-has-associated-control": ["error", { assert: "either" }],
    "linebreak-style": "off",

    "react/prop-types": "off",
    "react/react-in-jsx-scope": "off",
  },
};
```

</div>
</details>

## 3. 개발용 서버 실행방법

기존의 webpack을 이용하여 서버를 여는 방법은 "webpack-dev-server"였지만  
이것이 변경되어 현재는 아래의 명령어가 되었다.

```bash
npx webpack serve --mode development

# 또는

npm start
```

그리고 webpack.config.js에 mode 옵션이 없을 경우 에러가 발생하므로 아래와 같이 config 파일을 설정해야한다.

<details>
<summary class="black">클릭해서 webpack.config.js 코드 보기</summary>
<div markdown="1">

```jsx
// webpack.config.js
const path = require("path");

module.exports = {
  entry: path.resolve(__dirname, "src/index.jsx"),
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        use: "babel-loader",
      },
    ],
  },
  resolve: {
    extensions: [".js", ".jsx"],
  },
  devServer: {
    historyApiFallback: {
      index: "index.html",
    },
  },
};
```

</div>
</details>

<img src="https://user-images.githubusercontent.com/87808288/183346122-71f52957-01cc-4c50-9c47-248b6d7b02a5.png" width="30%">

그리고 public 폴더 내에 존재하는 <span class="blue">index.html</span> 내부에 <span class="tomato">main.js를 연결</span>해주어야 한다. 코드는 아래와 같다.

<details>
<summary class="black">클릭해서 index.html 코드 보기</summary>
<div markdown="1">

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Demo</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="/main.js"></script>
  </body>
</html>
```

</div>
</details>

## 4. babel 설정

### (1) babel 설치

```bash
npm i -D babel-loader # webpack에서 babel을 사용할 수 있도록 도와준다.(webpack에서 babel을 사용할 준비를 한다.)
npm i -D @babel/core #
npm i -D @babel/preset-env @babel/preset-react
```

<details>
<summary class="black">클릭해서 babel.config.js 코드 보기</summary>
<div markdown="1">

```jsx
// babel.config.js
module.exports = {
  presets: [
    [
      "@babel/preset-env",
      {
        targets: {
          node: "current",
        },
      },
    ],
    "@babel/preset-react",
  ],
  plugins: [
    [
      "@babel/plugin-transform-react-jsx",
      {
        runtime: "automatic",
      },
    ],
  ],
};
```

</div>
</details>

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
