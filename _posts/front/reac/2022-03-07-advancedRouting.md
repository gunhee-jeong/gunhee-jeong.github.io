---
layout: single
title: "Advanced Router"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [라우팅, 동적, 정적, path, query] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# 학습 목표

&nbsp; 1.

# Routing?

## 경로에 따라 각기 다른 화면을 보여주는 것

route + -ing: 경로(route)를 찾아가는 행위!  
즉 라우팅이란 -> 다른 경로(url 주소)에 따라 다른 view를 보여주는 것을 말함

## SPA(single Page Application, 단일 페이지 애플리케이션)

SPA는 사용자가 웨 애플리케이션과 상호 작용하는 방식을 획기적으로 바꾼 기술  
사용자가 다른 뷰로 이동할 때 애플리케이션은 뷰를 동적으로 다시 그림

# 동적 라우팅

웹 사이트는 전체 아이템이 보여지는 <u>리스트 페이지</u>와 거기서 어떤 아이템을  
선택했을 때 해당 아이템의 디테일한 정보가 보여지는 <u>상세 페이지<u>로 구성된다.

&nbsp; 리스트 페이지에서 각각의 상품을 클릭했을 때 -> 주소의 끝에 아이템의  
&nbsp; id 값이 추가되어 페이지 이동을 하는 것을 볼 수 있는데  
&nbsp; 이와 같이 라우트 경로에 특정 값을 넣어 해당하는 페이지로 이동할 수 있게  
&nbsp; 하는 것을 동적 라우팅이라고 한다.

정적이지 않은, <u>동적일 수 있는 경로에 대하여 라우팅</u>을 하는 것을 <span style="color:red">동적 라우팅</span>  
(Dynamic Routing)이라고 부른다.  
&nbsp; 이는 `Path Parameter`와 `Query Parameter`를 통해 적용할 수 있다.

## 동적인 라우팅을 처리하는 방법

### Path Parameter

```java
localhost:3000/product/2
localhost:3000/product/45
localhost:3000/product/125
```

<u>2, 45, 125</u>.url 경로에서 달라지는 부분을 저장하는 매개 변수를  
`Path Parameter`라고 한다.

Path Parameter는 Router 컴포넌트에서 아래와 같이 정의된다.

```java
<BrowserRouter>
  <Routes>
    <Route path='/product/:id' element={<ProductDetail />} />
  </Routes>
</BrowserRouter>
```

&nbsp; `:`는 <u>Path Parameter가 올 것임</u>을 의미한다.  
&nbsp; id는 해당 Path Parameter의 이름을 의미한다.  
&nbsp; 변수명을 짓듯, 임의의 이름을 지정할 수 있다.

### Query Parameter

### 동적 라우팅의 흐름

<img src="https://user-images.githubusercontent.com/87808288/156949745-466c02c9-3c37-467f-9119-6f1a51bd9a6b.png" width="800" height="500">  
리스트 페이지에서 상품을 클릭하면, <u>onClick 이벤트</u>시 발생하는  
<span style="color:red">navigate 함수</span>를 통하여 `/product/1`로 이동한다.  
&nbsp; 리스트 페이지의 개별 상품을 클릭 -> <span style="color:green">navigate("/product/1")</span>로  
&nbsp; 상세 페이지로 이동한다.  
&nbsp; 상세 페이지로 이동하면 url은 <span style="color:red">"http://localhost:3000/product/1"</span>과  
&nbsp; 같이 변경되어있다.  
페이지에 필요한 데이터를 useEffect에서 feching한다.  
&nbsp; <u>필요한 id는 URL에 존재</u>하므로 <span style="color:red">useParams().id</span>에서 가져올 수 있다.

```java
function ProductDetail() {
  const params = useParams();

  useEffect(() => {
    const productId = params.id;
    fetch(`http://123.456.789:8000/products/${productId}`) // 1
      .then(res => res.json())
      .then(res => setData(res));
  },[]);

return (
...
)
}
```

&nbsp; URL이 <span style="color:red">/product/1</span>로 변하면, Router 컴포넌트에 정의되어 있는  
&nbsp; <span style="color:red">path='/product/:id'</span>에 따라, ProductDetail 컴포넌트가 마운트된다.  
&nbsp; ProductDetail 컴포넌트에서는 back-end에 <span style="color:red">id가 1</span>인 아이템에 대한  
&nbsp; 정보를 요청한다. ->  
&nbsp; 응답으로 받은 정보를 <span style="color:red">setData 함수</span>를 통해 <span style="color:red">data</span>라는 state에 저장하고,  
&nbsp; 이를 통해 상세 페이지 UI가 그려진다.

### useNavigate, useLocation, useParams Hook

`useNavigate` 훅은 url을 변경하는 <span style="color:red">함수를 반환</span>하고,  
`useLocation` 훅은 현재 정보를 담고 있는 <span style="color:red">객체를 반환</span>하고,  
`useParams` 훅은 Router에 등록해준 path parameter 정보를 담고 있는  
<span style="color:red">객체를 반환</span>한다.

##### useNavigate Hook

```java
function Product(props) {
  const navigate = useNavigate();

  const goToDetail = () => {
    navigate(`/product/${props.id}`);
  }

  return (
    <div className="productContainer" onClick={goToDetail}>
	...
    </div>
  )
}
```

useNavigate 훅을 실행하면 페이지를 이동시키는(url을 변경시키는) 함수를  
반환한다.

##### useLocation Hook

```java
function ProductDetail(props) {
  const location = useLocation();
  console.log(location);

  return (
    ...
  )
}
```

`useLocation` 훅을 실행하면 <u>경로 정보를 담고 있는</u> <span  style="color:blue">객체를 반환</span>한다.  
위 코드에서는 <u>해당 객체를 location 이라는 변수에 할당</u>했다.  
location 변수를 콘솔로 출력해 보면 다음과 같은 로그가 출력된다.

```java
{
  pathname: '/product/1',
  search: '',
  hash: '',
  state: null,
  key: 'default'
}
```

여러가지의 정보가 있는데, 주목할 부분은 <u>pathname</u>과 <u>search</u> 프로퍼티이다.  
&nbsp; pathname: 현재 경로 값  
&nbsp; search: 현재 경로의 query parameter 값

##### useParams Hook

```java
// 현재경로: /product/1

function ProductDetail(props) {
  const params = useParams();

  console.log(params);

  return (
    ...
  )
}
```

`useParams` 훅을 실행하면 <u>path parameter 정보</u>를 담고 있는 <span   style="color:blue">객체를 반환</span>!  
위 코드에서 해당 <u>객체를 params라는 변수에 할당</u>해주었다.  
params 변수를 콘솔로 출력해 보면 다음과 같은 로그가 출력된다.

```java
{
  id: 1
}
```

### useParams().id

다시 돌아와서, 어떻게 <u>URL에 담겨있는 id 값을 가져올 수</u> 있을까?  
바로 <span style="color:red">useParams 훅을 이용</span>하여 가져올 수 있다.  
Path Parameter로 명시해둔 값은 usePatams 훅이 리턴하는  
객체에 담기기 때문이다.

```java
// ProductDetail.js
// current url -> localhost:3000/product/1

function ProductDetail() {
  const params = useParams();

  console.log(params.id) // 1

  return (
    ...
  );
}
```

따라서 `useEffect 훅에서` <span style="color:red">해당 id 값</span>을 통해 서버로 요청을 보내는 것을 통해  
원하는 정보를 받아올 수 있다.

```java
useEffect(() => {
  fetch(`${API}/${params.id}`)
    .then(res => res.json())
    .then(res => setData(res));
},[]);
```

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
