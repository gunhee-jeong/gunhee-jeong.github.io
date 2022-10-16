---
layout: single
title: "Hello Coding 알고리즘, 4장 퀵 정렬"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-23T20:50:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.crimson {
  color: crimson;
  font-weight: bold;
}

.mediumblue {
  color: mediumblue;
  font-weight: bold;
}

.forestgreen {
  color: forestgreen;
  font-weight: bold;
}

.black {
  color: black;
  font-weight: bold;
}
</style>

# Hello Coding 알고리즘, 4장 퀵 정렬
# 🔴 분할 정복
분할 정복 전략은 문제를 푸는 새로운 방식을 제시한다.

아래의 토지를 정사각형으로 나누고자 한다.  
<img src="https://user-images.githubusercontent.com/87808288/177139817-0faf82e7-c480-40c9-af75-dc875a5af7ad.png" width="50%">  
<u>정사각형으로 나누면서</u> 그중 `가장 큰 정사각형`을 구하려고 한다면 분할 정복을 사용해볼 수 있다. 우선 쉽게 생각해보면, 가로가 50m 세로가 25m라고 가정해보자. 그러면 가장 큰 정사각형을 만들 수 있는 것은 25 * 25이다.

<span class="crimson">분할 정복</span>으로 생각해보면 <span class="mediumblue">재귀 함수를 호출할 때마다 문제를 작게 나누어야</span> 한다. 우선 조건에 맞는 가장 큰 상자를 알아내는 것부터 시작이다. 아래의 이미지에는 <u>가로 1680 * 세로 640</u> 의 직사각형이 준비되어있다.  
<img src="https://user-images.githubusercontent.com/87808288/177140747-9bba975f-de74-4b05-9fcb-d3f9766a26cc.png" width="50%">  
한 변의 길이가 640m인 두 개의 정사각형 토지는 만들 수 있지만, <span class="forestgreen">토지가 남게 된다</span>. 원래는 <u>1680 * 640m 크기를 가진 토지를 나누는 것으로 시작</u>했지만 이제는 <span class="mediumblue">640 * 400의 토지를 나누는 문제를 푸는 것</span>이다. <u>남은 토지 크기에 맞는 정사각형을 찾는다면</u> <span class="crimson">이 정사각형으로 전체 농장을 나눌 수 있게</span> 된다. 이렇게 1680 * 640에서 640 * 400으로 그 대상이 바뀌었다.

다시 위와 같은 알고리즘으로, <u>640 * 400의 크기를 가진 토지</u>로 시작하여 <span class="forestgreen">가장 큰 정사각형의 크기는 400 * 400</span>이다. <span class="mediumblue">남은 부분은 400 * 240</span>이다.  
<img src="https://user-images.githubusercontent.com/87808288/177141773-6aa3b105-60da-402a-a881-fc5a3c07b773.png" width="30%">  
그리고 같은 방법으로 진행하면 <span class="mediumblue">240 * 160</span>이고  
<img src="https://user-images.githubusercontent.com/87808288/177142371-f1c523f7-1113-489a-b3d5-512422c81562.png" width="40%">  

이제 <u>토지를 나눌 수 있는 가장 큰 정사각형</u>이 <span class="crimson">80 * 80m</span> 라는 사실을 알게 되었다.  
<img src="https://user-images.githubusercontent.com/87808288/177142728-b65d6a54-5a7a-46be-a414-2cf7f8e77178.png" width="30%">  

# 🔴 퀵 정렬
퀵 정렬은 정렬 알고리즘이다. <u>선택 정렬보다 훨씬 빠르고</u> 실제로도 자주 사용된다.

배열을 정렬해야 한다면 이중에서 <u>가장 간단한 배열</u>의 경우는  
바로 아예 <span style="color:royalblue">정렬할 필요도 없는 정렬</span>이다.  
비어 있는 배열이나 원소가 하나인 배열은 있는 <span style="color:blue">그대로 반환</span>하면 된다.  
정렬할 것이 없기 때문이다.  

```js
function quickSort(array) {
  if (array.length < 2) return array;
}
```

`퀵 정렬`은 <span style="color:tomato">분할 정복 전략</span>을 사용하고 있다.  
다시 말해, 배열을 기본 단계가 될 때까지 나누는 것이다.  
우선 <u>배열에서 원소 하나를</u> 고른다. -> 이 원소를 <span style="color:blue">기준 원소</span>라고 부른다.  
<u>이제 모든 원소를</u> `기준 원소보다 작은 원소`와 `큰 원소`로 분류한다.  
이것을 분할이라고 하고, 이 결과로 아래의 3가지 그룹이 생긴다.  
- 기준 원소보다 작은 숫자들
- 기준 원소
- 기준 원소보다 큰 숫자들  

위의 그룹들이 만약 정렬되어 있다면 전체 배열을 정렬하는 것은 아주 쉬운 일이다.  
<u>왼쪽 배열</u> + <u>기준 원소</u> + <u>오른쪽 배열</u>과 같이 배열들을 합칠 수 있다.  
([10, 15] + [33] + [] = [10, 15, 33])  

<img src="https://user-images.githubusercontent.com/87808288/179386938-ada1588b-e37d-4246-b69c-7c3c224bf987.png" width="300">  
배열을 분할하는 방법은 기준 원소를 무엇을 고르냐에 따라 아래와 같이 달라질 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/179386942-95a66961-a577-4336-84ac-a4ad14b5d69b.png" width="400">  
그리고 <u>어떤 기준 원소를 고르든</u> <span style="color:royalblue">두 개의 하위 배열</span>에 <span style="color:blue">재귀적으로 퀵 정렬을 호출하면</span> 된다.  

