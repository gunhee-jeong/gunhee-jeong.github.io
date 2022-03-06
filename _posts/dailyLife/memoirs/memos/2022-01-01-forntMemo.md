---
layout: single
title: "front memo"
# categories: Git
categories:
  - Memo # HTML CSS JavaScript Server Algorithm Wecode Programmers CS vsCode
tag: [기록] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# 코드잇 진도

- React

웹 프론트엔드 스쿨 -> react 프론트엔드 개발 -> react 웹 개발 시작하기
&nbsp; 인덱스 파일에서 하는 일,

웹 프론트엔드 개발 -> react로 웹사이트 만들기:  
리액트 라우터 v6 소개, 리액트 라우터 설치하기, Routes로 페이지 나누기

# westudy

## React

React 0. 시작하기 전에 -> 9번 시청해야함!!!

```java
ReactDom.render(<h1>안녕 리액트!<h1>, document.getElementById('root'));
```

ReactDom.render 메소드는 첫번째 argument 값을 활용해서 HTML 요소를 만들고,
두번째 argumnet 값에 -> 그 요소를 넣어주는 역할을 한다.

JSX에서는 태그 안에 class를 넣을 때 `className=""으로 사용`해야한다.
<u>JS에서 class는 이미 객체지향의 의미를 갖는 class 선언에 사용</u>되기 때문이다.
그리고 HTML에서 form 태그 안에는 label 태그와 form 태그가 사용되는데
label 태그 안에는 'for' 속성이 있는데, 이것또한 JS에서 이미 for문에 사용되고 있으므로
`htmlFor`로 작성해서 사용해야한다.

```java
ReactDom.render(
  <form>
    <label htmlFor="name">이름</label>
    <input id="name" type="text" />
  </form>,
document.getElementByID('root'))
```

# fragment

react는 render를 하기위해서 여러 태그들을 하나의 태그로 감싸주어야 error가 발생하지 않는다.
아래의 코드처럼 여러 태그들이 하나의 태그로 감싸지지 못하면 error가 발생한다.

```java
//error 발생
ReactDom.render(
  <p>안녕</p>
  <p>리액트</p>,
document.getElementByID('root'))

//하나의 태그로 감싼 모습
ReactDom.render(
  <div>
    <p>안녕</p>
    <p>리액트</p>,
  </div>
document.getElementByID('root'))
```

이렇게 하나의 태그로 감싸기 위해서 만들어진 것이 fragment이다.

```java
ReactDom.render(
  <Fragment>
    <p>안녕</p>
    <p>리액트</p>,
  </Fragment>,
document.getElementByID('root'))

//축약형
ReactDom.render(
  <>
    <p>안녕</p>
    <p>리액트</p>,
  </>,
document.getElementByID('root'))
```

```java
ReactDom.render(
  <>
    <h1 id="title">가위바위보</h1>
    <button className="hand">가위</button>
    <button className="hand">바위</button>
    <button className="hand">보</button>
  </>,
document.getElementByID('root'));
```

다른 사람과 비교하지말고, 어제의 나와 비교하자.
하루하루를 최대한 밀도있게 보내자. 힘내자!

input 태그 속성의 outline은 무엇인가?
form 태그?(form 태그와 button의 연관성?)
&nbsp; 타입을 버튼으로!
&nbsp; button 태그의 속성 중 type은 아무것도 쓰지 않을 때 기본 속성이 submit이다.
&nbsp; 그래서 form 태그 안에 button을 눌렀을 때 -> 제출이 되면서 우리가 원하는 결과를 얻지 못할 수 있으므로
&nbsp; type=button으로 설정해주어야 한다.

- html 파일에서 script 태그를 바디 속 가장 아래에 사용하는 이유?

script 태그를 바디 속 가장 위에 놓고 실행해보면
&nbsp; error가 발생하는 것을 볼 수 있다. 그 이유는 js에서 addEvnetListener가 dom에 접근하여 값을 가져와야하는데
&nbsp; html이 구성되기 전에 js파일이 읽어지면 js파일에서 설정한 변수들의 값이 'undefined'되기 때문에 error가 발생하게 된다.

- 'use strit'란??

