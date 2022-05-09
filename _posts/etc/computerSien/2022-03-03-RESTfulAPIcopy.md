---
layout: single
title: "REST"
# categories: Git
categories:
  - CS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [REST, API] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

## REST(REpresentation State Transfer)하다?

<span style="color:red">REST</span>란 웹에 존재하는 모든 자원(resorce, ex, 이미지, 동영상, 데이터)에  
고유한 URI를 부여하여 자원에 주소를 지정하는 방법론 또는 규칙이다.

## RESTful API란?

`RESTful API`는 REST 특징을 지키면서 API를 제공한다는 의미이다.

장점: `self-descriptiveness`  
RESTful API는 그 자체만으로도 API의 목적이 쉽게 이해 되야한다.

단점으로는 -> 표준규약이 없어, <u>안티패턴으로 작성되는 경우가 흔하다</u>.

> 안티패턴?  
> 실제 많이 사용되는 패턴이지만, 비효율적이거나 비생산적인 패턴

##### 기본 배경 지식

URI(Uniform Resource Identifier)  
&nbsp; 해당 사이트의 특정 자원의 위치를 나타내는 유일한 주소

HTTP Method  
&nbsp; HTTP request가 의도하는 action을 정의한 것

Payload  
&nbsp; HTTP request에서 server로 보내는 데이터(body)

## RESTful API 설계 규칙

##### URI 정보를 명확하게 표현해야 한다.

resource는 명사를 사용한다.  
&nbsp; ex) GET/user/1 -> GET/users/1  
&nbsp; 복수 형식으로 작성하는 것이 좋다.

##### resource에 대한 행위를 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

URI에 HTTP Method가 포함되서는 안된다.  
&nbsp; ex) GET delete/user/1 -> DELETE /users/1  
URI에 `동사가 포함되서는 안된다`.  
&nbsp; ex) GET/ user/show/1 -> GET/users/1  
&nbsp; ex) POST insert/user/2 -> POST/users/2  
resource 사이에 연관 관계가 있는 경우  
&nbsp; /리소스/고유ID/관계 있는 리소스  
&nbsp; ex) GET/users/{user\*id}/profile  
파일의 경우 payload의 포맷을 나타내기 위한 파일 확장자를 URI에 포함시키지 않는다.  
&nbsp; ex) GET user/1/profile-photo/jpg (X)  
&nbsp; ex) GET user/1/profile-photo (이때, payload의 포맷은 headers에 accept를 사용한다.)  
URI 마지막 문자로 /를 포함하지 않는다  
&nbsp; ex) GET users/portfolios/ (X)  
불가피하게 URI가 길어지는 경우 -을 사용하여 가독성을 높인다  
&nbsp; \_는 사용하지 않는다  
URI 경로에는 대문자 사용을 피하도록 규정하고 있다.

##### RESTful하지 못한 API 설계 예시

<img src="https://user-images.githubusercontent.com/87808288/156532749-c9168d30-7ca5-4258-a190-a0bc95815f26.png" width="500" height="400">

## Path parameter

## Query parameter

<img src="https://user-images.githubusercontent.com/87808288/156530859-9bdfcd2a-1fa5-4207-8bba-bb7498e0936a.png" width="500" height="400">

<img src="https://user-images.githubusercontent.com/87808288/156533246-5190f2e4-d14a-4e00-a80c-34f3a3ecc77e.png" width="500" height="400">

<img src="https://user-images.githubusercontent.com/87808288/156531480-7adac8a0-3524-43bb-aa11-ac188b355632.png" width="500" height="200">

<img src="https://user-images.githubusercontent.com/87808288/156531682-297228b8-dfcb-4e4a-9e53-3805ec5d6e53.png" width="500" height="200">

<img src="https://user-images.githubusercontent.com/87808288/156533027-cd544f02-9323-465e-8b65-09f2b4f7db0f.png" width="500" height="200">

## Status Code

<img src="https://user-images.githubusercontent.com/87808288/156533414-6c35ad40-bace-4d7b-b470-2a6cb064baf3.png" width="500" height="200">

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
