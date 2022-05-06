---
layout: single
title: "6장 네트워크의 규칙, 7장 OSI모델과 TCP/IP모델, 8장 캡슐화와 역캡슐화"   
# categories: Git
categories:
  - network # HTML CSS JavaScript Server Algorithm Wecode Programmers CS vsCode
tag: [모두의 네트워크, 프로토콜(protocol), OSI, TCP/IP, 캡슐화, VPN] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-04-25T11:30:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---  
# 네트워크의 규칙  
## 프로토콜이란?  
일상생활에서 <u>지켜야 할 규칙</u>이 존재하듯이,  
네트워크에서도 문제없이 통신하려면 이러한 <span style="color:blue">규칙</span>을 지켜야 한다.  
서로 다른 언어를 사용하면 대화를 할 수 없듯이, 통신을 위해서도 `서로 알아들을 수 있는 언어`로 대화해야한다.   
이러한 규칙을 <span style="color:red">프로토콜(protocol)</span>이라고 부른다.  
프로토콜은 컴퓨터 간에 정보를 주고받을 때의 <span style="color:blue">통신 방법에 대한 규칙이나 표준</span>이다.  

# OSI 모델과 TCP/IP 모델  
## OSI 모델  
지금은 상상할 수 없겠지만, 같은 회사의 컴퓨터끼리만 통신할 수 있던 시절이 존재했다.  
(삼성 <--> 삼성, 애플 <--> 애플)  
거기에다가 케이블을 연결하는 커넥터까지 회사별로 다르면서 표준 규격의 필요성을 인지하게 된다.  
이러한 표준 규격을 정하는 여러 단체가 존재하는데, 그 중에서도 <span style="color:red">ISO</span>라는 <u>국제표준화기구</u>가 있었고  
이 단체는 <span style="color:red">OSI 모델</span>이라는 표준 규격을 제정했다.  

데이터의 송수신은 컴퓨터에서 컴퓨터로 데이터를 전송하는 것으로  
이때 컴퓨터 내부에서는 여러 가지 일들이 일어난다.  
이런 일을 일곱 개 계층으로 나눠서 이루어지는데 -> 이것이 바로 OSI 모델이다.  
<img src="https://user-images.githubusercontent.com/87808288/165018916-ad460a58-37c8-41ff-b66d-f3b1acf8aec0.png" width="300"><img src="https://user-images.githubusercontent.com/87808288/165022115-5729a229-007a-4ad1-bfae-754c4940490f.png" width="400">  
통신할 때 데이터는 -> 맨 위의 응용 계층에서 순차적으로 아래 계층으로 전달된다.  
데이터를 전송하는 쪽(송신)은 데이터를 보내기 위해서 상위 계층에서 -> 하위 계층으로 데이터를 전송하고  
각 계층은 독립적이므로 데이터가 전달되는 동안에 다른 계층의 영향을 받지 않는다.  
데이터를 받는(수신)쪽은 하위 계층에서 상위 계층으로 각 계층을 통해 전달된 데이터를 받게 된다.  

## TCP/IP 모델  
OSI 모델의 7계층을 4계층으로 바꾼 4계층의 모델이 바로 TCP/IP 모델이다.  
TCP/IP 모델의 4계층에는 <span style="color:red">응용</span> 계층, <span style="color:red">전송</span> 계층, <span style="color:red">인터넷</span> 계층, <span style="color:red">네트워크 접속</span> 계층이 있다.  

