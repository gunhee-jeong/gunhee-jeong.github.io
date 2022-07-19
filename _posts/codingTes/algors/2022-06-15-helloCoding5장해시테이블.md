---
layout: single
title: "Hello Coding-> 5장 해시 테이블"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-06-15T19:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 5장 해시 테이블
## 1. 해시 함수의 소개
<u>식료품 가게에서</u> 일하고 있다면  
손님이 물건을 사러 오면 <span style="color:royalblue">모든 물건의 가격이 적힌 장부</span>를 확인해야한다.  
만약 가격 장부가 <u>알파벳 순서로 되어 있지 않다면</u> apple을 찾기 위해서 <span style="color:royalblue">모든 가격을 살펴</span>보느라 `O(n)` 시간이 걸린다.  
만약 장부가 <u>알파벳 순서로 되어 있다면</u> <span style="color:royalblue">이진 탐색</span>으로 `O(log n)` 시간이 걸린다.  

O(n)과 O(log n) 사이에는 엄청난 차이가 존재한다.  
1초에 장부 10줄을 읽을 수 있다면 단순 탐색과 이진 탐색의 시간은 아래와 같다.  
<img src="https://user-images.githubusercontent.com/87808288/179389102-49823f82-ddef-4ac6-aeb1-6ffb462cea2c.png" width="400">  

<u>이진 탐색이 엄청나게 빠르다는 것을 잘 알고 있지만</u> 가격을 찾는 동안 손님은 계속해서 밀려든다.  
그때문에 우리에게 필요한 것은 모든 물건의 <span style="color:blue">이름과 가격을 외우고 있는 동료</span>이다.  
그러면 장부는 더이상 필요가 없어진다.  
식료품 가게의 동료인 매기는 모든 항목에 대해 O(1) 실행 시간만에 가격을 알려준다.  
가격 장부의 리스트가 아무리 많아도 상관없다. 매기는 이진 탐색보다도 훨씬 빠르다.  
<img src="https://user-images.githubusercontent.com/87808288/179392212-b71603cf-689c-4908-8cce-cf484787fba7.png" width="400">  

## 2. 해시 함수
`해시 함수`는 <span style="color:blue">문자열을 받아서</span> <span style="color:tomato">숫자를 반환</span>하는 함수이다.  
<img src="https://user-images.githubusercontent.com/87808288/179392277-41f0c632-efa4-4632-8449-92f7a5878534.png" width="300">  
해시 함수는 문자열에 대해 숫자를 할당한다.  
- 해시 함수는 일관성이 있어야 한다.  
만약 "apple"을 넣었을 때 "4"를 반환한다면 "apple"을 넣을 때마다 항상 "4"를 반환해야한다.  
- 다른 단어가 들어가면 다른 숫자가 나와야 한다.  
어떤 단어를 넣어도 "1"만 나온다면 좋은 해시 함수가 아니다.  

모든 가격을 배열에 저장한다.  
"apple"의 가격을 추가한다. -> 해시 함수에 "apple"을 넣는다. -> 해시 함수는 "3"을 출력한다.  
<img src="https://user-images.githubusercontent.com/87808288/179392461-0bda32fc-86eb-4fbf-a86b-d76ccbcd90c9.png" width="300">  

해시 함수는 가격이 저장된 위치를 정확하게 알려준다.  
그렇기때문에 탐색을 할 필요가 없다.  
<img src="https://user-images.githubusercontent.com/87808288/179392517-40982185-c5b9-44bb-bf3e-327fcaf1c3be.png" width="300">  

해시 함수와 배열을 합치면 해시 테이블이라고 하는 자료구조를 만들 수 있다.  

해시 테이블은 해시 맵, 맵, 딕셔너리, 연관 배열이라는 이름으로도 알려져 있다.  

해시 테이블은 직접 구현할 일은 없다.  
대부분의 프로그래밍 언어들은 해시 테이블이 구현되어 있기 때문이다.  
(파이썬에도 딕셔너리라고 불리는 해시 테이블이 존재한다.)  

`해시 테이블`은 <span style="color:red">키key</span>와 <span style="color:red">값value</span>을 가진다.  
book이라는 해시 테이블에서 상품 이름은 키가 되고, 가격은 값이 된다.  

## 3. 해시 테이블을 사용하는 예
### (1) 해시 테이블로 조회하기
휴대폰에는 간단한 전화번호부가 들어가있다.  
각각의 이름은 관련된 전화번호를 가지고 있다.  
<img src="https://user-images.githubusercontent.com/87808288/179392656-028510cb-1211-4a50-bc15-c07a2b5800a6.png" width="400">  

- 사람의 이름과 그 사람에 관련된 전화번호를 추가한다.  
- 사람 이름을 입력하면 그 이름과 관련된 전화번호를 알려준다.  

이것은 `해시 테이블`을 표현할 수 있는 예시이다.  

