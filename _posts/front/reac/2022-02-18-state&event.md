---
layout: single
title: "State & Event"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [state, event, props] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# State

- 단어의 뜻 그대로 컴포넌트 내부에서 가지고 있는 `컴포넌트의 상태값`을 의미한다.
- state는 화면에 보여줄 컴포넌트 UI 정보(상태)이다.
- state는 컴포넌트 내에서 정의하고 사용하며 <u>얼마든지 데이터가 변경</u>될 수 있다.

## state의 정의

### Function component: state

```java
//parent component
import React, { useState } from "react";
import Child from "./Child/Child";

const Parent = () => {
  const [color, setColor] = useState("red");
  return (
    <>
      <h1>Parent Component</h1>
      <Child text="기 화이팅" number={30} color={color} />
      <button>Click!</button>
    </>
  );
};

export default Parent;


```

<span style="color:green">useState('red')</span>는 함수를 호출하면서  
<u>argument로 'red'를 함수로 전달</u>하게된다.  
&nbsp; 그러면 <span style="color:green">const [color, setColor]</span>에 `구조분해할당`을 하면서  
&nbsp; 'red'라는 value를 <u>const color에 할당</u>하게된다.  
<span style="color:green"><Child text="기 화이팅" number={30} color={color} /></span>  
&nbsp; Parent component에서 `<child>`에게 데이터를 전달하게되는데  
&nbsp; 이때 color:<u>{color}에서 color는 이미 구조분해할당</u>을 거쳐 생성된 const color 라는  
&nbsp; `변수명 color`를 사용하게 된 것이다! -> 여기서 사용한 color는 JS를 통해 만들어진  
&nbsp; 것이기 때문에 <u>{}를 사용하여 구분</u>해주었다.

```java
//child component
import React from "react";

const Child = (props) => {
  console.log(`child component props ->`, props.color);
  return (
    <p style= { { color: props.color } }>
      {props.number}
      {props.text}
    </p>
  );
};

export default Child;
```

parent 컴포넌트에서, const color에 구조분해할당을 거쳤고,  
child 컴포넌트에서 이를 바탕으로 -> p태그 안에 inline style 방식으로  
<span style="color:green"><p style= { { color: props.color } }></span> 이렇게 코드를 작성할 수 있다.

이제 한 단계 더 나아가서, <u>button 태그를 누를 때마다 색이 전환</u>되도록 만들어보자.  
<u>switch가 눌러지는 것</u>을 `boolean 데이터로` 표현할 수 있으므로  
<span style="color:green">const [isSwitchOn, setSwitchOn] = useState(false);</span> 를 만들어주었다.

```java
//Parent component
import React, { useState } from "react";
import Child from "./Child/Child";

const Parent = () => {
  const [color, setColor] = useState("red");
  // console.log(color); //output == 'red'
  const [isSwitchOn, setSwitchOn] = useState(false);
  // console.log(`isSwitchOn ->`, { isSwitchOn }); //output == falsse -> true -> ...

  const toggleSwitch = () => {
    if (isSwitchOn === false) {
      setSwitchOn(true);
    } else {
      setSwitchOn(false);
    }
  };

  return (
    <>
      <h1>Parent Component</h1>
      <Child text="기 화이팅" number={30} color={color} />
      <button onClick={toggleSwitch}>Click!</button>
    </>
  );
};

export default Parent;
```

<span style="color:green"><button onClick={toggleSwitch}>Click!</button></span>  
&nbsp; 그리고 버튼이 눌리면 == <u>onClick 이벤트가 실행</u>되도록 하고 ->  
&nbsp; 결과적으로 onClick 이벤트가 실행되면서 `toggleSwitch 함수가 실행`된다.  
<span style="color:green">const toggleSwitch = () => {}</span>  
&nbsp; `toggleSwitch 함수`는, 버튼이 눌릴때 마다 -> <u>isSwitchOn의 value를 비교</u>한다.  
&nbsp; 그래서 <u>isSwitchOn의 value가 false</u>라면 -> <span style="color:red">setSwitchOn(true);</span> 을 실행하여  
&nbsp; isSwitchOn의 value가 true가 되도록 만들어준다!