엄격모드를 사용하는 것을 말하는데,
사람으로 발생하는 error를 방지하기 위해 사용한다.
좀더 찾아보자... 부족하다!!!

- '이벤트 버블링' 기억해야할 키워드! 검색해보자

- getElementsByClassName와 getElementById의 차이?

- event, keyup과 input의 차이?

- addEventLis의 구조 다시보자

x.addEL(event,)를 사용할 때 뒤에 argumnet에는 함수이름만 들어가도 호출이된다....
원래 함수 호출하려면 함수() 이렇게 해야하는거 아닌가?...

- JS 코드를 짤때는 한 번에 쫙하는 것이 아니라, console.log를 중간중간 넣어서 값을 체크해야한다.

이거 안하다가 큰코 다친다 정말!

- boolean naming convention

boolean 타입을 값으로 받게되는 변수명에는 is를 붙여서,
네이밍만 보더라도 boolean 타입의 값을 받음을 알 수 있도록 하자!

- keycode보다는 code를 사용하자

- window.event 속성 검색해보자

```java
if(window.event.code === 'Enter') {
    success();
  }
```

- trim의 사용법을 검색해보자

댓글창에 스페이스바만 입력할 경우, 댓글창은 빈화면이기 때문에 이를 막아주어야한다.
이때 trim()을 사용하면, 스페이스바의 공백을 제거하여 빈 상태로 만드는 듯 하다.

- innerHTML 과 innerText의 차이

리액트에선 쓰이지 않는데, 그 개념을 알아두면 좋을 듯 하다.

- DOM을 이용하여 class 이름을 부여할 때의 방법 2가지

```java
userId.className = 'name';
userId.classList.add('name');

```

input의 경우, 복사 -> 붙여넣기를 하여도 입력이 되고
&nbsp; 'input' 이벤트의 경우 값이 바뀔 때 작동되는
keyup은 타자를 쳤을 때 작동하게 되는 것

vh와 %의 차이점 정리하기

common.css에서 따로 flex를 모아서 사용??

자바스크립트의 연결은 body 태그의 가장 마지막에 넣어주자
&nbsp; 그런데 defer를 넣으면??
어디든 들어가도 상곤이 없다?!

getElementsBy와 element의 차이?
querySelector를 가장 많이 사용함
&nbsp; 이걸 쓰면 document를 다 돌지 않기 때문에 이걸 선호함

form 태그를 공부하자? id input을 쓰지 말고
이벤트 위임에 관련해서 꼭 블로그 쓰기
<span style="color:red">이벤트 버블링, 이벤트 </span>위임!

input 이벤트는 뭔가요 ㅠㅠ
input 내역이 달라지면?? 인지하는 그런 이벤트?
이것도 블로그 써야할 듯...

const boolena naming convention 사용하기 (isValidid)

키코드와 코드의 차이?
&nbsp; 근데 code를 쓰는 것이 좋다! 아마 키코드는 지원하지 않을 것이다

inhtml와 innerText의 차이?

학습 목표에 알맞은 대답을 할 수 있는가?

# React

일단 화면에 불러와지는 파일은 html 파일이다. -> public 파일에  
index라는 것은 entry point의 기능이다.(이름 바꾸지마세요!)  
이 public 파일이 /뒤의

컴포넌트 파일은 PascalCase 방법으로 작성함 -> 그 안의 파일들도?

함수형 컴포넌트 나누기

# git

충돌하면 -> 마스터로 이동하고 pull ->

폴더명은 유니크하게..  
폴더안의 파일들은 상관없음

새로운 브랜치를 만들고 싶다면 메인에서 만들어야한다? 1 + 2 + 3
let a = 1 + 2

# React

set 함수의 비동기화적인 문제를 발견함

set 함수의 무한루프 error를 공부해야함  
&nbsp; state가 변화할 때마다 -> 랜더링됨!  
&nbsp; 그래서 loop error가 발생하는 것임

set 함수를 사용하기 위해서 -> 함수 안에 변수 선언, 함수 밖에 변수 선언,  
함수 밖에 return, method안에 method

react, key .id가 존재하는 이유는 무엇인가?

## Router.js

back-end와의 연결 blog 작성하기