### (2) 중복된 항목을 방지하기
<u>투표를 할 때는</u> <span style="color:royalblue">당연하게도 모든 사람은 단 한 번만 투표를</span> 할 수 있다.  
어떤 사람이 투표했는지 확인하기 위해 -> <u>누군가가 투표소로 오면 먼저 이름을 확인</u>하고,  
<span style="color:blue">이미 투표한 사람의 목록에 그 사람의 이름이 있는지 확인</span>하게 된다.  
이때 리스트에 이름이 있다면 -> 이미 투표를 한 사람이다.  

이렇게 사람들이 투표를 하러 들어올 때마다 투표했는지 확인하기 위해 모든 목록을 살펴보게 되는데  
더 나은 방법은 바로, <span style="color:red">해시 테이블</span>을 이용하는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/179392772-764d206e-9ee9-4bd9-abd3-6ed59df36803.png" width="300">  

<u>만약 투표한 사람의 이름</u>을 <span style="color:blue">리스트(배열)에 저장한다면</span> 리스트 전체에 대해 <span style="color:tomato">단순 탐색을 반복해야하므로 함수가 느려지게</span> 된다.  
하지만 이름을 <span style="color:red">해시 테이블에 저장</span>하면 해시 테이블에 이름이 있는지, 없는지 <u>빠르게 알려주게</u> 된다.  

### (3) 해시 테이블을 캐시로 사용하기
<u>행성에 대해 지겹게 물어보는 어린 조카</u>가 있다고 가정해보자.  
"화성은 지구에서 얼마나 떨어져 있어?", "<span style="color:royalblue">달은 얼마나 떨어져 있어?</span>"......  
<u>조카가 물어볼 때마다 구글을 검색해서 대답</u>해줘야한다.  
이렇게 질문이 들어오면, 그에 <span style="color:blue">맞는 대답을 위해 몇 분의 시간이 발생하는 것</span>이다.  
그러나 조카가 항상 "달은 얼마나 떨어져 있어?"라고 물어보는 바람에 384,000km 떨어져 있다는 것을 <u>외우게 되었다면</u>  
구글에 일일이 찾아보지도 않고 <span style="color:tomato">빠르게 답해줄 수 있다</span>.  
이렇게 <span style="color:tomato">정보를 다시 계산하지 않고 저장했다가 알려주는 것</span>이 바로 <span style="color:red">캐싱</span>이다.  

페이스북에 로그인하면 모든 내용은 사용자에게 맞추어져 있다.  
하지만 로그인하지 않았다면 로그인 밖에는 보이지 않게 된다.  
(모든 사람이 똑같은 로그인 페이지를 마주하게 된다.)  
그래서 서버는 홈페이지에 어떤 정보를 제공할지 고민할 필요 없이 홈페이지의 내용을 그냥 외워서 사용자에게 보여준다.  

캐싱은 작업 속도를 올리는 일반적인 방법이다.  
그리고 그 자료는 바로 해시 테이블에 저장된다.  

페이스북은 홈페이지만 캐싱하는 것이 아니라 회사 소개, 회사 연락처, 사용 약관 등 많은 것을 캐싱한다.  
그래서 페이지 URL에 해당 페이지의 자료를 할당한다.  
<img src="https://user-images.githubusercontent.com/87808288/179392931-73eac4cb-ecd5-407a-afd1-c671d0d683db.png" width="350">  

캐시에 URL이 없을 때만 서버가 작업을 한다.  
또 자료를 반환하기 전에는 캐시에 저장을 한다.  

[해시 테이블의 장점]  
- 어떤 것과 다른 것 사이의 관계를 모형화할 수 있다.  
- 중복을 막을 수 있다.  
- <span style="color:red">서버에게 작업을 시키지 않고 자료를 캐싱</span>할 수 있다.  

## 4. 충돌
해시 테이블의 성능을 이해하려면 우선 충돌에 대해 이해해야 한다.  

해시 함수는 서로 다른 키를 배열의 서로 다른 위치에 할당한다고 말했다.  
<img src="https://user-images.githubusercontent.com/87808288/179393021-1eb108c7-254e-4620-bc1f-705134679f10.png" width="400">  
하지만 사실 이것은 불가능하다.  
간단한 예로 26개의 공간이 있는 배열이 있다고 해보자.  

우리가 만든 해시는 첫 글자에 따라 공간을 할당하는 간단한 해시 함수이다.  
0번의 공간에 -> Apples를 넣고,  
1번의 공간에 -> Bananas를 넣었다.  
그런데 Avocados를 해시에 넣고 싶으면 첫 번째 공간에 다시 할당해야하는데  
Apples가 이미 공간을 차지해버렸다. 이런 것을 우리는 <span style="color:red">충돌</span>: collision이라고 한다.  
<img src="https://user-images.githubusercontent.com/87808288/179393105-bb27e4e8-975c-4e2f-919b-2fca84453d5d.png" width="300">  

