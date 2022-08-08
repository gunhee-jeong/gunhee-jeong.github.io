---
layout: single
title: "components 컴포넌트"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [유데미 리액트 완벽 가이드] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-08-08T10:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1장 컴포넌트
## 1. 컴포넌트 트리
<span class="red">컴포넌트 트리</span>의 가장 맨 위에 중요한 컴포넌트인 <span class="tomato">App 컴포넌트</span>가 존재한다.  
맨 위에 있는 컴포넌트만이 <span class="blue">리액트 돔 렌더의 지시로 HTML 페이지에 직접 렌더링</span>된다.  

<img src="https://user-images.githubusercontent.com/87808288/183323241-135a4c59-dd49-40ae-969e-86fd1ae6dbdd.png" width="30%">  
이렇게 <span class="tomato">컴포넌트 트리의 가장 상위</span> 위치로 존재하는 <span class="blue">App.js는 src 폴더에</span> 존재하게 되고  
<span class="royalblue">다른 컴포넌트 파일</span>들은 <span class="blue">components 폴더</span> 내에 위치하게 된다.  
또한 컴포넌트가 되는 <span class="blue">파일들의 이름은 대문자</span>로 시작하는 단어로 생성하게 된다.  

리액트에서 <span class="red">컴포넌트</span>는 결국 <span class="red">함수</span> 일뿐이다.  

```jsx
// ExpenseItem.js
function ExpenseItem() {
  return <h2>Expense item!</h2>
}

export default ExpenseItem;
```

그리고 이 <span class="royalblue">ExpenseItem 컴포넌트</span>를 App.js에 연결하여  
<span class="blue">하나의 HTML 태그와 같이</span> ExpenseItem 컴포넌트를 사용할 수 있다.  

```jsx
// App.js
import ExpenseItem from './components/ExpenseItem';

function App() {
  return (
    <div>
      <h2>Let's get started!</h2>
      <ExpenseItem></ExpenseItem>
    </div>
  );
}

export default App;
```

## 2. CSS 파일 연결하기
```jsx
// ExpenseItem.js
import './ExpenseItem.css';

function ExpenseItem() {
  return (
    <div className='expense-item'>
      <div>March 28th 2022</div>
      <div className='expense-item__description'>
        <h2>Car Insurance</h2>
      </div>
      <div className='expense-item__price'>$294.67</div>
    </div>
  )
}

export default ExpenseItem;
```

```css
/* ExpenseItem.css */
.expense-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
  padding: 0.5rem;
  margin: 1rem 0;
  border-radius: 12px;
  background-color: #4b4b4b;
}

/* ...... */
```

이렇게 css 파일을 만들고, <span class="blue">ExpenseItem.js 파일에 import</span>하는 방식으로 CSS 파일과 연결할 수 있다.  








`Component`란 <span style="color:red">재사용이 가능한 UI 단위</span>를 말한다.

<u>동일한 코드가 반복되는 부분</u>을 하나의 component로 만들어서 같은 디자인의 input이 필요한 곳마다  
재사용할 수가 있다.  
컴포넌드를 하나만 만들고 여기저기서 재사용하면, input 디자인이 바꼈을 때 CSS 한 줄만 수정하면  
로그인, 회원가입, 내정보수정 페이지에 바뀐 디자인이 모두 반영된다.

`컴포넌트는 독립적으로, 재사용가능한 코드로 관리할 수` 있다.  
하나의 컴포넌트에 필요한 <u>HTML, CSS, JS를 모두 합쳐서</u> 만들 수 있다.

컴포넌트는 `함수와 비슷`하다.  
함수도 기능이 독립적이고 <u>한번 선언해두면 필요할 때 마다 호출하면서 재사용</u>할 수 있기 때문이다.  
그리고 <u>컴포넌트도 함수처럼 input을 받아서 return할 수</u> 있다.

React 컴포넌트에서는 `input`을 <span style="color:red">props</span>라 하고, `return`은 화면에 보여져야할 <span style="color:red">React 요소</span>가 return된다.

# Component 만들기

React는 component를 만들고 관리하기 좋은 라이브러리이다.

React에서는 component를 class나 함수로 만들 수 있다.  
어떤 경우에는 함수로 만들면 좋고, 어떤 경우에는 class로 만들어야만 한다.

# Component 사용