<img src="https://user-images.githubusercontent.com/87808288/179387024-2bb05ad5-ebd9-43a3-834a-7e29fe5702bb.png" width="400">  
예를 들어, 기준 원소로 3을 고르면 다음과 같이 하위 배열에 대해 퀵 정렬을 호출한다.  
각 하위 배열들이 정렬되면 합쳐서 전체 배열을 정렬한다.  

```js
function quickSort (array) {
  if (array.length < 2) return array;
   
  const pivot = [array[0]];
  const left = [];
  const right = [];
  
  for (let i = 1; i < array.length; i++) {
    array[i] < pivot ? left.push(array[i]) : right.push(array[i]);
  }
  return quickSort(left).concat(pivot, quickSort(right));
}

const sorted = quickSort([5, 3, 7, 1, 9]);
console.log(sorted); // [ 1, 3, 5, 7, 9 ]
```

## 3. 빅오 표기법 복습
<img src="https://user-images.githubusercontent.com/87808288/179387465-bc7d88e0-210d-4ab2-bedd-10a9512139a5.png" width="600">  

### (1) 병합 정렬과 퀵 정렬 비교
리스트(배열)에 있는 <u>모든 element를 출력하는 간단한 함수</u>가 있다고 가정하자.  
리스트 전체에 대해 반복문을 실행하므로 이 함수의 실행 시간은 <span style="color:royalblue">O(n)</span>이다.  
이번엔 <u>element를 출력하기 전에 1초 동안 대기하도록 하는 함수</u>가 있다고 가정하자.  
그렇다면 하나의 element를 출력하기 전에 1초 멈추게 될 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/179388119-eb299ca1-1a24-4190-a60f-f6544a530cb8.png" width="600">  

<u>두 함수 모두</u> 리스트를 한 번씩 순회하기 때문에 <span style="color:royalblue">O(n)의 실행시간</span>을 가진다.  
하지만 <u>실제로는 첫 번째 함수가 1초 동안 기다리지 않기 때문에 훨씬 빠르다</u>.  
빅오 표기법으로는 두 함수 모두 같은 속도를 가지지만,  
실제로는 첫 번째 함수가 빠른 것이다.  
O(n)과 같은 빅오 표기법을 사용한다는 것은 이러한 의미가 있는 것이다.  

C 언어에서는 알고리즘이 소비하는 어떤 특정한 시간으로, 이를 상수라고 부른다.  
위의 첫 번째 함수는 10 milliseconds * n 시간이 걸리고,  
두 번째 함수는 1 second * n 시간이 걸리는 것이다.  

만약 두 개의 함수의 알고리즘이 서로 다른 빅오 표기법의 시간을 가진다면  
상수는 크게 문제 되지 않기 때문에 상수들은 보통 무시하게 된다.  

<img src="https://user-images.githubusercontent.com/87808288/179388317-8a863018-a4ed-4d8b-ac21-13fe38145c9f.png" width="250">  
위의 자료를 보고,  
단순 탐색은 10 밀리 초의 상수를 가지는데  
이진 탐색은 1초의 상수를 가지니 -> 단순 탐색이 훨씬 빠르다 말할지도 모른다.  
그런데 40억 개의 원소를 가진 리스트를 탐색한다고 가정해보면  

- 단순 탐색 -> 10밀리 초 * 40억 개 = 463초
- 이진 탐색 -> 1초 * 32 = 32초  

이진 탐색이 훨씬 빠르다는 것을 알 수 있다.  
이렇게 <u>상수는 전혀 문제가 되지 않는다</u>.  

### (2) 평균적인 경우와 최악의 경우 비교
퀵 정렬의 성능은 우리가 선택한 기준 원소에 크게 의존하게 된다.  
만약 첫 번째 원소를 항상 기준 원소로 선택한다면  
퀵 정렬은 주어진 배열이 이미 정렬되어있는지, 아닌지는 확인하지 않기 때문에 그냥 정렬하려고 한다.  

<img src="https://user-images.githubusercontent.com/87808288/179388515-c7d03932-dedc-4350-9f46-e785b1854d40.png" width="500">  

주어진 배열이 정렬되어있다면,  
두 개의 하위 배열 중 하나는 항상 빈 배열이 된다.  
그래서 위의 자료와 같이 호출 스택이 아주 길어진다.  
이번에는 가운데 element를 항상 기준 원소로 사용한다고 가정해보자.  
<img src="https://user-images.githubusercontent.com/87808288/179388582-c503bee3-ee2b-4288-98d2-a5c97c24c28d.png" width="500">  
매번 배열을 절반으로 나누기 때문에 재귀적 호출을 할 필요가 많이 사라졌다.  
그래서 호출 스택도 짧아졌다.  

살펴본 첫 번째 예는 최악의 경우를 나타내는 시나리오였다.  
그리고 바로 위의 두 번째 예제는 최선의 경우를 나타내는 시나리오이다.  
`최악의 경우`는 스택의 크기가 <span style="color:royalblue">O(n)</span>이 되었고,  
`최선의 경우`에는 스택의 크기가 <span style="color:royalblue">O(log n)</span>이 된다.  

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
