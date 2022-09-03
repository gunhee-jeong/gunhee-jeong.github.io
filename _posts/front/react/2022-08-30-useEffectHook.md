---
layout: single
title: "useEffect Hook"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [useEffect, hook, setInterval, clearInterval] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-08-30T14:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.crimson {
  color: crimson;
  font-weight: bold;
}

.royalblue {
  color: royalblue;
  font-weight: bold;
}

.olive {
  color: olive;
  font-weight: bold;
}

.forestgreen {
  color: foresgreen;
  font-weight: bold;
}
</style>

# useEffect Hook
(React 공식문서) : [Using the Effeck Hook](https://ko.reactjs.org/docs/hooks-effect.html)

# 1장 학습목표
- `useEffect` 훅을 활용해 다양한 <u>side effect(부수효과)</u>를 일으킬 수 있다.
- React에서 일어나는 <span class="crimson">UI Rendering</span>과 <span class="crimson">Side Effect</span>의 차이를 구분하여 설명할 수 있다.
- `useEffect Hook`을 활용해 원하는 타이밍(<span class="olive">의존성 배열</span>)에 Side Effect를 일으킬 수 있으며, 이 과정에서 일어나는 컴포넌트 랜더링 과정을 설명할 수 있다.

useEffect 훅을 이해하는 데 있어 가장 중요한 것은<span class="royalblue">발생 시점</span>이다. 컴포넌트가 화면에 올라가고 내려가고 훅은 업데이트 되는 과정 속에서 <u>어느 시점에 useEffect 훅이 발생하는지</u> 정확하게 파악할 수 있어야한다.

# 2장 Side Effect

## 1. What is?
React에서 함수 컴포넌트의 `rendering` 이란 <u>state, props를 기반으로 UI 요소를</u> 그려내는 행위이다. <span class="olive">rendering 결과물에 영향을 주는 요소</span>는 <span class="royalblue">state</span>와 <span class="royalblue">props</span>이다.

## 2. Side Effect
부작용, 부수 효과라고도 부른다. 일상 생활에서는 부정적인 의미로 사용되지만, 프로그래밍 측면에서는 단순히 부정적인 의미로만 사용하지 않는다. <span class="royalblue">외부 변수의 개입</span>이 있다면 `side effect`이다.

```jsx
let count = 0

function greetWithSideEffect(name) { // Input
  count = count + 1 // Side Effect!

  return `${name}님 안녕하세요!` // Output
}
```

이 함수는 <u>함수 외부 세계에 count라는 변수를 조작</u>한다. 이는 <span class="crimson">함수의 결과값 이외의 다른 상태를 변경시키는 행위</span>에 해당하고 <span class="royalblue">Side Effect가 있다</span>고 할 수 있다. react의 함수 컴포넌트에서의 Side Effect는, rendering이 아니고 <span class="olive">외부 세계에 영향을 주는 어떠한 행위</span>이다. 대표적으로 <u>Data Fetching, DOM에 직접 접근, 구독</u>과 같은 행위들이 있다.

# 3장 useEffect
<u>함수 컴포넌트</u>의 <span class="olive">리턴 값은 UI 요소</span>라고 했고, <span class="royalblue">state와 props의 변화가 있을 때마다 함수가 실행</span>된다. 이 말은 <u>매 Rendering 때마다 함수 body에 있는 로직이 실행</u>된다는 의미이다. 그리고 <span class="royalblue">rendering과 무관한 로직이 rendering 과정에서 실행</span>되기 때문에 rendering 자체에 영향을 줘 <span class="crimson">성능에 악영향</span>을 끼칠 수 있다. 그래서 react에서는 이런 <u>side effect를 일으키기 위한 장소</u>로 `useEffect hook`을 제공한다.

```jsx
function greetWithSideEffect({ name }) { //
  // Bad!
  document.title = `${name}님 안녕하세요!`; // Side Effect

  return <div>{`${name}님 안녕하세요!`}</div>; // Output
}
```

react 공식문서에도 <span class="crimson">useEffect</span>를 "React의 순수한 함수적인 세계에서 <u>명령적인 세계로의 탈출구</u>로 생각하세요"라고 설명하고 있다. 여기서 <span class="olive">'순수한 세계' = rendering(input -> output)</span>을 뜻하고, <span class="royalblue">rendering 이외에 일으켜야 하는 Side Effect</span>를 일으킬 탈출구로 <span class="crimson">useEffect</span>를 사용하라는 의미를 가진다.

useEffect는 <u>Side Effect</u>를 `rendering 이후에 발생`시킨다.(예외: useLayoutEffect) useEffect가 <u>수행되는 시점에 이미 DOM이 업데이트 되었음을 보장</u>한다는 뜻이고, 바뀌 말하면 `Side Effect가 rendering에 영향을 주지 않도록 설계`되었음을 의미한다.

```jsx
import { useEffect } from 'react';

function greetWithSideEffect({ name }) { // Input
  useEffect(() => {
    // Good!
    document.title = `${name}님 안녕하세요!`; // Side Effect
  }, [name]);

  return <div>{`${name}님 안녕하세요!`}</div>; // Output
}
```

만약 Side Effect 이후 업데이트 된 정보가 있어 새롭게 화면이 그려져야 할 경우 (state, props의 업데이트) 새롭게 rendering을 일으킨다. 함수 컴포넌트는 최신 state와 props를 반영한 화면을 리턴하게 된다. `effect를 일으킬 타이밍`은 앞서 설명했던 <u>useEffect의 두 번째 argumnet</u>인 <span style="color:red">의존성 배열(Dependancy Array)</span>를 통해 표현하게 된다.

## 1. Rendering Cycle with useEffect
useEffect는 다음과 같은 형태로 사용된다.

```jsx
import { useEffect } from "react"

// 사용법
useEffect( 실행시킬 동작, [ 타이밍 ] )
document.addEventListener("타이밍", 실행시킬 동작) // 추상화 한 예시

//1번
// 매 렌더링마다 Side Effect가 실행되어야 하는 경우
useEffect(() => {
  // Side Effect
})

//2번
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

### (1) 렌더링 될 때마다 실행
<span class="royalblue">컴포넌트가 렌더링될 때마다</span> 매번 call function이 실행된다. 컴포넌트가 <span class="olive">처음 화면에 렌더링될 때</span> 그리고 <span class="olive">다시 컴포넌트가 렌더링될 때 실행된다.

### (2) 컴포넌트가 처음 화면에 렌더링될 때, 배열 안의 엘리먼트의 값이 바뀔 때 실행
<u>만약 빈 배열이라면</u> 화면에 <span class="crimson">처음 rendering될 때만</span> 실행된다.

## 2. useEffect를 사용하여 버튼만들기

```jsx
//App component
function App() {
  const [count, setCount] = useState(1);
  const [name, setName] = useState("");

  const handleCountUpdate = () => {
    setCount(count + 1);
    // console.log(`rendering 했어요! 🍎`);
  };

  const handleInput = (e) => {
    setName(e.target.value);
  };

  useEffect(() => {
    console.log(`rendering 헀어요! 🌈`);
  });

  useEffect(() => {
    console.log(`rendering 했어요! 🍎`);
  }, [name]);

  useEffect(() => {
    console.log(`rendering 했어요! ⭐️`);
  }, []);

  return (
    <div>
      <button onClick={handleCountUpdate}>Update</button> //버튼
      <span>Count: {count}</span>
      <input onChange={handleInput} type="text" /> //이름을 입력하는 input
      <span>name: {name}</span>
    </div>
  );
}
```

<span style="color:green">useEffect(() => {console.log(\`rendering 했어요! 🍎\`);}, [name])</span>  
이렇게 <span style="color:red">빈 array에 name</span>이 들어가면 -> useState를 통해 `name의 state가`  
`변화하면` useEffect가 실행!  
&nbsp; useState를 통해 name이 변하는 경우는 input에 onChange 이벤트가 발생하는 경우이다.

<span style="color:green">useEffect(() => {console.log(`rendering 헀어요! 🌈`);});</span>  
이렇게 useEffect에 <u>두번째 argument가 존재하지 않는다면</u> <span style="color:red">모든 state의 상태가 변경될 때마다  
rendering</span>된다.

<span style="color:green">useEffect(() => {console.log(`rendering 했어요! ⭐️`);}, []);</span>  
이렇게 빈 배열로 useEffect를 이용하면 <u>맨처음 한 번만 rendering</u>되고 난 이후에는,  
rendering되지 않는다.

## cleanUp을 이용한 버튼 만들기

```java
//App.js
const App = () => {
  const [showTimer, setShowTimer] = useState(false);

  return (
    <div>
      <button onClick={() => setShowTimer(!showTimer)}>Toggle Timer</button>
      {showTimer && <Timer />}
    </div>
  );
};

//Timer.js
const Timer = () => {
  useEffect(() => {
    const timer = setInterval(() => {
      console.log(`타이머 실행중...`);
    }, 1000);

    return () => {
      clearInterval(timer);
      console.log(`타이머가 종료되었습니다.`);
    };
  }, []);

  return (
    <div>
      <span>타이머를 시작</span>
    </div>
  );
};

```

### App.js

<u>'Toggle Timer'라는 버튼</u>과 이 버튼을 누르면 -> <u>'타이머 실행중...'이라는 span 태그</u>가  
toggle되도록 만든다.

<span style="color:green">const [showTimer, setShowTimer] = useState(false);</span>  
&nbsp; 버튼을 누르면 `<Timer />`가 <u>나왔다 사라졌다</u>를 반복하면서  
&nbsp; <span style="color:red">상태가 계속해서 변하므로</span> 이를 `state`를 사용해 value를 담았다.

<span style="color:green"><button onClick={() => setShowTimer(!showTimer)}>Toggle Timer</button></span>  
&nbsp; <u>버튼을 누르는 이벤트가 감지</u>되면 -> `setShowTimer가 실행`되면서  
&nbsp; showTimer의 state를 <span style="color:red">boolean 타입의 value</span>로 바꾸게된다.  
&nbsp; showTimer의 값이 <u>false일 때 버튼</u>을 누르면 -> <span style="color:red">'!showTimer'</span>는  
&nbsp; ture가 되므로 showTimer의 값은 `ture`가 되고  
&nbsp; showTimer의 값이 <u>ture일 때 버튼</u>을 누르면 -> <span style="color:red">'!showTimer'</span>는  
&nbsp; false가 되므로 showTimer의 값에는 `false`가 할당되게 된다.

<span style="color:green">{showTimer && <Timer />}</span>  
&nbsp; useState를 통해 showTimer의 값이 false일 경우에는 화면에 보이지 않지만,  
&nbsp; <u>showTimer의 값이 ture</u>일 경우에는 `ture && ture` 이므로 <u>화면에 노출</u>된다!

### Timer.js

위에서 App.js에서 버튼을 눌렀을 때 showTimer의 값이 ture일 경우에는  
`<Timer />`가 노출되도록 설정했다.  
그리고 `<Timer />`는 <u>화면에 처음 노출</u>되었을 때 -> <span style="color:red">1초 단위로 setInterval()를 실행</span>하고,  
버튼을 다시 눌러 <u>showTimer의 값이 false가 되어 화면에서 사라지면</u>  
<span style="color:red">setInterval()를 종료</span>하도록 설정해야한다.

useEffet를 사용하면서 2번째 argument에 [] 이렇게 빈 array를 사용하면서  
화면에 처음 rendering되었을 때만 최초로 useEffect가 실행된다.  
<span style="color:green">setInterval(() => {console.log(`타이머 실행중...`);}, 1000);</span>  
&nbsp; <u>setInterval()</u>은 1초 단위로 반복하여 코드블록을 실행하고 이는 <u>화면에서 사라져도 계속</u>된다.  
&nbsp; <u>그래서 setInterval()을 종료하도록</u>, useEffect의 return에 `clearInterval()`를 사용한다.  
&nbsp;

<!-- ① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨-->

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
