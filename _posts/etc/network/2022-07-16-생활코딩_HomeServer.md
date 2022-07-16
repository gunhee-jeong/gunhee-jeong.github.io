---
layout: single
title: "생활코딩 -> Home server"
# categories: Git
categories:
  - network # HTML CSS JavaScript Server Algorithm Wecode Programmers CS vsCode
tag: [생활코딩, web] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-16T18:00:00+09:00   
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---  
# Home server
인터넷의 흥행을 예상치 못했기에 준비했던 <u>IP 주소는 동나버리고</u> 말았다.  
이런 IPv4를 대체하여 그 <u>증가된 IP 주소</u>를 가지고 온 것이 바로 <span style="color:royalblue">IPv6</span>인 것이다.  
또한 이런 <u>IP 주소를 아껴쓰기 위한</u> 것 중 하나가 바로 <span style="color:red">공유기</span>인 것이다.  
공유기를 사용하면 <span style="color:tomato">하나의 IP 주소를 나누어 사용할 수 있게 된다.  

## 1. 공유기(router)
### (1) IP address
랜선을 연결하거나 wifi에 접속하면 자동적으로 <span style="color:red">IP</span> 주소를 받게된다.  
그런데 기존에는 컴퓨터 한 대였지만, 이제는 <u>스마트폰, 노트북, 테블릿 등 많은 제품을 사용</u>하게 되었다.  
이론적인 방법으로는 통신사에 회선을 하나더 계약하는 것이다.  
그런데 당연하게도 비싸기 때문에 다른 방법을 찾기 시작한 것이다.  

통신사 등에서 하나의 회선을 계약하고 ->  
<span style="color:red">공유기</span>라는 제품을 준비하고  
<u>통신사에서 받은 케이블</u>을 <span style="color:blue">WAN</span>에 꽂아주게 된다.  
그렇게 원래 컴퓨터에 꽂아있던 케이블을 공유기에 연결하면 통신사로부터 발급받은 IP address는 공유기의 것이 된다.  
<span style="color:royalblue">59.6.66.238에 접속하면</span> 더이상 컴퓨터에 접속하는 것이 아니라 <span style="color:blue">공유기로 접속할 수 있게</span> 되는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/179349246-eaa8e08b-f6a0-4749-8c7f-2e0af3f265f6.png" width="600">  
이렇게 연결된 스마트폰, 노트북 등을 <span style="color:red">LAN</span>(Local Area Network) 네트워크라고 한다.  
또한 이 공유기는 <span style="color:red">광역 네트워크(WAN)</span>에 소속되어있다.  
그래서 `공유기`는 LAN과 WAN의 사이에서 <span style="color:royalblue">교환원 같은 역할</span>을 해주는 기계인 것이다.  


<img src="https://user-images.githubusercontent.com/87808288/179349441-937c165b-f52a-4b58-9457-d2dec72fa5ee.png" width="500">  
<u>공유기와 연결된 기기들</u>은 모두 <span style="color:royalblue">각각 IP 주소를 부여</span>받는다.  
또한 <u>공유기 자체도 네트워크의 일부</u>이므로 <span style="color:royalblue">IP 주소를 부여</span>받는다.  
공유기가 받은 이 <u>IP 주소는 중요한 역할</u>을 하므로 특수한 이름이 주어지는데 바로  
<span style="color:blue">Gateway address</span> 또는 <span style="color:blue">Router address</span>로 불린다.  

위 이미지에서 <span style="color:blue">WEN</span>의 IP 주소 59.6.66.238은 <u>누구나 접속 가능하다</u>는 의미로  
<span style="color:tomato">public IP address(공용 IP 주소)</span>라고 부르고  
<u>안의 컴퓨터들에게 부여된 IP</u>들은 <span style="color:royalblue">내선번호</span>라고 생각하면 된다.  
그래서 이렇게 <span style="color:blue">LAN 안에서만 사용</span>할 수 있는 IP address를 <span style="color:tomato">Private IP address(사설 IP 주소)</span>라고 부른다.  

## 2. NAT(Network Address Translation)
노트북으로 <u>어떠한 사이트에 접속한다면</u> 공유기는 이 요청을 인지하게 된다.  
A라는 사이트는 LAN 안에는 존재하지 않기 때문에 <span style="color:royalblue">이 요청을 WAN으로</span> 넘기게 된다.  