그런데 여기서 **toggleSwitch**를 `code refactoring`을 통해 -> code를 정리하고  
<span style="color:red">가독성</span>을 올릴 수 있다.

```java
//Parent Component
//1차
const toggleSwitch = () => {
  if (isSwitchOn === false) {
    setSwitchOn(true);
  } else {
    setSwitchOn(false);
  }
};

//2차
const toggleSwitch = () => {
  setSwitchOn(isSwitchOn === false ? true : false);
};

//3차
const toggleSwitch = () => {
  setSwitchOn(!isSwitchOn);
};
```

<span style="color:green">setSwitchOn(isSwitchOn === false ? true : false);</span>  
&nbsp; 1차 toggleSwitch 함수를 살펴보면 <u>setSwitchOn(); 부분이 중복</u>되는 것을 알 수 있다.  
&nbsp; 중복되는 것은 <span style="color:red">중복을 없애는 방법으로 refactoring</span>을 할 수 있는데 ->  
&nbsp; `setSwitchOn()`의 argument로 true와 false 이렇게 두 개의 value가 번갈아 들어가기 때문에  
&nbsp; 이를 삼항연산자를 사용하여 <u>코드의 가독성을 개선</u>할 수 있었다.  
<span style="color:green">setSwitchOn(!isSwitchOn);</span>  
&nbsp; <u>isSwitchOn</u>에는 `boolean 타입`의 데이터로 value가 담기게 되는데 ->  
&nbsp; isSwitchOn의 값이 **false**라면, <span style="color:red">not 연산자</span>를 사용하여 `!isSwitchOn` -> <u>true라는 value</u>로!  
&nbsp; isSwitchOn의 값이 **true**라면, <span style="color:red">not 연산자</span>를 사용하여 `!isSwitchOn` -> <u>false라는 value</u>로  
&nbsp; 바꾸어 사용할 수 있다.

전체적으로 코드를 다시 한 번 설명하자면

```java
//Parent component
import React, { useState } from "react";
import Child from "./Child/Child";

const Parent = () => {
  const [color, setColor] = useState("red");
  // console.log(color); //output == 'red'
  const [isSwitchOn, setSwitchOn] = useState(false);
  // console.log(`isSwitchOn ->`, { isSwitchOn }); //output == falsse -> true -> ...
  const changeColor = () => {
    setColor("blue");
  };

  const toggleSwitch = () => {
    setSwitchOn(!isSwitchOn);
  };

  return (
    <>
      <h1>Parent Component</h1>
      <Child text="기 화이팅" number={30} color={color} />
      <button onClick={toggleSwitch}>Click!</button>
    </>
  );
};

export default Parent;
```

<span style="color:green">changeColor 함수</span>는  
&nbsp; **const color**의 <u>기본 값이 'red'</u> 설정되어있지만 -> 함수가 실행되면  
&nbsp; `setColor('blue')`를 통해, <u>const color의 value를 'blue'로 재할당</u>해준다.  
<span style="color:green">toggleSwitch 함수</span>는  
&nbsp; <u>버튼이 클릭될 때마다</u>(onClick) 실행되는 함수로, ->  
&nbsp; `const isSwitchOn`의 기본 값이 false로 설정되어있지만, 함수가 실행되면  
&nbsp; const isSwitchOn의 <u>value가 true와 false로 번갈아가며 할당</u>된다.

### state와 props를 활용하여 버튼의 색 바뀌기

- props를 사용하여 Child Component 색 변경하기

Parent component에서 Child compnent에게 `isSwitchOn을 전달`할 수 있다.