## westagram 리뷰

공통 파일은 branch를 따로 만들자!

login 컴포넌트 분리하지 말것

인라인 스타일 지양할 것 (버튼 활성화)

const를 사용할 것(습관화 하자!!!)  
재할당이된다는 확신이 있지 않은 이상

파스칼케이스는 컴포넌트만

boolean naming conven

map method 사용하기  
실제로 상품

useRef() ?? 이거 뭐야?

태그 셀랙터를 사용하지 말고 ->

순서 컨벤션 확인하기....

localhost 는 생략 가능합니다  
fetch에서!

addClick! 같이

get은 생략이 가능함  
이것은 취사선택임(누그는)

css 적용 우선순위 검색해보기

성훈님 fetch 함수 error 핸들링 -> 래영님이 리뷰보기

react에서 id를 사용하면 -> component에서 문제가 생길 수 있음

성훈님 코드 꼭 다시보자!  
정말 좋은 것 같아요!!

& 표시? 뭐지??

react로 사고하기....?  
button del 속성을??

.className에는 숫자를 넣지 말자

## 22 02 25 wrap-up

인터넷이란?  
웹이란?  
1세대 웹이란?  
2세대 웹이란?  
3세대 웹이란?  
DOM은 무엇인가?  
react로 왜 개발공부를 선택하였는가?  
back-end와의 협업을 하면서 느낀점?  
HTTP 통신의 내용 심화하기

## 2월 28일

몬스터 과제: filter를 이용한 방법 정리하기

## 얌얌프룻

원하는 것, 모든 것을 팔아도된다

제일 중요한 것은 필수구현 사항  
&nbsp; 네트워크 로딩은 필수적으로 처리하고 싶은 기능

##### 필수구현

<span style="color:red">로그인 회원가입</span>  
메인페이지  
<span style="color:red">장바구니</span>  
&nbsp; 이 부분은 꼭 해보길!!!  
<span style="color:red">상품리스트</span>  
&nbsp;  
<span style="color:red">상품 상세정보</span>  
&nbsp;

#### 추가구현 사항

어드민 페이지  
&nbsp; 중요한 부분이지만, 어드민은 이거 하나로 엄청난 작업임...  
&nbsp; 하지만 이전의 작업들을 수행한다면 다 할 수 있기 때문에 생략을 추천함  
결제  
&nbsp; 이것은 따로 서비스가 나오기 때문에(외부 API) 이것은 제외함

##### 얌얌프룻 코드리뷰

form 태그의 사용법을 알고있나?(form 태그 개념, 다시 잡기)

img 태그에서 alt속성 꼭 넣자

jsx 문법에서 content가 없는 element는 `</>` 이렇게 사용해야!

bottom-up 방식  
&nbsp; 어떤 <u>element를 감싸는 레이아웃</u>에서는 `고정 px로 height 값을`  
&nbsp; `주지 않는다!` 그 이유는 추후에 해당 레이아웃 안에 element가 추가될 수 있고  
&nbsp; <span style="color:red">크기 등이 충분히 바뀔 수 있기 때문</span>이다.  
&nbsp; 그래서 레이아웃을 짤 때에는 <span style="color:red">bottom-up 방식</span>으로 `아래에 있는 element에`  
&nbsp; `고정 값`을 주고 해당 element를 감싸는 요소에는 자식 요소로 인해 저절로  
&nbsp; 레이아웃을 형성할 수 있도록 하는 방식으로 작성하는 것이 <span style="color:red">유지보수에 좋다</span>!

22 03 03  
&nbsp; mockData 먼저연결하기  
&nbsp;

##### 느낀 것

백엔드와의 소통  
&nbsp; get 요청, post 요청의 차이?  
&nbsp; put 요청, PATCH 요청의 차이? -> 블로깅

## 3월 6일

##### 저녁 회의

주문상세에서 보내줘야할 것  
&nbsp; product_id, quantity, option(true, false)

<!-- 메소드 위에 변수 선언, 메소드 안에 메소드, 메소드 끝나고 리턴 -->

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

유형1: ('사이즈를 조절' -> HTML 태그 사용) :  링크 걸기)


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
