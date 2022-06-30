---
layout: single
title: "Hello Coding-> 1장 알고리즘의 소개"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-10T06:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1장 알고리즘의 소개
## 1. 들어가는 글
### (1) 성능에 대해 알아야 하는 것들
프로그래밍 언어로 <u>대부분의 알고리즘은 이미 구현</u>이 되어있다.  
따라서 우리는 스스로 <span style="color:royalblue">모든 알고리즘을 코딩해야할 필요는 없는 것</span>이다.  
하지만 여러 가지 <u>알고리즘들의 차이점을 이해하지 못한다면</u> 미리 <span style="color:blue">구현해 놓은 알고리즘은 쓸모가 없어진다</span>.  

알고리즘들의 차이점을 이해하고,  
병합 정렬을 사용할 것인지 퀵 정렬을 사용할 것인지  
그리고 단순히 다른 자료구조를 사용하는 것만으로도 성능이 크게 달라진다.  

## 2. 이진 탐색
전화번호부로 누군가의 번호를 찾는다고 생각해보자.  
찾는 사람의 이름이 K로 시작한다면 어떻게 찾는 것이 효율적일까.  
한 장씩 앞에서 부터 찾는 방법도 있지만, 이 방법보다는 책 한 가운데를 펼치는 방법을 사용할 수 있다.  
(전화번호부의 중간쯤에 K가 있을테니까!)  

위의 문제같은 경우를 <span style="color:royalblue">탐색 문제</span>라고 한다.  
그리고 위의 예를 들었던 경우에는 "<span style="color:red">이진 탐색</span>"이라고 하는 알고리즘을 사용할 수 있다.  

<img src="https://user-images.githubusercontent.com/87808288/176601208-9a6e6cac-9eec-475c-b68d-281922bbf817.png" width="500">  
숫자를 추측할 때마다 그 숫자가 너무 작은지, 너무 큰지, 맞는 숫자인지 알 수 있다.  
그런데 <u>1부터 순서대로 모두 추측</u>하는 것을 "<span style="color:tomato">단순 탐색</span>"이라고 한다.   

### (1) 더 좋은 탐색 방법
100의 중간, 즉 50부터 시작하는 것이다.  
"50이 너무 작다"는 대답 하나로 숫자의 절반이 답이 아니라는 것을 알 수 있게 된다.  
1부터 50까지의 숫자는 너무 작다고 하니 -> 이번에는 남은 51과 100까지의 숫자 중 중간에 속하는 75로 추측하자.  
"75가 너무 크다"는 대답으로 75보다 같거나 큰 숫자들은 제외할 수 있게 되었다.  

이진 탐색에서는 매번 남은 숫자 중의 가운데 숫자를 말하고 대답에 따라 그보다 큰 숫자 작은 숫자들을  
한꺼번에 없앨 수 있다.  

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const item = 10;

let low = 0;
let high = arr.length - 1; //탐색의 끝점 -> 9
let mid = 0;
let guess = 0;