충돌을 해결하는 가장 간단한 방법은 <span style="color:tomato">같은 공간에 여러 개의 키를 연결 리스트로</span> 만들어 넣는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/179393159-abb4693c-c417-4d5e-a424-ad75949f9574.png" width="450">  
그러나 여기서 Apples와 Avocados가 같은 공간에 할당이 되어 있으므로  
Bananas의 가격을 알고 싶다면 빨리 알 수 있지만, Apples의 가격을 알고 싶다면 시간이 더 걸리게 된다.  
(연결 리스트가 3~4개 정도면 큰 문제가 아니지만, 식료품 가게에서 A자로 시작하는 모든 상품이 들어가있다면?  
<span style="color:royalblue">결국 이렇게 해시 테이블이 느려지게</span> 된다.)  

## 5. 성능
<img src="https://user-images.githubusercontent.com/87808288/173979315-5eb79a42-90a8-4fc6-980f-ad59fa994db6.png" width="400">  
`해시 테이블`의 속도는 빠른데,  
평균적인 경우 모든 항목에 <span style="color:blue">O(1) 시간</span>이 걸린다. 이를 <span style="color:blue">상수 시간</span> constant time이라고 부르다.  

예를 들어, <u>단순 탐색</u>은 <span style="color:royalblue">선형 시간: O(n)</span>이 걸리고, <u>이진 탐색</u>은 더 빠른 <span style="color:royalblue">로그 시간: O(Log n)</span>이 걸린다.  

<img src="https://user-images.githubusercontent.com/87808288/179393282-c2f729ef-da2f-4535-a69a-527d0d3cc073.png" width="300">  
평균적인 경우, 해시 테이블의 성능을 살펴보면 탐색을 할 때는 배열만큼 빠르다.  
그리고 삽입이나 삭제 시에는 연결 리스크만큼 빠르다.  
이렇게 양쪽의 좋은 점만을 가지게 된다.  
하지만 <u>최악의 경우</u> <span style="color:royalblue">해시 테이블이 가장 느리기도</span> 하다.  
그렇기 때문에 해시 테이블에서는 <u>최악의 상황이 발생하지 않도록 하는 것이 중요</u>하다.  
그래서 <span style="color:tomato">충돌을 피해야</span> 한다.  

해시 테이블이 <u>평평한 선 모양</u>을 가질 수 있었던 이유는  
해시 테이블이 <span style="color:royalblue">하나의 항목을 가지든 10억 개의 항목을 가지든</span>  
해시 테이블에서 <span style="color:blue">무언가를 찾는 데 걸리는 시간은 항상 똑같기 때문</span>이다.  

### (1) 사용률
해시 테이블의 사용률을 구하는 것은 쉽다.  
<img src="https://user-images.githubusercontent.com/87808288/179393454-f0919e9d-7a64-4e5f-bdf9-9332e5313d49.png" width="150">  
해시 테이블은 저장을 위해 배열을 사용한다.  
아래 해시 테이블의 사용률은 2/5, 즉 0.4이다.  
<img src="https://user-images.githubusercontent.com/87808288/179393458-50420fd1-8115-4c2d-b38c-454fc56b5f5e.png" width="200">  

100개의 물건 가격을 해시 테이블에 저장해야 한다면 해시 테이블에는 100개의 공간이 있어야 한다.  
이때 해시 테이블의 사용률은 1이 된다.  
만약 해시 테이블의 공간이 50개 밖에 없다면 사용률은 2가 된다.  
공간의 수가 충분하지 않기 때문에 모든 항목이 다른 공간을 차지할 수 있는 방법은 없다.  
사용률이 1보다 크다면 배열에 공간의 수보다 항목의 수가 많다는 의미이다.  
사용률이 커지기 시작하면 해시 테이블의 공간을 추가해야하는데 이것을 리사이징이라고 한다.  

아래의 해시 테이블은 리사이징을 할 필요가 있다.  
<img src="https://user-images.githubusercontent.com/87808288/179393640-81b3ad40-9135-4177-acbe-a7ee32fe8385.png" width="200">  
우선 더 큰 배열을 생성해야하는데, 대략 두 배 정도의 크기로 배열을 만드는 것이 보통이다.  
이제 새로 만들어진 해시 테이블에 해시 함수를 사용해서 모든 항목을 다시 넣어야 한다.  
<img src="https://user-images.githubusercontent.com/87808288/179679386-76680ff1-9ff4-4abd-88c4-d1b95120931a.png" width="300">  
새로 만들어진 해시 테이블의 사용률은 3/8이다.  
사용률이 낮을수록 충돌이 적게 일어나며 해시 테이블의 성능도 좋아진다.  
보통은 사용률이 0.7보다 커지면 리사이징을 실시한다.  

### (2) 좋은 해시 함수란
좋은 해시 함수란 배열에 값을 고루 분포시키는 함수이다.  
<img src="https://user-images.githubusercontent.com/87808288/179680892-2d74771e-0b07-43f7-8709-4fe3fe23de57.png" width="300">  
나쁜 해시 함수는 값들이 뭉쳐져 있어서 충돌이 자주 발생한다.  
<img src="https://user-images.githubusercontent.com/87808288/179680920-7a6e5870-e115-44e7-9ef0-95804c6d0f8c.png" width="300">  

<!-- <span style="color:royalblue"> -->

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
