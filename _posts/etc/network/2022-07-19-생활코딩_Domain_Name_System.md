---
layout: single
title: "생활코딩 -> Domain Name System(DNS)"
# categories: Git
categories:
  - network # HTML CSS JavaScript Server Algorithm Wecode Programmers CS vsCode
tag: [생활코딩, web] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-19T19:30:00+09:00   
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---  
# Domain Name System
host와 host가 서로 통신하기 위해서는 주소가 필요하다.  
이를 위한 주소가 바로 IP address이다.  

DNS의 핵심은 바로 <span style="color:red">DNS Server</span>이다.  
DNS Sever에는 <u>수많은 IP 주소의 domain 이름이 저장</u>되어있다.  

<img src="https://user-images.githubusercontent.com/87808288/179732103-fdffc426-57d6-4615-a6cb-cc59541b34e3.png" width="100%">  
우리가 웹 브라우저에 "www.icann.org"라고 입력하면  
우리의 OS는 DNS Server에 접속해서 icann.org의 IP 주소가 무엇인지 검색하게 된다.  
그렇게 DNS Server가 컴퓨터에게 IP 주소를 알려주면  
이때서 이제 IP 주소에 해당하는 컴퓨터에 접속하게 되는 것이다.  

## 1. DNS의 태동
### (1) before DNS
93.184.216.34라는 IP 주소를 가진 사이트가 있는데  
다른 컴퓨터에서 위의 복잡한 IP 주소를 이용해 사이트에 접속하는 것이 아니라  
고유한 이름을 검색하면 그 이름이 93.184.216.34으로 변환되어 접속할 수 있도록 하고 싶었다.  

<img src="https://user-images.githubusercontent.com/87808288/179759382-d73ea018-d405-4a94-932e-58f2168c4dcb.png" width="100%">  
그래서 <u>Stanford Research Institute</u>라는 단체를 통해 <span style="color:blue">신뢰할 수 있는 hosts 파일</span>을  
클라이언트가 다운받아 example.com을 누르면 저장된 IP 주소로 변환되어 이동하는 방식을 사용했다.  

하지만 인터넷이 점점 거대해지면서 이 방식에도 문제가 있다는 것을 느끼게 된다.  
Stanford Research Institute에서는 hosts 파일을 갱신함에 있어서  
수동으로 처리하는 부분들이 있었고 그러다보니 즉각적인 업데이트를 하지 못했다.  
또한 hosts 파일 하나에 모든 IP 주소들이 담긴다는 것은 한계를 빠르게 경험하게 했다.  

## 2. DNS의 원리
<img src="https://user-images.githubusercontent.com/87808288/179763198-1e1d983f-df20-4488-9dae-6a33203c9dab.png" width="100%">  
예전에는 IP 주소가 변경되면 이를 수동으로 알리는 행위를 통헀지만  
DNS를 통해 이런 부분들이 사라지고 즉각적으로 DNS Server에 업데이트할 수 있게 되었다.  
또한 <u>예전에는 hosts 파일로 IP 주소들을 관리</u>했지만 <span style="color:royalblue">이제는 서버로 관리</span>하기 때문에 <span style="color:tomato">안정적</span>이고 <span style="color:tomato">즉각적</span>이다.  

## 3. Public DNS
클라이언트 컴퓨터는 그럼 어떻게 DNS Server의 IP 주소를 알고있는 것일까?  
우리가 컴퓨터에 인터넷을 연결하면 DNS Server의 IP 주소를 자동적으로 연결해준다.  

## 4. 도메인 이름의 구조
DNS Server에는 2가지 역할이 존재한다.  
첫 번째는 서버로 사용될 컴퓨터가 자신의 이름과 IP 주소를 DNS Server에 제출하는 것이고  
두 번째는 클라이언트로 사용될 컴퓨터가 DNS Server에게 이름을 물어보면 IP 주소를 알려주는 것이다.  

<img src="https://user-images.githubusercontent.com/87808288/179775654-d4c79820-927f-4502-9d25-0eca7b882df0.png" width="80%">  
`DNS Server`는 한 대의 컴퓨터가 모두 관리하는 것이 아니다.  
각 부분마다 DNS Server 컴퓨터가 <u>나누어져 관리한다</u>.  

또한 <span style="color:blue">상위가 하위를 알고 있어야</span>한다.  
<u>Root 도메인을 담당하는 서버</u>는 <span style="color:royalblue">하위</span>라고 할 수 있는 <span style="color:royalblue">Top-level 도메인을 담당하는 서버</span>들의 <span style="color:blue">목록을 알고 있어야</span> 한다.  
하지만 Root는 Second-level을 알지는 못한다.  

IP 주소가 아닌 도메인 이름으로 접속하면  
Root 도메인을 담당하는 서버는 .com으로 끝나기 때문에 그에 맞는 Top-level 도메인을 담당하는 서버의 IP를 알려주고  
Top-level 도메인을 담당하는 서버는 example.com.으로 끝나기 때문에  
그에 맞는 Second-level 도메인을 담당하는 서버의 IP 주소를 알려준다.  
그렇게 최종적으로는 sub 도메인을 담당하고 있는 네임 서버에 접속하게 된다.  
<img src="https://user-images.githubusercontent.com/87808288/179777415-aef12414-052a-41f2-a37b-1bac88e30bb4.png" width="80%">  

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