이때 <u>WAN으로 넘기기 위해서는 2가지의 일을</u> 필요로 한다.  
첫 번째는 우선 <span style="color:blue">192.168.0.4가 요청했다는 사실을 기록</span> 남겨야하고,  
<img src="https://user-images.githubusercontent.com/87808288/179350478-cf76782d-ee2e-452f-a524-89a37ef8720b.png" width="600">  
두 번째는 <u>192.168.0.4라는 IP</u> 주소는 <span style="color:royalblue">사설 IP 주소</span>이기 때문에 외부에서 접속할 수 없기에  
192.168.0.4라는 <span style="color:blue">IP 주소를 59.6.66.238로 변경</span>한 다음에 그 변경된 IP 주소를 A라는 사이트로 보내게 되는 것이다.  
그러면 다시 A라는 사이트는 59.6.66.238 이라는 IP 주소로 다시 응답을 보낸다.  
이러한 방법으로 사설 IP를 사용하고 있는 컴퓨터가 사설 IP 바깥에 해당하는 public IP라고 하는 외부에  
접속할 수 있게 되고 이때 사용되는 기술이 바로 <span style="color:red">NAT</span>인 것이다.  

## 3. IP 주소 알아내기
### (1) mac
환경설정 -> 네트워크 -> 초록색 불이 들어온 부분이 현재 연결된 부분이다.  
그것을 선택하고 밑에 "고급" 버튼을 클릭한다.  
이제 TCP/IP에 들어가면 보이는 IPv4가 바로 IP address이다.  
그리고 router라고 되어있는 부분이 바로 공유기의 IP address이다.  

## 4. port
우리의 컴퓨터를 서버로 사용하여 외부(WAN)의 사람이 우리의 컴퓨터에 도달하려면 어떠한 방법을 사용해야할까?  
59.6.66.238이라는 IP 주소에 접속을 해보았자  
어느 내선(LAN)으로 가야하는지 알 수 없기 때문이다.  

65535에 달하는 포트 중에서 0 ~ 1023까지는 Well-known port(예약된 포트)라고 하여  
우리가 web을 사용하게 되면 80번 포트로 자동적으로 연결되도록 설정되어있다.  
<img src="https://user-images.githubusercontent.com/87808288/179351545-91d07c3c-f9a5-4faa-a4dc-55da2ce18de2.png" width="700">  
만약 web 서버가 2개라면 url 뒤에 포트번호를 추가로 기입하여 해당 web 서버의 포트로 이동할 수 있다.  

### (1) port forwarding
59.6.66.238:8081로 접속하면 -> 192.168.0.4:80으로 연결하는 것을 말한다.  
<img src="https://user-images.githubusercontent.com/87808288/179352306-ec58f728-ed41-4c80-b145-02e8534ead43.png" width="700">  
공유기는 이렇게 59.6.66.238 IP 주소로 접속하고 어떤 포트로 연결되느냐에 따라서 사설 IP 주소로 연결시켜준다.  

## 5. Dynamic & Static IP address
ISP(인터넷 서비스 제공자)는 IP를 오랜시간 사용하지 않으면 IP를 회수해 다른 곳에 이 IP를 주게 된다.  
그러다가 회수한 곳에서 다시 접속하게 되면 새로운 IP를 전달하게 된다.  
이렇게 동적으로 바뀌게 되는 IP 주소를 -> Dynamic IP address라고 한다.  

Static IP address는 반대로 이 IP 주소를 고정하는 것을 말한다.  

## 6. DHCP
Dynamic Host Configuration Protocol  
IP 주소를 세팅하는 방법  

<img src="https://user-images.githubusercontent.com/87808288/179353050-594d510f-9e65-4b03-b7ea-4faf1fa3fb4b.png" width="700">  
<img src="https://user-images.githubusercontent.com/87808288/179353084-0166a2a3-48b5-4fcb-9015-7f91a7d00b2a.png" width="700">  
<img src="https://user-images.githubusercontent.com/87808288/179353124-68dd5ebc-ebd4-4ffd-a36a-61cd41812074.png" width="700">  
<img src="https://user-images.githubusercontent.com/87808288/179353184-1afaeb85-1f64-4f5e-b6ec-299fc3f9b2ca.png" width="700">  
<img src="https://user-images.githubusercontent.com/87808288/179353238-d0644e0b-513c-4892-8aa9-0015768082ac.png" width="700">  

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
