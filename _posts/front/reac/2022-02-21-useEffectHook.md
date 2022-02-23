---
layout: single
title: "useEffect Hook"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [useEffect, hook, sideEffect] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

웹 사이트를 만들다 보면 화면에 보일 수 있는 데이터를 서버에서 받아오기도 해야 하고,  
'state'가 바뀔 때마다 함수를 실행 시키거나, 이벤트 리스너를 달았다가 해제하는 등의  
동작이 필요할 수 있다. -> 이때 useEffect Hook이 필요로하다!

# 학습목표

- `useEffect` 훅을 활용해 다양한 <u>side effect(부수효과)</u>를 일으킬 수 있다.
- React에서 일어나는 <span style="color:red">UI Rendering</span>과 <span style="color:red">Side Effect</span>의 차이를 구분하여 설명할 수 있다.
- `useEffect Hook`을 활용해 원하는 타이밍(<span style="color:red">의존성 배열</span>)에 Side Effect를 일으킬 수 있으며,  
   이 과정에서 일어나는 컴포넌트 랜더링 과정을 설명할 수 있다.

useEffect 훅을 이해하는 데 있어 가장 중요한 것은`발생 시점`이다.  
&nbsp; 컴포넌트가 화면에 올라가고 내려가고 훅은 업데이트 되는 과정 속에서  
&nbsp; <u>어느 시점에 useEffect 훅이 발생하는지</u> 정확하게 파악할 수 있어야한다.

# Side Effect

## What is?

### Rendering in React

React에서 함수 컴포넌트의 `rendering` 이란 <u>state, props를 기반으로 UI 요소를</u>  
그려내는 행위이다.
&nbsp; rendering 결과물에 영향을 주는 요소는 <u>state</u>와 <u>props</u>이다.

### Side Effect

<span style="color:red">부작용, 부수 효과</span>라고도 부른다.  
일상 생활에서는 부정적인 의미로 사용되지만,  
프로그래밍 측면에서는 단순히 부정적인 의미로만 사용하지 않는다.  
`외부 변수의 개입이 있다면 side effect`이다.

```java
let count = 0

function greetWithSideEffect(name) { // Input
  count = count + 1 // Side Effect!

  return `${name}님 안녕하세요!` // Output
}
```

이 함수는 <u>함수 외부 세계에 count라는 변수를 조작</u>한다.  
이는 `함수의 결과값 이외의 다른 상태를 변경시키는 행위`에 해당 ->  
Side Effect가 있다고 할 수 있다.  
&nbsp; react의 함수 컴포넌트에서의 <u>Side Effect</u>는, rendering이 아니고  
&nbsp; <span style="color:red">외부 세계에 영향을 주는 어떠한 행위</span>이다.  
&nbsp; 대표적으로 <u>Data Fetching, DOM에 직접 접근, 구독</u>과 같은 행위들이 있다.

# useEffect

<u>함수 컴포넌트</u>의 `리턴 값은 UI 요소`라고 했고, <span style="color:red">state와 props의 변화가 있을 때마다  
함수가 실행</span>된다. -> 이 말은 <u>매 Rendering</u> 때마다  
<u>함수 body에 있는 로직이 실행</u>된다는 의미이다.

그리고 <u>rendering과 무관한 로직</u>이 `rendering 과정에서 실행`되기 때문에 rendering 자체에  
영향을 줘 <span style="color:red">성능에 악영향</span>을 끼칠 수 있다.  
그래서 react에서는 이런 <u>side effect를 일으키기 위한 장소</u>로 `useEffect hook`을 제공!

```java
function greetWithSideEffect({ name }) { //
  // Bad!
  document.title = `${name}님 안녕하세요!`; // Side Effect

  return <div>{`${name}님 안녕하세요!`}</div>; // Output
}
```

react 공식문서에도 <span style="color:red">useEffect</span>를 "React의 순수한 함수적인 세계에서  
`명령적인 세계로의 탈출구`로 생각하세요"라고 설명하고 있다.  
&nbsp; 여기서 <u>'순수한 세계' = rendering(input -> output)</u>을 뜻하고,  
&nbsp; `rendering 이외에 일으켜야 하는 Side Effect`를 일으킬 탈출구로  
&nbsp; <span style="color:red">useEffect</span>를 사용하라는 의미를 가진다.

useEffect는 <u>Side Effect</u>를 `rendering 이후에 발생`시킨다.(예외: useLayoutEffect)  
useEffect가 <u>수행되는 시점에 이미 DOM이 업데이트 되었음을 보장</u>한다는 뜻이고,  
바뀌 말하면 `Side Effect가 rendering에 영향을 주지 않도록 설계`되었음을 의미한다.

```java
import { useEffect } from 'react';

function greetWithSideEffect({ name }) { // Input
  useEffect(() => {
    // Good!
    document.title = `${name}님 안녕하세요!`; // Side Effect
  }, [name]);

  return <div>{`${name}님 안녕하세요!`}</div>; // Output
}
```

만약 Side Effect 이후 업데이트 된 정보가 있어 새롭게 화면이 그려져야 할 경우  
(state, props의 업데이트) 새롭게 rendering을 일으킨다.  
함수 컴포넌트는 최신 state와 props를 반영한 화면을 리턴하게 된다.  
`effect를 일으킬 타이밍`은 앞서 설명했던 <u>useEffect의 두 번째 argumnet</u>인  
<span style="color:red">의존성 배열(Dependancy Array)</span>를 통해 표현하게 된다.

## Rendering Cycle with useEffect

useEffect는 다음과 같은 형태로 사용된다.

```java
import { useEffect } from "react"

// 사용법
useEffect( 실행시킬 동작, [ 타이밍 ] )
document.addEventListener("타이밍", 실행시킬 동작) // 추상화 한 예시

// 매 렌더링마다 Side Effect가 실행되어야 하는 경우
useEffect(() => {
  // Side Effect
})

// Side Effect가 첫 번째 렌더링 이후 한번 실행 되고,
// 이후 특정 값의 업데이트를 감지했을 때마다 실행되어야 하는 경우
useEffect(() => {
  // Side Effect
}, [value])

// Side Effect가 첫 번째 렌더링 이후 한번 실행 되고,
// 이후 어떤 값의 업데이트도 감지하지 않도록 해야 하는 경우
useEffect(() => {
  // Side Effect
}, [])
```

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
