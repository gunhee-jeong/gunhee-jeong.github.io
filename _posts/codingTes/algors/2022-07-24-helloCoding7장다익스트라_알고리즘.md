---
layout: single
title: "Hello Coding-> 7장 다익스트라 알고리즘"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-24T21:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 7장 다익스트라 알고리즘
## 1. 너비 우선 탐색 VS 다익스트라 알고리즘
<u>최단 경로</u>와 <u>더 빠른 경로</u>는 다를 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/180646475-7788ff4b-385f-47a5-b1a8-9eb4dff5d3b9.png" width="40%">  
`너비 우선 탐색`을 사용했을 때는, <span style="color:white;background:royalblue;">가장 적은 수의 구간을 가지는 경로</span>를 찾았다.  
하지만 위의 이미지와 같이 <span style="color:white;background:royalblue;">가장 빠른 경로</span>를 찾고 싶다면 <span style="color:white;background:tomato;">다익스트라 알고리즘</span>을 사용해야한다.  

## 2. 다익스트라 알고리즘
각 구간은 분 단위로 표시한 이동 시간을 가진다.  
<img src="https://user-images.githubusercontent.com/87808288/180646642-dc6e61b2-0773-44e4-96d6-94cda5c741e0.png" width="30%">  

다익스트라 알고리즘은 4 단계로 이루어진다.  
1. 가장 "가격"이 "싼" 정점을 찾는다.  
가장 가격이 싼 정점이란 도달하는 데 시간이 가장 적게 걸리는 정점을 의미한다.  
2. 이 정점의 이웃 정점들의 가격을 조사한다.  
3. 그래프 상의 모든 정점에 대해 이러한 일을 반복한다.
4. 최종 경로를 계산한다.

<u>1번</u>에서 가장 싼 정점을 찾는다고 했다.  
지금까지는 A와 B 중에서 정점 B가 가장 가까우며 2분이 걸린다.  
<img src="https://user-images.githubusercontent.com/87808288/180646797-c784abf1-a6c5-4e25-a2f7-6bf8dfe8250a.png" width="25%">  

<u>2번</u> -> 정점 B의 모든 이웃 정점에 대해 정점 B를 통과하여 정점 A에 도달하는 데 걸리는 시간을 계산한다.  
<img src="https://user-images.githubusercontent.com/87808288/180647016-8d8a6384-2952-4e22-95e1-1b61ac95e179.png" width="60%">  
정점 B의 이웃 정점에 대해 더 빠른 경로를 찾으면 가격을 바꾸어준다.  
- 정점 A로 가는 더 짧은 거리(6분에서 5분으로 수정)
- 도착점까지 가는 더 짧은 거리(무한대에서 7분으로 수정)

<u>3번</u> -> 이제 <span style="color:white;background:royalblue;">지금까지 한 일을 반복</span>한다.  
다시 1단계로, 가장 빨리 도착할 수 있는 정점을 찾는다.  
<u>정점 B는 이미 처리</u>했고, <span style="color:white;background:royalblue;">정점 A가 그 다음으로 시간이 적게 걸린다</span>.  
다시 2단계로, 정점 A의 이웃 정점에 대한 가격을 수정한다.  
<img src="https://user-images.githubusercontent.com/87808288/180647401-17ed0ba6-5ddd-4584-9fb9-c72bca355cb2.png" width="35%">  
이제 도착점까지의 거리는 6분으로 줄어든다.  

위의 다익스트라 알고리즘을 통해  
- 정점 B에 도달하는 데는 2분이 걸린다.  
- 정점 A에 도달하는 데는 5분이 걸린다.
- 도착점에 도달하는 데는 6분이 걸린다.

<img src="https://user-images.githubusercontent.com/87808288/180647555-1bd05fe2-8607-4765-9fe0-bc7b818f54e2.png" width="25%">
<img src="https://user-images.githubusercontent.com/87808288/180647595-2af32206-61a9-472b-8944-438b386b51cf.png" width="30%">  
위 탐색 방식은 <span style="color:white;background:royalblue;">너비 우선 탐색으로는 찾을 수 없는 경로</span>이다.  
위의 이미지의 경로는 <span style="color:white;background:blue;">구간이 3개</span>나 되고,  
2개의 구간만으로 출발점에서 도착점으로 가는 경로도 존재하기 때문이다.  
<!-- 161 페이지 -->




<style>
.red {
  color: ivory;
  background-color: red;
}

.tomato {
  color: ivory;
  background-color: tomato;
}

.blue {
  color: ivory;
  background-color: blue;
}

.royalblue {
  color: ivory;
  background-color: royalblue;
}

.forestgreen {
  color: ivory;
  background-color: forestgreen;
}

.darkorange {
  color: ivory;
  background-color: darkorange;
}
</style>

<!-- <span style="color:white;background:royalblue;"> -->

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
