---
layout: single
title: "리액트 Testing(Jest)"
# categories: Git
categories:
  - feDevEnvironment # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [TDD] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-08-15T16:00:00+09:00
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
우리가 <span class="blue">무언가를 수정했을 때 다른 컴포넌트들이 올바르게 동작하는지</span> 손으로 직접 테스트하는 것은 많이 시간이 소요된다.  
이 모든 것을 <span class="tomato">컴퓨터가 자동으로 아주 빠르게 확인</span>해주면 어떨까에서 시작한 것이 바로 <span class="red">TDD</span>이다.  

# 1장 Jest
<span class="red">Jest</span>는 <span class="blue">자바스크립트 테스팅 프레임워크</span>이다.  

- 간단한 설정으로 테스트를 실행할 수 있다.  
- 풍부한 matcher를 제공하여 별도의 모듈 없이 테스트를 풍부하게 표현할 수 있다.  
- Coverage도 별도의 설치없이 확인할 수 있다.
- Mocking 등을 지원하여 테스트를 더 쉽게 가능하게 해주는 프레임워크이다.

## 1. 설치
### (1) Jest 설치
```bash
npm i -D jest babel-jest
```

```bash
npm i -D @types/jest
```

`@types/jest`는 <span class="blue">Jest의 타입 정의를 가지고 있는 모듈</span>이다.  
TypeScript에서 주로 사용되지만 이 모듈을 설치하면 <span class="royalblue">편집기 내에서 자동완성을 지원</span>하기 때문에 설치하는 것이 좋다.  

### (2) 파일 설정
```jsx
// eslintrc.js
module.exports = {
  env: {
    browser: true,
    es2021: true,
    jest: true, // 이 부분을 추가함
  },
  extends: [
    'plugin:react/recommended',
    'airbnb',
  ],
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 12,
    sourceType: 'module',
  },
  plugins: [
    'react',
  ],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
    actor: 'readonly',
    Feature: 'readonly',
    Scenario: 'readonly',
    context: 'readonly',
  },
  rules: {
    indent: ['error', 2],
    'no-trailing-spaces': 'error',
    curly: 'error',
    'brace-style': 'error',
    'no-multi-spaces': 'error',
    'space-infix-ops': 'error',
    'space-unary-ops': 'error',
    'no-whitespace-before-property': 'error',
    'func-call-spacing': 'error',
    'space-before-blocks': 'error',
    'keyword-spacing': ['error', { before: true, after: true }],
    'comma-spacing': ['error', { before: false, after: true }],
    'comma-style': ['error', 'last'],
    'comma-dangle': ['error', 'always-multiline'],
    'space-in-parens': ['error', 'never'],
    'block-spacing': 'error',
    'array-bracket-spacing': ['error', 'never'],
    'object-curly-spacing': ['error', 'always'],
    'key-spacing': ['error', { mode: 'strict' }],
    'arrow-spacing': ['error', { before: true, after: true }],
    'jsx-a11y/label-has-associated-control': ['error', { assert: 'either' }],
    'linebreak-style': 'off',

    'react/prop-types': 'off',
    'react/react-in-jsx-scope': 'off',
  },
};
```

```jsx
// jest.setup.js
import '@testing-library/jest-dom';
```

```jsx
// jest.config.js
module.exports = {
  setupFilesAfterEnv: [
    'jest-plugin-context/setup',
    './jest.setup',
  ],
  coverageThreshold: {
    global: {
      branches: 100,
      functions: 100,
      lines: 100,
      statements: 100,
    },
  },
};
```

### (3) 실행
```bash
npx jest
```

이렇게 위의 명령어를 실행하면 jest를 실행해 볼 수 있다.  
또한 jest를 그때그때 실행하는 방법이 아닌 자동으로 하기 위해서는 아래의 명령어를 사용할 수 있다.  

```bash
npx jest --watchAll
```

## 2. Assertion
<span class="red">단정문</span>이라고 부르는 `Assertion`은 우리가 <span class="blue">기대하는 값이 실제 값이랑 일치하는지 확인</span>하게 된다.  

```jsx
// simple.test.js
test('simple', () => { // 첫 번째 인자는 실행할 테스트의 이름이다.
  // assertion => A(actual)가 B(expect)여야 한다.
  expect(1 + 1).toBe(2);
});
```

## 3. Signature
모든 연산은 연산의 이름, 매개변수, 반환값을 명세한다. 이를 시그니처라고 한다.  

