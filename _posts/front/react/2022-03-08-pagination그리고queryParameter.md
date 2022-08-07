---
layout: single
title: "Pagination & Query Parameter"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [queryString, 쿼리스트링, 페이지네이션, 쿼리스트링] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Pagination

back-end에서 가지고 있는 데이터는 무수히 많고, 그 데이터들을  
<u>한 화면에 전부 보여줄 수 없는 경우</u>에 사용한다.  
흔히 게시판의 "이전" 그리고 "다음" 페이지를 끊어서 보여주는 기능으로  
이해할 수 있다.

front-end에서는 **현재의 위치(offset)**과 추가로 보여줄 **컨텐츠의 수(Limit)**를  
back-end에게 전달한다. ->  
back-end에서는 그에 해당하는 데이터를 끊어 보여주는 방식으로 구현하게 된다.

# Query Parameter(Query String)

`localhost:8000/products?limit=10&offset=5` 라는 주소가 있다면,  
API 뒷 부분에 붙어있는 `?`로 시작하는 텍스트가 바로 <span style="color:red">쿼리스트링</span>이다.  
<span style="color:red">limit=10&offset=5</span>의 경우 -> "limit이 10이면서 offset이 5일 경우의  
product 페이지를 보여달라"는 요청으로 해석된다.  
&nbsp; <u>?기호</u>는 `쿼리스트링의 시작`을 알린다. url에서 ?기호는 유일무이하다.  
&nbsp; <u>limit</u>는 한 페이지에 `보여줄 데이터의 수`를 나타낸다.  
&nbsp; <u>offset</u>은 `데이터가 시작하는 위치`(index)를 나타낸다.  
&nbsp; <span style="color:red">parameter=value</span>로 필요한 파라미터의 값을 작성한다.  
&nbsp; 파라미터가 여러 개일 경우 <u>&를 붙여서</u> 여러 개의 파라미터를 넘길 수 있다.

# useLocation().search

쿼리스트링을 이용한 <u>페이지 네이션</u> 기능 또한 <u>동적 라우팅</u> 기능과 크게 다르지 않다.

## 두 기능의 비교

##### 동적 라우팅

&nbsp; 1. 리스트 페이지에서 카드를 클릭한다.  
&nbsp; 2. url 이동을 한다. 이때, 카드의 고유한 id 값이 url에 포함된다.  
&nbsp; 3. 이동한 페이지에서, url에 담겨있는 id 값을 <span style="color:red">useParams</span> 훅을  
&nbsp; &nbsp; &nbsp; 이용해 가져온다.  
&nbsp; 4. 가져온 id 값을 이용하여 데이터를 요청한다.

##### 페이지네이션

&nbsp; 1. 리스트 페이지에서 페이지 이동 버튼을 클릭한다.  
&nbsp; 2. url 이동을 한다. 이때 url에는 각 버튼에 <u>해당하는 쿼리 스트링이 포함</u>된다.  
&nbsp; 3. 이동한 페이지에서, url에 담겨있는 쿼리스트링을 <span style="color:red">useLocation</span> 훅을  
&nbsp; &nbsp; &nbsp; 이용하여 가져온다.  
&nbsp; 4. 가져온 쿼리스트링을 이용하여 데이터를 요청한다.

`Path Parameter`에 대한 정보가 <span style="color:red">useParams</span> 훅이 반환한 객체에 담기듯이,  
`쿼리스트링`에 대한 정보는 <span style="color:red">useLocation</span> 훅이 반환한 객체의  
search 프로퍼티에 담긴다.

```java
// current url -> localhost:3000/products?offset=10&limit=10

function ProductList(b) {
  const location = useLocation();

  console.log(location.search) // ?offset=10&limit=10

  return (
      ...
  )
}
```

이를 통해 url에서 쿼리스트링 정보를 받아와서, 해당 정보를 통해 데이터를  
요청할 수 있다.

```java
fetch(`${API}${location.search}`)
  .then(res => res.json())
  .then(res => ...)
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
