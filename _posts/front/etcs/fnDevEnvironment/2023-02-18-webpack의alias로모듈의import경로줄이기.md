---
layout: single
title: "Webpack의 alias로 모듈의 import 경로 줄이기(feat. 테스트 코드에도 적용하는 방법)"
# categories: Git
categories:
  - feDevEnvironment # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [웹팩, 바벨, Jest] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2023-02-18
last_modified_at: 2023-02-18
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

✏️ 글의 목적: 모듈을 import 하는 경로를, 변수를 만들어 단축하거나 가독성 있게 표현하고자 하는 분들에게 정보를 제공하기 위해 글을 작성한다. 또한 테스트 코드(Jest)에서도 alias를 사용한 코드가 통과되도록 설정값을 만들어야 하는데 다른 분들에게 도움이 되었으면 한다.

이번에 진행하고 있는 개인 프로젝트를 리팩터링 하면서 _컴포넌트의 구조를 한눈에 보이게_ 하기 위해서 아래와 같이 **디렉터리들을 더 추가하여** 구조를 만들고 있었다.

```bash
🗂 src
  ├── 🗂 Header
  ├── 🗂 Footer
  ⎪	├── 🗂 FooterTopContainer
  ⎪	⎪   ├── FooterTopList.jsx
  ⎪	⎪   └── FooterTopList.test.jsx
  ⎪	├── 🗂 FooterBottomLayout
  ⎪	├── FooterPage.jsx
  ⎪	└── FooterPage.test.jsx
  └── 🗂 styles
```

그러다 보니 위와 같이 `깊이가 깊어지기 시작`했다. FooterTopList.jsx에서 _styles 디렉터리에서_ import 하는 모듈을 가져오는 데에 **상대 경로**를 사용하다 보니 아래의 코드와 같이 조금 _지저분한 느낌이_ 들기 시작했다.

```jsx
// FooterTopList.jsx
import FOOTER_MENU_LIST from "../../../fixtures/Footer/footerMenuList";
```

이것을 참지 못하고? 방법들을 알아보다가 `Webpack의 alias`라는 객체를 추가하면, 내가 만들고 싶은 _절대 경로의 값을 변수에 넣어 지정할_ 수 있었다. 만약에 **/styles**라는 절대 경로를 **@fixtures**에 담으면 아래와 같이 최종적으로 리팩터링이 된다.

```jsx
// FooterTopList.jsx
import FOOTER_MENU_LIST from "@fixtures/Footer/footerMenuList";
```

나름 만족하는 결과인 것 같다. 그렇다면 본격적으로 어떻게 설정해야 하는지 하나씩 차근차근 알아보자.

# 📌 webpack.config.js

```jsx
// webpack.config.js
module.exports = () => {
  // ......
    resolve: {
      alias: {
        '@fixtures': path.resolve(__dirname, 'fixtures'),
      },
    },
  // ......
};
```

위의 설정 코드에서, `__dirname`은 **현재 파일이 위치한 디렉터리**를 나타낸다. webpack.config.js는 root에 위치 (_/webpack.config.js_) 하므로 **dirname은 /가 되는 것이다. path.resolve() 메서드는 인자로 전달된 경로들을 병합하여 절대 경로로 반환한다. \*\***dirname**과 똑같이 _root에 위치한_ **fixtures**를 병합하여 `/fixtures`라는 **절대 경로\*\*를 반환한다.

# 📌 Babel

Babel에서는 babel-plugin-module-resolver 플러그인을 사용하여 alias를 설정하게 된다. 먼저 아래와 같이 설치가 필요하다.

```bash
$ npm install --save-dev babel-plugin-module-resolver
```

## 📍 babel.config.js

```jsx
module.exports = {
  presets: [
    "@babel/preset-env",
     "@babel/preset-react"
  ],
  plugins: [
    "@babel/plugin-proposal-class-properties",
    "@babel/plugin-transform-runtime",
  ],
};
```

# 📌 Eslint

위의 설정을 마치면, 이제 @를 사용한 경로로 import가 정상적으로 진행되는 것을 확인할 수 있을 것이다. 그런데 이것과는 별개로 eslint에서는 에러를 나타내고 있다.

<img src="https://user-images.githubusercontent.com/87808288/219870252-80c28418-8089-4543-bba6-e28701625da4.png" width="50%">

eslint의 **import/no-unresolved** 규칙이 발생한 것이다. 이 규칙은 _경로가 정확한지_ 확인하고, _존재하는 모듈이 import 되었는지_ 확인한다.

## 📍 eslintrc.js

```javascript
// eslintrc.js
{
  "rules": {
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        "js": "never",
        "jsx": "never"
      }
    ]
  }
}
```

위의 설정을 살펴보면, **JavaScript 파일**이나 **JSX 파일**을 import 할 때, `확장자를 붙이지 않도록 설정`한 것이다. 이렇게 설정하고 저장하면 eslint의 에러가 사라지는 것을 확인할 수 있다.

# 📌 테스트 코드 에러

<img src="https://user-images.githubusercontent.com/87808288/219870260-41065399-1188-4832-8eba-d1550af1559e.png" width="60%">

npm start를 통해 살펴보면 import가 정상적으로 잘 붙었지만, 위의 이미지와 같이 테스트 코드에서는 아주 좋아하고 있다(부끄러운지 잔뜩 빨갛다🥹).

## 📍 jest.config.js

테스트 코드에서도 @fixtures 경로를 인식하려면, jest.config.js도 설정을 해주어야 한다.

```jsx
// jest.config.js
module.exports = {
  // ...
  moduleNameMapper: {
    "^@fixtures/(.*)$": "<rootDir>/fixtures/$1",
  },
};
```

위의 정규식은 ‘**@fixtures/**’ 기호로 시작하는 모듈 경로를 잡아내게 된다. 그렇게 잡아낸 모듈 경로를 '<rootDir>/fixtures/' 경로로 대응시켜준다.

# 📌 추가로 배운 것

기본적으로 웹팩과 바벨은 프로덕션 환경에서 코드를 번들링하고 모듈 로딩 등을 수행한다. 반면, Jest는 테스트 환경에서 코드 실행, 테스트 결과 확인 등의 기능을 수행한다. 따라서 Jest는 테스트를 위한 환경을 구성하는 것이 목적이다. 그래서 테스트를 위한 설정들을 추가로 설정해야 한다.

_Jest의 환경은 Node.js 기반으로_, 웹팩은 브라우저에서 동작하는 코드 번들링을 수행하고 Jest에서도 브라우저에서 동작하는 코드를 테스트하기 위하여 `jsDom`과 같은 브라우저 환경 모듈을 추가로 설정해 주어야 한다.

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