# 2장 TDD 테스트 주도 개발
<span class="red">테스트 주도 개발</span>은 <span class="tomato">테스트가 개발을 주도</span>하는 방법이다.  
테스트가 개발을 주도한다는 것은 <span class="blue">테스트가 코딩의 방향을 이끌어</span> 간다는 말이다.  
테스트가 실패하는 코드가 없으면 코딩을 하지 않고,  
코드상에 중복이 있으면 제거한다는 간단한 규칙을 지켜나가면 자연스레 아름다운 코드가 펼쳐진다.  

## 1. 왜 TDD를 해야 하는가
(테스트 자동화와 Mocha) : [JAVASCRPT.INFO](https://ko.javascript.info/testing-mocha#ref-1068)  

### (1) 테스트는 왜 해야 하는가?
함수 하나를 만들고 있다고 가정하고,  
개발 중엔 <u>콘솔 창 등을 사용</u>하여  
실제 실행 결과가 기대했던 결과와 같은지 비교하면서 원하는 기능이 잘 구현되고 있는지 확인하게 될 것이다.  
그런데 이렇게 <span class="blue">수동으로 "재실행"</span>한다는 것은 <span class="tomato">상당히 불완전</span>하다.  
그리고 코드를 수동으로 재실행하면서 테스트를 한다면 <span class="blue">무언가를 놓치기도 쉽다</span>.  

개발자는 무언가를 만들 때 머릿속에 <span class="blue">수많은 유스 케이스를 생각하며 코드를 작성</span>하는데  
코드를 변경할 때마다 <span class="red">모든 케이스를 생각하며 코드를 수정하는 것은 거의 불가능하다</span>고 할 수 있다.  
하나를 고치면 또 다른 문제가 튀어나오는 것이 바로 이러한 이유이다.  
<span class="red">테스팅 자동화</span>는 테스트 코드가 <span class="tomato">실제 동작에 관여하는 코드와 별개로 작성되었을 때 가능</span>하게 된다.  


## 2. 2가지 간단한 룰
1. 먼저 자동화된 테스트에서 실패하지 않는 한 새로운 코드를 작성하지 않는다.
2. 중복을 제거한다.  

<img src="https://user-images.githubusercontent.com/87808288/184624552-60cec687-4910-490f-bfdb-69d67eb9f62b.png" width="60%">  
TDD에서는 처음에는 통과하지 못할`(RED) 테스트`를 작성하고  
이 테스트를 통과하게끔`(Green) 코드`를 작성하고,  
결과 코드를 `최대한 깔끔하게 리팩터링` 하는 짧은 주기로 반복한다.  

### (1) RED
```jsx
// Item.test.jsx
test('add', () => {
  expect(add(1, 2)).toBe(3);
});
```

add 함수는 아직 <span class="tomato">구현된 코드가 없기에 당연히 테스트에서 실패</span>하게 된다.  
여기서 주의할 점은 <span class="blue">아직 add 함수를 선언하지 않은 점</span>이다.  
<span class="red">테스팅 프레임워크의 에러 메시지를 먼저 확인하는 게 가장 중요</span>하다.  

그러면 이제 아래의 에러 메시지를 만나게 된다.  

```bash
ReferenceError: add is not defined
```

이제 <span class="blue">add 함수를 선언할 때</span>이다.  
<span class="royalblue">절대 스텝을 건너 뛰고 진행하면 안된다</span>.  

```jsx
// Item.test.jsx
function add() {
}

test('add', () => {
  expect(add(1, 3)).toBe(4);
});
```

그러면 아래와 같이 실패하게 된다.  
<span class="royalblue">왜냐하면 add 함수에 내용이 존재하지 않기 때문</span>이다.  

```bash
expect(received).toBe(expected) // Object.is equality

Expected: 4
Received: undefined
```

### (2) Green
<span class="red">Green</span>에서 수단과 방법을 가리지 않고 <span class="blue">가장 빠르게 테스트를 통과시키는 방법</span>은 아래와 같다.  

```jsx
// Item.test.jsx
function add() {
  return 4;
}

test('add', () => {
  expect(add(1, 3)).toBe(4);
});
```

말도 안된다고 생각할 수 있지만 <span class="tomato">TDD에서는 이것은 올바른 방법</span>이다.  

### (3) Refactor
이제 중복을 몰아낼 차례이다.  

```jsx
// Item.test.jsx
function add() {
  return 1 + 3;
}
```

위의 코드에서는 입력값이 바뀔 때마다 return을 계속 수정해주어야 한다.  
이런 중복을 몰아내기 위해 아래와 같이 수정할 수 있다.  

```jsx
// Item.test.jsx
function add(x, y) {
  return x + y;
}
```

위의 코드와 같은 방법으로 중복을 몰아낼 수 있다.  
TDD에서 핵심은 Refactoring 단계이다.  
우리에겐 테스트 코드가 있으니 마음에 들 때까지 얼마든지 코드를 수정해도 문제가 생기지 않는다.  
이 부분에서 Kent Beck이 말한 TDD가 두려움을 조절하는 기술임을 확실하게 느낄 수 있다.  

## 3. BDD 방법론
(테스트 자동화와 Mocha) : [JAVASCRPT.INFO](https://ko.javascript.info/testing-mocha#ref-1068)  

Behavior Driven Development라 불리는 방법론에 대해 알아보자.  
이 방법론은 <u>test</u>, <u>documentation</u>, <u>example</u>를 한데 모아놓은 개념이다.  
### (1) 예시: 거듭제곱 함수와 명세서
x를 n번 곱해주는 함수인 pow(x, n)을 구현하고 있다고 가정해보자.  
(사실 JS에는 거듭제곱 연산자, **가 이미 존재하지만 BDD에 관한 설명을 위해 함수로 만든다.)  

코드를 작성하기 전에 먼저 <span class="royalblue">코드가 무슨 일을 하는지</span> 이를 자연어로 표현해야한다.  
이때 만들어진 산출물을 BDD에선 <span class="royalblue">명세서(specification)</span> 또는 <span class="royalblue">스펙(spec)</span>이라고 부른다.  
명세서에는 아래와 같이 유스 케이스에 대한 자세한 설명과 테스트가 담겨있다.  

```jsx
describe("pow", function() {

  it("주어진 숫자의 n 제곱", function() {
    assert.equal(pow(2, 3), 8);
  });

});
```

`스펙`은 <span class="blue">세 가지 주요 구성 요소</span>로 이루어진다.  
⓵ <span class="forestgreen">describe</span>("title", function() { ... })  
<u>구현하고자 하는 기능에 대한 설명</u>이 들어간다.  

⓶ <span class="forestgreen">it</span>("유스 케이스 설명", function() { ... })  
<span class="tomato">it</span>의 <u>첫 번째 인수</u>엔 <span class="blue">특정 유스 케이스에 대한 설명</span>이 들어간다.  
이 설명은 <span class="blue">누구나 읽을 수 있고 이해할 수 있는 자연어로</span> 적게된다.  
두 번째 인수엔 유스 케이스 테스트 함수가 들어간다.  

⓷ <span class="forestgreen">assert.equal</span>(value1, value2)  
기능을 제대로 구현했다면 it 블록 내의 코드 <span class="darkorange">assert.equal(value1, value2)</span> 이 <u>에러 없이 실행</u>된다.  

### (2) 스펙 실행하기
#### [라이브러리 설명]
- Mocha: 핵심 테스트 프레임워크로, describe it과 같은 테스팅 함수와 테스트 실행 관련 주요 함수 제공
- Chai: 다양한 assertion을 제공해 주는 라이브러리(assert.equal)
- Sinon: 함수의 정보를 캐내는 데 사용하는 라이브러리로, 내장 함수 등을 모방한다.  

# 3장 React testing library
리액트 테스팅 라이브러리는 사용자와 동일한 방식으로 DOM 쿼리를 사용할 수 있게 도와준다.  
실제 사용자가 앱을 사용하는 방식으로 테스트하여 우리의 앱이 올바르게 동작하는지 테스트할 수 있다.  

## 1. 설치
```bash
npm i -D @testing-library/react @testing-library/jest-dom
```

### (1) @testing-library/jest-dom
@testing-library/jest-dom은 jest의 matcher들을 확장하여 테스트의 의도를 명확하게 표현할 수 있다.  

### (2) fireEvent
테스팅에서 DOM 이벤트를 편리하게 발생시켜주는 메서드이다.  
click, change 등의 이벤트를 발생시킬 수 있다.  

### (3) Mocking
mocking은 일부 기능을 테스트할 때 의존 관계를 끊고 독립적으로 테스트할 수 있게 한다.  
`jest.fn()`을 통해서 <span class="blue">함수를 mocking</span> 할 수도 있다.  
Jest에서 제공하는 다양한 mocking 방법이 있다.  


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