```java
//Parent component
import React, { useState } from "react";
import Child from "./Child/Child";

const Parent = () => {
  const [color, setColor] = useState("red");
  // console.log(color); //output == 'red'
  const [isSwitchOn, setSwitchOn] = useState(false);
  // console.log(`isSwitchOn ->`, { isSwitchOn }); //output == falsse -> true -> ...
  const changeColor = () => {
    setColor("blue");
  };

  const toggleSwitch = () => {
    setSwitchOn(!isSwitchOn);
  };

  return (
    <>
      <h1>Parent Component</h1>
      <Child isSwitchOn={isSwitchOn} text="기 화이팅" number={30} color={color} />
      <button onClick={toggleSwitch}>Click!</button>
    </>
  );
};

export default Parent;

//child component
import React from "react";

const Child = (props) => {
  // console.log(props); //output == {isSwitchOn: false, text: '기 화이팅', number: 30, color: 'red'}
  return (
    <p style= { { color:  props.isSwitchOn ? "blue" : "red"} }>
      {props.number}
      {props.text}
    </p>
  );
};

export default Child;
```

<span style="color:green"><Child isSwitchOn={isSwitchOn} text="기 화이팅" number={30} color={color} /></span>  
&nbsp; Parent Component에서 Child에게 isSwitchOn을 전달했고 ->  
<span style="color:green"><p style= { { color: props.isSwitchOn ? "blue" : "red"} }></span>  
&nbsp; Child Component에서 받은 <span style="color:red">props는 객체의 데이터 타입</span>으로, isSwitchOn의 value를  
&nbsp; 가져와야하므로 `props.isSwitchOn으로 접근`할 수 있다.

- Parent Component에서 직접 색 변경하기

```java
//Parent component
import React, { useState } from "react";
import Child from "./Child/Child";

const Parent = () => {
  const [color, setColor] = useState("red");
  // console.log(color); //output == 'red'
  const [isSwitchOn, setSwitchOn] = useState(false);
  // console.log(`isSwitchOn ->`, { isSwitchOn }); //output == falsse -> true -> ...
  const changeColor = () => {
    setColor("blue");
  };

  const toggleSwitch = () => {
    setSwitchOn(!isSwitchOn);
  };

  return (
    <>
      <h1 style= color: { { color: isSwitchOn ? "blue" : "red" } }>Parent Component</h1>
      <Child isSwitchOn={isSwitchOn} text="기 화이팅" number={30} color={color} />
      <button onClick={toggleSwitch}>Click!</button>
    </>
  );
};

export default Parent;

//child component
import React from "react";

const Child = (props) => {
  // console.log(props); //output == {isSwitchOn: false, text: '기 화이팅', number: 30, color: 'red'}
  return (
    <p style= { { color:  props.isSwitchOn ? "blue" : "red"} }>
      {props.number}
      {props.text}
    </p>
  );
};

export default Child;
```

Parent Component에서는, Child Component에서 처럼 값을 전달해주고 props를 사용해서  
값을 전달받지 않아도 된다!  
<span style="color:green"><h1 style= color: { { color: isSwitchOn ? "blue" : "red" } }>Parent Component</h1></span>  
&nbsp; `Child Component`에서는 isSwitchOn의 value를 받기 위해 -> color: <span style="color:red">props.isSwitchOn</span> 이렇게  
&nbsp; props(object)에 접근하여 정보를 받아왔지만,  
&nbsp; `Parent Compontent`에서는 <u>isSwitchOn에 직접 접근</u>할 수 있으므로 color: <span style="color:red">props.isSwitchOn</span>으로  
&nbsp; isSwitchOn의 value에 접근할 수 있다.

<!-- &nbsp; 그래서 버튼이 눌릴 때마다 isSwitchOn의 value가 바뀌게되고 ->  -->

## state 사용 예시

state에서 상태값을 설정하는 이유는 결국 컴포넌트 안의 요소에서 그 상태 값을 반영해서  
데이터가 바뀔 때마다 효율적으로 화면(UI)에 나타내기 위함이다.

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