while(true) {
  mid = parseInt((low + high) / 2); //parseInt(4.5) -> 4
  guess = arr[mid]; //2

  console.log(`mid-> ${mid}`); //'mid-> 4' 'mid-> 7' 'mid-> 8' 'mid-> 9'
  console.log(guess); //5 8 9 10

  if(guess === item) break;
  else if(guess > item) high = mid;
  else if(guess < item) low = mid + 1;
}
```

위의 코드와 같이 <u>이진 탐색은</u> 리스트들의 <span style="color:tomato">원소들이 정렬되어 있어야만 사용</span>할 수 있다.  


### (2) 로그
<span style="color:tomato">log<sub>10</sub> 100</span>이라는 수는 <u>"10"을 몇 번 곱해야 100일 될까</u>라고 묻는 것과 같다.  
10 * 10 == 100 이므로 답은 2가 된다.  
즉 <span style="color:red">로그</span>는 <span style="color:tomato">거듭제곱의 반대말</span>이다.  
<span style="color:red">빅오 표기법</span>에서 실행 시간을 나타내는 모든 log 함수는 <span style="color:red">log<sub>2</sub></span>를 뜻한다.  

단순 검색으로 element를 찾을 때, 최악의 경우 모든 원소를 살펴봐야 한다.  
이진 탐색을 사용하면 최악의 경우에는 log n개의 숫자만 확인하면 된다.  
<u>리스트에 숫자가 8개</u> 있다면 2<sup>3</sup> == 8, 즉 <span style="color:tomato">log 8</span> == <u>3이므로 3번만 확인</u>하면 된다.  
<u>원소가 1024개</u>이면 2<sup>10</sup> == 1024, 즉 <span style="color:tomato">log 1024</span> = <u>10이므로 숫자 10개만 확인</u>해도 충분하다.  

### (3) 실행시간
위의 상황에서 <u>1번부터 차례로 1 2 3 4 5... 10</u> 이렇게 순차적으로 정답을 유추하는 방법으로  
걸리는 시간을 <span style="color:red">선형 시간</span>이라고 한다.  
배열안에 100개의 숫자가 담겨있다면 100번을 유추해야하고, 40억 개의 숫자가 담겨있다면 40억 번을 유추해야하는 것이다.  

하지만 <span style="color:red">이진 탐색</span>은 다르다.  
<u>100개의 숫자</u>가 담겨있다면 -> `7번`, <u>40억 개</u>라고 해도 -> <span style="color:blue">32번만 유추하면 정답을</span> 찾을 수 있는 것이다.  
이진 탐색은 <span style="color:red">단순 탐색보다 아주 빠르다</span>.  

## 3. 빅오 표기법
<span style="color:red">빅오 표기법</span>은 <span style="color:tomato">알고리즘이 얼마나 빠른지 표시</span>하는 특별한 방법이다.  

### (1) 알고리즘 실행 시간이 증가하는 속도가 다르다면?  
원소의 개수가 증가해도 이진 탐색에 걸리는 시간은 얼마 늘어나지 않는다. 하지만 단순 탐색의 시간은 엄청나게 증가한다.  
그러므로 원소의 개수가 커질수록 이진 탐색은 단순 탐색보다 훨씬 빨라지게 된다.  

<u>원소 하나를 확인하는 데 1초</u>가 걸린다고 가정하자.  
`단순 탐색`을 사용하면 <span style="color:royalblue">100개의 원소를 확인</span>하는 데 <span style="color:blue">100초</span>가 소요된다.  
`이진 탐색`을 사용하면 7개(<span style="color:red">log<sub>2</sub></span> <u>100은 약 7</u>)의 원소만 확인하면 되니까 <span style="color:blue">7초</span>가 걸린다.  
그런데 실제로는 리스트에 10억 개 이상의 원소가 있을 수 있다.  

<span style="color:royalblue">10억 개의 원소</span>에 대해 `이진 탐색`을 실행한 결과 -> <span style="color:blue">30초</span>가 걸렸다.  
<span style="color:royalblue">100개의 원소</span>로 실행했을 때 <u>이진 탐색은 7초</u>, <u>단순 탐색은 100초</u>가 걸렸으므로 <span style="color:blue">이진 탐색이 15배</span> 빠르고  
30 * 15 == 450초가 걸릴 것이라고 생각할 수 있다.  
하지만 이는 <span style="color:tomato">완전히 잘못된 생각</span>이다.  
<span style="color:blue">10억 개의 원소</span>에 대한 `단순 탐색` 실행 시간은 <u>10억 초</u>로, <span style="color:red">약 11일</span>이다.  
`이진 탐색과 단순 탐색의 실행 시간이 같은 비율로 증가하지 않기 때문`이다.  

<u>원소의 개수가 증가</u>해도 `이진 탐색`에 걸리는 <span style="color:blue">시간은 얼마 늘어나지 않는다</span>.  
하지만 `단순 탐색`의 시간은 <span style="color:blue">엄청나게 증가</span>하게 된다.  
그래서 <u>알고리즘의 실행 시간이 얼마나 걸리는지만 고려할 것이 아니라</u>,  
<span style="color:tomato">리스트의 크기가 증가할 때 어떻게 증가하는지를 파악</span>할 필요가 있는 것이다.  
<span style="color:red">빅오 표기법을 사용하는 이유</span>가 바로 이 때문이다.  

<img src="https://user-images.githubusercontent.com/87808288/176609911-595bcdab-03e4-473a-83de-0832c332d390.png" width ="500">  
<span style="color:red">빅오 표기법</span>은 <span style="color:tomato">알고리즘이 동작하기 위해 필요한 연산 횟수</span>를 나타낸다.  


### (2) 여러 가지 빅오 실행 시간 살펴보기
`A 알고리즘`은  
<u>한 번에 하나씩</u> 총 16개의 네모 칸을 만든다.  
총 16개의 네모 칸을 만들어야 하니까 한 번에 하나의 상자를 만들면 몇 번의 연산이 필요할까?  

`B 알고리즘`은  
<u>종리를 한 번 접는 것이 하나의 연산</u>이다.  
이렇게 하면 한 번의 종이 접기로 두 개의 박스가 생긴다.  
이렇게 네 번 접은 종이를 펼치면 <span style="color:royalblue">4번의 연산으로 16개의 네모 칸</span>을 만들 수 있다.  

`A 알고리즘`의 실행 시간은 <span style="color:red">O(n)</span>시간, `B 알고리즘`의 실행 시간은 <span style="color:red">O(log n)</span> 시간이다.  

### (3) 최악의 실행 시간을 나타내는 빅오 표기법
전화번호부에서 사람을 찾기 위해 단순 탐색을 사용하고 있다면,  
그리고 `단순 탐색`의 실행 시간이 <span style="color:red">O(n)</span> 시간이란 것은 <span style="color:tomato">최악의 경우</span>,  
즉 <u>전화번호부의 모든 사람의 이름을 확인하는</u> 경우를 뜻한다.  

`단순 탐색`의 <span style="color:blue">실행 시간은 어떠한 경우에도 O(n)</span> 시간이다.  
<u>Adit 이라는 이름의 경우, 한 번에 찾기는 했지만</u> <span style="color:royalblue">최선의 경우이고</span>  
<span style="color:red">빅오 표기법</span>은 <span style="color:tomato">최악의 경우를 나타내기 때문</span>이다.  
이것은 <span style="color:blue">단순 탐색이 절대로 O(n) 시간보다 느려지지 않는다는 것을 보장</span>하게 된다.  

### (4) 많이 사용하는 빅오 실행 시간의 예
`O(log n)`, 로그 시간: 이진 탐색  
`O(n)`, 선형 시간: 단순 탐색  
`O(n * log n)`: 퀵 정렬  
`O(n<sup>2</sup>)`: 선택 정렬  
`O(n!)`: 외판원 문제  

위의 다섯 가지의 알고리즘을 가지고 16개의 네모 칸을 만드는 문제를 다시 한 번 접근해보자.  
첫 번째 알고리즘을 사용하면 격자를 완성하는데 O(log n) 시간이 걸린다.  
1초에 10번의 연산을 할 수 있다면 16개의 네모 칸을 완성하는 데 4(log 16 == 4)번의 연산이면 되므로  
약 0.4초가 걸리게 된다.  
먄약 1024개의 네모 칸을 그려야 한다면 10(log 1024 == 10)번의 연산이 필요하므로 1초가 걸리게 된다.  

`알고리즘의 속도`는 <u>시간이 아니라</u> <span style="color:tomato">연산 횟수가 어떻게 증가하는지로 측정</span>하게 된다.  
이렇게 하면 <span style="color:blue">입력 데이터의 크기가 늘어날 때</span> <u>알고리즘의 실행 속도가 얼마나 증가하는지</u> 알 수 있다.  
<span style="color:red">O(log n)</span>는 O(n)보다 빠르고, <span style="color:blue">찾으려는 리스트의 원소의 개수가 증가하면 상대적으로 더 빨라진다</span>.  
<img src="https://user-images.githubusercontent.com/87808288/176619482-58339468-6f6b-4f04-8e70-97c451e7508f.png" width="300">  

### (5) 외판원 문제
실행 시간이 O(n!) 시간인 알고리즘은 없다고 생각할 수 있겠지만, 그렇지 않다.  
정말 실행 시간이 느린 알고리즘도 존재한다.  

외판원은 다 섯 개의 도시를 방문해야 한다.  
가장 짧은 거리로 다섯 개의 도시를 방문하고자 한다.  
<img src="https://user-images.githubusercontent.com/87808288/176619855-76c3629c-1fc2-4cbc-96c5-1cff3cc3e94d.png" width="200">  

이 문제를 푸는 한 가지 방법은 도시를 방문하는 모든 경로를 살펴보는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/176620086-cc30f158-8e9f-4090-aec6-253e0d67e427.png" width="400">  
그 다음 전체 거리를 더해서 가장 짧은 경로를 택하면 된다.  
도시가 5개이면 120 가지 경우의 수, 도시가 6개라면 720개의 경우의 수,  
도시가 7개라면 연산 횟수는 5040번이 된다.  

만약 n개의 도시가 있다면 결과를 계산하는 데 n!(n 팩토리얼)번의 연산이 필요하다.  
만약 100개 이사으이 도시를 돌아야 한다면 사실상 계산이 불가능하게 된다.  

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