# 캡슐화와 역캡슐화  
## 캡슐화와 역캡슐화란  
데이터를 보낼 때는 `데이터의 앞부분에 전송하는 데 필요한 정보를 붙여서` 다음 계층으로 보내야한다.  
이 정보를 <span style="color:red">헤더</span>라고 하는데, 헤더는 <u>데이터를 전달받을 상대방에 대한 정보도 포함</u>되어 있다.  
헤더 <-(필요한 정보)(송신 데이터)  
이처럼 헤더를 붙여 나가는 것을 <span style="color:red">캡슐화</span>라고 한다.  
그리고 데이터를 받는 쪽에서는 헤더를 하나씩 제거해야하는데 -> 이것을 <span style="color:red">역캡슐화</span>라 한다.  
<img src="https://user-images.githubusercontent.com/87808288/165023438-39a90cee-d38a-48be-9011-fa32cb98aa67.png" width="600">   
> `응용 계층`에서 웹 사이트를 접속하기 위한 <u>요청 데이터가 만들어지고</u> ->   
`전송 계층`에서 신뢰할 수 있는 통신이 이루어지도록 <u>응용 계층에서 만들어진 헤더가</u> 붙는다 ->  
그리고 전송 계층에서 만들어진 데이터를 다른 네트워크와 통신하기 위해 `네트워크 계층`에서 헤더를 붙인다 ->  
또 네트워크 계층에서 만들어진 데이터에 물리적인 통신 채널을 연결하기 위해  
`데이터 링크 계층`에서 <u>헤더와 트레일러</u>를 붙인다.  

이렇게 <span style="color:blue">전송 계층 헤더</span>, <span style="color:blue">네트워크 계층 헤더</span>, <span style="color:blue">데이터 링크 계층 헤더</span> 그리고 <span style="color:blue">트레일러</span>가 추가되었다.  
> OSI 모델에서 데이터 송신 측은 응용 계층 -> 전송 계층 -> 네트워크 계층 -> 데이터 링크 계층 순서로 캡슐화가 진행   
반대로 수신 측은 데이터 링크 계층 -> 네트워크 계층 -> 전송 계층 -> 응용 계층 순으로 역캡슐화가 진행  

[트레일러]  
트레일러는 데이터를 전달할 때 데이터의 <u>마지막에 추가하는 정보</u>를 말한다.  

이렇게 데이터 링크 계층에서 만들어진 데이터는 최종적으로 <span style="color:red">전기 신호</span>로 변환돼서 수신 측에 도착한다.  
이렇게 필요한 데이터를 추가해 나가는 것을 캡슐화라고 한다.  

수신 측은 각 계층의 헤더를 제거하면서 데이터를 전달하고 있다. 아까와는 반대로 데이터 링크 계층부터  
순서대로 <u>상위 계층으로 전달</u>하고 있다.  
(송신 측의 데이터 링크 계층에서 추가된 헤더와 트레일러를 수신 측인 데이터 링크 계층에서 제거함)  

[VPN]  
VPN은 Virtual Private Network(가상 사설망)의 약어이다.  
가상 통신 터널을 만들어 기업 본사나 지사와 같은 거점 간을 연결하여 통신하거나 외부에서 인터넷으로  
사내에 접속하는 것을 말한다.  
예를 들어 서울에 본사가 있고 부산에 지사가 있다면 본사 내부 랜에서 지사 내부 랜에 접속하여  
통신하는 것은 물리적인 거리가 멀어 어렵다. 이럴 때는 VPN을 사용하여 본사와 지사를 연결하여 통신한다.  
> 인터넷 VPN  
>> 인터넷 VPN에는 거점 간 접속과 원격 접속 연결이 있다. 둘 다 일반 인터넷망을 사용한다.   
거점 간 접속은 IPsec이라는 암호 기술 프로토콜을 사용하여 접속한다.  
반면 원격 접속 연결은 외부에서 사용하는 컴퓨터와 사내 네트워크를 연결하기 때문에  
암호화된 통신로를 만든다.    

> IP-VPN  
>> IP-VPN은 MPLS라는 기술을 사용하며 인터넷망이 아닌 통신 사업자 전용 폐쇄망을 사용한다.  
MPLS는 폐쇄망을 사용하기 때문에 제삼자에 의한 해킹이나 데이터 변조의 위험이 없어   
암호화 기능이 필요하지 않는다.  



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