위처럼 정의한 컴포넌트는 <span style="color:red">함수 이름 or class 이름</span>으로 사용할 수 있다. 태그처럼 `<Welcome />`으로 작성해야한다.

우리가 정의한 컴포넌트를 사용할 때, <u>원하는 property를 얼마든지 추가할 수</u> 있다.  
그러면 Welcome 컴포넌트(함수)에서 parameter로 해당 property를 받아서 사용할 수 있다.  
이것을 <span style="color:red">props</span>라고 한다! <u>props는 property의 줄임말</u>이다.  
`.(dot)으로 속성명에 접근`가능하고, props.속성명으로 속성값을 가져올 수 있다.

```java
// 1. Welcome 컴포넌트 정의
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// 2. App 컴포넌트 정의
function App() {
  return (
    <div>
      <Welcome name="wecoder" />
      <Welcome name="John" />
      <Welcome name="Sara" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

1. Welcome 컴포넌트  
   Welcome 컴포넌트를 사용한 측(부모)에서 `name이라는 property`를 부여했고,  
   <u>props.name</u>의 값을 사용한다.
2. App 컴포넌트를 보니 div로 감싸져있고, `<Welcome />` 컴포넌트를 세번 사용했다.  
   <span style="color:red">name이라는 property</span>를 부여해주었다.
3. <span style="color:red">ReactDOM.render</span> 함수로 React 요소를 그려준다.  
   root라는 id를 찾아 `<App />` 컴포넌트를 그려준다.

# 더 작은 Component로 분리하기

```java
function Comment(props) {
  return (
    <div className="comment">
      <div className="user-info">
        <img className="avatar"src={props.author.avatarUrl}alt={props.author.name}/>
        <div className="user-info-name">
          {props.author.name}
        </div>
      </div>
      <div className="comment-text">
        {props.text}
      </div>
      <div className="comment-date">
        {formatDate(props.date)}
      </div>
    </div>);
}
```

위의 <u>component에서 .avatar</u> 부분을 그대로 떼와서 <u>Avatar라는 이름으로 component</u>를 만들면  
&nbsp; Comment 컴포넌트에서는 `props.author`로 접근해서 avatarUrl과 name을 가져왔는데,  
&nbsp; Avatar 컴포넌트에서는 <u>좀 더 직관적으로 사용할 수 있도록</u> <span style="color:red">user</span>라는 이름으로 받아올 수 있다.  
&nbsp; <span style="color:red">props.user</span>에서 avatarUrl, name 값을 가져왔고, `<Avatar />`를 사용하는 측에서  
&nbsp; user라는 attribute를 추가해야한다.

```java
function Avatar(props) {
  return (
    <img className="avatar"src={props.user.avatarUrl}alt={props.user.name}/>);
}
```

&nbsp; Avatar 컴포넌트에서 user의 avatarUrl과 name이 필요하므로, Comment 컴포넌트에서  
&nbsp; props.author 정보를 user라는 attribute로 넘겨주었다.  
&nbsp; props.author의 avatarUrl, name 값이 user를 통해 전달되었다.

```java
function Comment(props) {
  return (
    <div className="comment">
      <div className="user-info">
        <Avatar user={props.author} />
        <div className="user-info-name">
          {props.author.name}
        </div>
      </div>
      <div className="comment-text">
        {props.text}
      </div>
      <div className="comment-date">
        {formatDate(props.date)}
      </div>
    </div>);
}
```

&nbsp; 이제 한 번더 분리하여, `.user~info` 부분을 컴포넌트로 만든다.  
&nbsp; 재사용할 가능성이 조금이라도 있다면 컴포넌트로 만들어주는 것이 좋다.  
&nbsp; `.uesr-info` 부분을 그대로 떼어다가 UserInfo라는 컴포넌트로 만들었다.

```java
function UserInfo(props) {
  return (
    <div className="user-info">
      <Avatar user={props.user} />
      <div className="user-info-name">
        {props.user.name}
      </div>
    </div>);
}
```

Comment 컴포넌트가 이제 <u>아래의 코드처럼 간결</u>해진다!

```java
function Comment(props) {
  return (
    <div className="comment">
      <UserInfo user={props.author} />
      <div className="comment-text">
        {props.text}
      </div>
      <div className="comment-date">
        {formatDate(props.date)}
      </div>
    </div>);
}
```

## reference

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
