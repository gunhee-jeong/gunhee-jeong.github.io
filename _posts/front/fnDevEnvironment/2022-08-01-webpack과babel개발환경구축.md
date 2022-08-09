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
# 1장 개발환경 구축
## 1. Node.js
<span class="red">Node.js</span>는 <span class="blue">Chrome V8 JavaScript Engine</span>으로 빌드된 <span class="blue">JavaScript Runtime Enviroment</span>이다.  

### (1) Node.js 설치
(Node.js 다운로드) : <https://nodejs.org/ko/>  

<span class="royalblue">LTS(Long Term Supported)</span> 버전은 장기적으로 안정적인 지원을 보장하므로 LTS 버전을 선택했다.  
정상적으로 설치했다면 아래와 같은 결과를 확인할 수 있다.  

```bash
node -v # Node.js version 확인
> 12.17.0
```

## 2. NPM 프로젝트 만들기
### (1) NPM?
(NPM 공식문서) : <https://docs.npmjs.com/about-npm>  
(NPM의 이해) : [김정환님 블로그](https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html)  

<span class="red">NPM(Node Package Manager)</span>은 <span class="blue">Node.js에서 사용할 수 있는 모듈</span>들을 <span class="royalblue">패키지화하여 모아둔 저장소</span> 역할과  
<span class="royalblue">패키치 설치 및 관리를 위한 CLI(Command Line Interface)를 제공</span>한다.  

NPM 프로젝트를 생성하여 package.json을 생성하기 위해서는 아래의 2가지의 명령어가 있다.  

```bash
npm init # 설정을 직접

npm init -y # 개별 설정 없이 package.json 생성
```

### (2) NPM 의존성 추가 및 webpack 설치
```bash
npm install <name>
# 또는
npm i <name>
```

<span class="tomato">devDependencies</span> 에는 <span class="blue">개발 시에만 사용하는 개발용 의존 패키지를 기록</span>한다.  
예를 들어 Eslint는 개발 단계에서만 필요로하고 실제 사용자가 쓰는 제품에서는 필요하지 않다.  
그래서 devDependencies 에만 Eslint를 포함시키게 된다.  
<span class="darkorange">npm install</span> 명령어에 <span class="darkorange">--save-dev</span>(축약형-D) 옵션을 사용하면  
패키지 설치와 함께 <span class="royalblue">package.json</span>의 <span class="blue">devDenpendencies 에 설치된 패키지와 버전이 기록</span>된다.  

```bash
npm i --save-dev
# 또는
npm i -D
```

우리는 <span class="blue">webpack 까지 설치</span>해야하므로 <span class="royalblue">아래와 같이 작성</span>한다.  

```bash
 npm i -D webpack webpack-cli webpack-dev-server
```

위의 명령어를 이용하여 설치하고 나면  
아래의 이미지와 같이 <span class="blue">package.json</span>에 <span class="tomato">devDependencies가 생성</span>되고  
그 안에 webpack이 들어가 있는 것을 볼 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/183345012-1bc2cc35-348f-41b2-a8ba-883064cd67d9.png" width="55%">  

### (3) eslint 추가
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

## 3. 개발용 서버 실행방법
기존의 webpack을 이용하여 서버를 여는 방법은 "webpack-dev-server"였지만  
이것이 변경되어 현재는 아래의 명령어가 되었다.  

```bash
webpack serve --mode development
```

그리고 webpack.config.js에 mode 옵션이 없을 경우 에러가 발생하므로 아래와 같이 config 파일을 설정해야한다.  

```js
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        use: 'babel-loader',
      },
    ],
  },
};

```

<img src="https://user-images.githubusercontent.com/87808288/183346122-71f52957-01cc-4c50-9c47-248b6d7b02a5.png" width="30%">  
그리고 public 폴더 내에 존재하는 <span class="blue">index.html</span> 내부에 <span class="tomato">main.js를 연결</span>해주어야 한다.  

```html
<!-- index.js -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Demo</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="main.js"></script>
  </body>
</html>
```

## 4. babel 설정
### (1) babel 설치
```bash
npm i -D babel-loader # webpack에서 babel을 사용할 수 있도록 도와준다.(webpack에서 babel을 사용할 준비를 한다.)
npm i -D @babel/core # 
npm i -D @babel/preset-env @babel/preset-react
```

```js
// babel config 설정
module.exports = {
  presets: [
    [
      '@babel/preset-env',
      {
        targets: {
          node: 'current',
        },
      },
    ],
    '@babel/preset-react',
  ],
};
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
