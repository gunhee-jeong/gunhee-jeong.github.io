---
layout: single
title: "React-Component의 State"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [component, state] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# state

state란 말 그대로 <u>컴포넌트의 상태 값</u>을 의미한다.

state와 props는 둘 다 object이고, 화면에 보여줄 정보(상태)를 가지고 있다는 점에서 비슷한 역할을 한다.  
props는 컴포넌트를 사용하는 부모쪽에서 전달해야만 사용할 수 있고(함수의 parameter처럼), 읽기전용이다.  
state는 컴포넌트 내에서 정의하고 사용하며 업데이트할 수 있다.

아래의 코드는 버튼을 눌렀을때, state를 변화시켜 보여줘야할 텍스트를 바꾸는 코드이다.  
&nbsp; 예제코드에서는 isClicked라는 하나의 state만 있지만, 여러 개의 state를 추가할 수 있다.  
&nbsp; 그리고 state의 이름은 원하는대로 지을 수 있다.

```java
import { useState } from "react";
import ReactDOM from "react-dom";

function Button(props) {
  const [isClicked, setIsClicked] = useState(false);

  return (
    <button className="btn" onClick={() => setIsClicked(!isClicked)}>
      {isClicked ? "좋아요" : "싫어요"}
    </button>
  );
}

ReactDOM.render(<Button />, document.getElementById("root"));
```

&nbsp; `<button />`를 클릭하면 <u>onClick에 넘긴 함수를 실행</u>하게 된다.

```java
<button className="btn" onClick={() => setIsClicked(!isClicked)}>
      {isClicked ? "좋아요" : "싫어요"}
</button>
```

## 코드 해석

### const [isClicked, setIsClicked] = useState(false)

- useState를 통해서 isclicked라는 state와,  
  setIsClicked라는 state를 업데이트할 수 있는 함수를 선언했다.
- useState의 인자로 false를 전달하여서 isClicked의 초기값이 false가 되도록 설정하였다.

설명

- isClicked라는 state를 선언하는 코드이다.
- 함수형 컴포넌트에서 state를 만들 때는 useState라는 함수를 이용한다.
- useState의 인자로 전달된 값은 선언된 state의 초기값으로 할당된다.
- useState의 실행 결과는 좌측에 [state, state를 갱신할 수 있는 함수] 배열 형태로 리턴된다.
- useState의 리턴값을 배열 구조 분해 할당문법을 이용해서 각각 isClicked와 setIsClicked라는 이름으로 선언했다.

### onClick={() => setIsClicked(!isClicked)}

설명

- onClick이 달려있는 `<button />`를 클릭할 때마다, isClicked 상태가 <u>true나, false</u>로 업데이트된다.
- click하면 isClicked라는 state를 수정한다. setIsClicked 함수로 state를 업데이트할 수 있다.
- setIsclicked 함수의 인자로 전달된 값으로 isClicked 값이 업데이트된다.
- !isClicked으로 인자로 전달해 업데이트한다는 말은,
- 현재 isClicked의 반대로(true면 false로, false면 true로) 저장한다는 말이다.
- 위 코드로 인해 button에 click event가 발생할 때마다 isClicked state가 업데이트된다.

# props와 state

`<Button />`에 type을 추가했고, Button 컴포넌트에서 props로 받을 수 있다.

```java
import { useState } from "react";
import ReactDOM from "react-dom";
import "./index.css";

function Button(props) {
  const [isClicked, setIsClicked] = useState(false);

  return (
    <button
      className={`btn ${props.type === "like" ? "like" : ""}`}
      onClick={() => setIsClicked(!isClicked)}>
      {isClicked ? "좋아요" : "싫어요"}
    </button>
  );
}

ReactDOM.render(<Button type="like" />, document.getElementById("root"));
```

props.type이 'like'이면 like-btn이라는 class 속성이 추가된다.  
미리 .like-btn에 배경색이 나오도록 css는 추가해 두었다.

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
