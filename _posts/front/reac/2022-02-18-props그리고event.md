---
layout: single
title: "Props & Event"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [props] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Props

props는 `properties`(속성)를 의미한다. 이는 단어의 뜻 그대로 <span style='color:red'>컴포넌트의 속성값</span>이다.

props는 `부모 컴포넌트로부터 전달 받은 데이터를` 지니고 있는 <span style="color:red">객체</span>이다.  
&nbsp; 사람이 태어나 <u>이름을 부여받을 때 부모로부터 이름을 받듯</u>이  
&nbsp; `부모 컴포넌트`로부터 전달받은 <span style="color:red">객체 타입</span>의 데이터를 <span style='color:red'>props</span>라고 말한다.

props를 이용해 어떤 자바스크립트 값이든 <u>모두 자식 컴포넌트에 전달할 수</u> 있다.

App.js에서 Counter component을 사용하고 있는데

```java
//App.js
function App() {
  return (
    <div className="App">
      <MyHeader />
      <Counter />
    </div>
  );
}
```

Counter component는 아래의 모습을 하고 있다.

```java
//Counter component
const Counter = () => {
  const [count, setCount] = useState(0);

  const onIncrese = () => {
    setCount(count + 1);
  };

  const onDecrese = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h2>{count}</h2> //버튼의 초기값을 const count의 0으로 지정함
      <button onClick={onIncrese}>+</button> //+버튼을 누르면 onIncrese 실행
      <button onClick={onDecrese}>-</button> //-버튼을 누르면 onDecrese 실행
    </div>
  );
};
```

그런데 우리가 초기값으로 지정한 `<h2>{count}</h2>`을 Counter component의  
<span style="color:red">Parent component</span>인 <u>App component에서</u> 받아올 수 있다.

```java
//App.js
function App() {
  return (
    <div className="App">
      <MyHeader />
      <Counter a={1} b={2} c={3} d={4} e={5}/> //Parent에서 child로 props 전달
    </div>
  );
}

//Counter component
const Counter = (props) => { //Parent에서 props를 받고
  const [count, setCount] = useState(0);
  console.log(props); //output == {a: 1, b: 2, c: 3, d: 4, e: 5}
```

Parent component에서 위와 같은 방법으로 <u>Child인 Counter에게 속성을 전달</u>하고  
`Child component에서는 props를` 사용해 이를 <span style="color:red">object</span>로 받아올 수 있다.

```java
//parent component
import React from "react";
import Child from "./Child/Child";

const Parent = () => {
  return (
    <>
      <h1>Parent Component</h1>
      <Child text="기 화이팅" / number={30}>
    </>
  );
};

export default Parent;

```

`Parent 컴포넌트` 안에 있는 <u>Child 컴포넌트의 attribute인 text에 30기 화이팅'</u>라는  
`데이터를` 넣었고, 자식 컴포넌트인 <span style="color:red">Child에서 props</span>를 사용해 console.log로 찍어보면  
<u>'30기 화이팅'가 아닌</u> <span style="color:red">object</span>로 출력된다!  
왜냐하면 <span style="color:red">prop</span>는 `부모 컴포넌트로부터 전달받은 객체 타입의 데이터`이기 때문이다.

```java
//child component
import React from "react";

const Child = (props) => {
  console.log(props); //{text: '기 화이팅', number: 30}
  return <p>Child!</p>;
};

export default Child;

```

여기서 console.log가 아닌 view에서 '30기 화이팅'로 보이게 하기 위해서는  
아래와 같은 방법으로 view를 직접 변경시킬 수 있다.

```java
import React from "react";

const Child = (props) => {
  console.log(props);
  return (
    <p>
      {props.number}
      {props.text}
    </p>
  );
};

export default Child;
```

아니면 아래와 같이 parent 컴포넌트 안에서, <u>변수를 할당</u>할 수도 있다.

```java
//parent component
import React from "react";
import Child from "./Child/Child";

const Parent = () => {
  const thirty = 30;
  return (
    <>
      <h1>Parent Component</h1>
      <Child text="기 화이팅" number={thirty}>
    </>
  );
};

export default Parent;

//child component
import React from "react";

const Child = (props) => {
  console.log(props);
  return (
    <p>
      {props.number}
      {props.text}
    </p>
  );
};

export default Child;
```

만약 부모 컴포넌트로부터 'red'라는 데이터를 전달받아 -> 자식 컴포넌트의 color를  
red로 변경하고자 한다면 아래와 같이 코드를 만들 수 있다.

```java
//parent component
import React from "react";
import Child from "./Child/Child";

const Parent = () => {
  const thirty = 30;
  return (
    <>
      <h1>Parent Component</h1>
      <Child text="기 화이팅" number={thirty} color="red">
    </>
  );
};

export default Parent;

//child component
import React from "react";

const Child = (props) => {
  console.log(props);
  return (
    <p style={ { color: props.color } }>
      {props.number}
      {props.text}
    </p>
  );
};

export default Child;
```

Parent component에서 Child component에게 color='red'를 -> props를 통해  
object 데이터로 물려주었고 -> Child Component에서는 p태그의 인라인 style을 주는  
방법으로 Child Component의 color를 변경할 수 있다.  
&nbsp; <span style="color:green"><p style={ { color: props.color } }></span>에서 `porps.color`를 사용하여  
&nbsp; <u>Parent component에서 전달받은 데이터를 사용</u>할 수 있다.

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
