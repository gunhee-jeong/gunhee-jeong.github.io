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
## 3. 해시 테이블을 사용하는 예
### (1) 해시 테이블로 조회하기
휴대폰에는 간단한 전화번호부가 들어가있다.  
각각의 이름은 관련된 전화번호를 가지고 있다.  

- 사람의 이름과 그 사람에 관련된 전화번호를 추가한다.  
- 사람 이름을 입력하면 그 이름과 관련된 전화번호를 알려준다.  

이것은 `해시 테이블`을 표현할 수 있는 예시이다.  

### (2) 중복된 항목을 방지하기
<u>투표를 할 때는</u> <span style="color:royalblue">당연하게도 모든 사람은 단 한 번만 투표를</span> 할 수 있다.  
어떤 사람이 투표했는지 확인하기 위해 -> <u>누군가가 투표소로 오면 먼 이름을 확인</u>하고,  
<span style="color:blue">이미 투표한 사람의 목록에 그 사람의 이름이 있는지 확인</span>하게 된다.  
이때 리스트에 이름이 있다면 -> 이미 투표를 한 사람이다.  

이렇게 사람들이 투표를 하러 들어올 때마다 투표했는지 확인하기 위해 모든 목록을 살펴보게 되는데  
더 나은 방법은 바로, <span style="color:red">해시 테이블</span>을 이용하는 것이다.  

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

캐시에 URL이 없을 때만 서버가 작업을 한다.  
또 자료를 반환하기 전에는 캐시에 저장을 한다.  

[해시 테이블의 장점]  
- 어떤 것과 다른 것 사이의 관계를 모형화할 수 있다.  
- 중복을 막을 수 있다.  
- <span style="color:red">서버에게 작업을 시키지 않고 자료를 캐싱</span>할 수 있다.  

## 4. 충돌
해시 테이블의 성능을 이해하려면 우선 충돌에 대해 이해해야 한다.  

해시 함수는 서로 다른 키를 배열의 서로 다른 위치에 할당한다고 말했다.  
하지만 사실 이것은 불가능하다.  
간단한 예로 26개의 공간이 있는 배열이 있다고 해보자.  
우리가 만든 해시는 첫 글자에 따라 공간을 할당하는 간단한 해시 함수이다.  
0번의 공간에 -> Apples를 넣고,  
1번의 공간에 -> Bananas를 넣었다.  
그런데 Avocados를 해시에 넣고 싶으면 첫 번째 공간에 다시 할당해야하는데  
Apples가 이미 공간을 차지해버렸다. 이런 것을 우리는 <span style="color:red">충돌</span>: collision이라고 한다.  

충돌을 해결하는 가장 간단한 방법은 <span style="color:tomato">같은 공간에 여러 개의 키를 연결 리스트로</span> 만들어 넣는 것이다.  
그러나 여기서 Apples와 Avocados가 같은 공간에 할당이 되어 있으므로  
Bananas의 가격을 알고 싶다면 빨리 알 수 있지만, Apples의 가격을 알고 싶다면 시간이 더 걸리게 된다.  



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
