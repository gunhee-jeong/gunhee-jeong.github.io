---
layout: single
title: "Array.prototype -> sort"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Array.prototype] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-06-21T22:50:00+09:00
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

# sort
sort 를 사용하기 전 기본적인 용어를 우선 살펴보자면  
- 오름차순: 1, 2, 3, 4, 5......
- 내림차순: 9, 8, 7, 6, 5......

# 🔴 알고리즘
## 🟠 정렬 알고리즘: Stable & In-Place(안정 & 불안정)
<span class="crimson">안정 정렬</span>과 <span class="crimson">불안정 정렬</span>은 중복된 키를 순서대로 정렬하는 정렬 알고리즘을 말한다.

`안정 정렬`이란 <span class="mediumblue">중복된 값</span>을 <span class="forestgreen">입력 순서와 동일하게 정렬하는 것</span>을 말하는데, 기존의 정렬 형태를 유지한 상태에서 정렬한다는 것을 의미한다.

`불안정 정렬`이란 <span class="mediumblue">중복된 값</span>을 <span class="forestgreen">입력 순서와 상관없이 무작위로 뒤섞인 상태에서 정렬</span>이 이루어진다.

```js
let a = [1, 3, 4, 5, 7(2), 7(1), 9];
```

<u>변수 a</u>에는 <span class="forestgreen">7이 중복되어 총 2개</span>가 존재한다. 이 2개의 7을 구분하기 위해서 1번과 2번이라고 지정하였다! <u>7(1)이 앞에 나오는 것</u>을 <span class="mediumblue">안정 정렬</span>, 그렇지 않은 경우를 <span class="mediumblue">불안정 정렬</span>이라고 표현할 수 있다.

# 🔴 특징
`sort 메서드`는 array의 요소를 정렬한 후 반환하기 때문에, sort를 사용시 <span class="crimson">원본이 수정</span>된다. sort 메서드의 사용으로 <span class="mediumblue">복사본이 만들어지지 않는다</span>.

## 🟠 유니코드 기준
`sort 메서드`는 문자열의 <span class="mediumblue">유니코드 포인트</span>를 따르게 된다.

```js
example = [5, 3, 2, 1, 10];
example.sort();
console.log(example); //output == [1, 10, 2, 3, 5]
```

<span class="forestgreen">숫자 정렬</span>에서는 <u>2가 10보다 앞서지만</u>, 숫자는 문자열로 변환되기 때문에 <u>'10'은 <span class="forestgreen">유니코드</span> 순서에서 '2' 앞에 위치하게</u> 된다. '2'의 아스키 코드는 50이고, '1'의 아스키 코드는 49이기 때문에 '10'이 배열에서 앞서게 된 것이다!

## 🟠 compareFunction
`compareFunction`을 선언한 경우 sort() 메서드는 compareFunction 에게 <u>array의 element 를 2개씩 반복</u>해서 보낸 뒤 <span class="forestgreen">compareFunction 이 반환하는 값을 기준으로 정렬</span>한다. 안정 정렬을 하기 위해서는 compareFunction을 사용해야 한다.

```js
arr.sort([compareFunction])
```

> 대괄호[]는 괄호 안의 매개변수가 필수가 아니라 상황에 따라 생략이 가능함을 의미한다.  

- 반환 값 < 0: a가 b보다 앞에 있어야 함
- 반환 값 = 0: a와 b의 순서를 바꾸지 않음
- 반환 값 > 0: b가 a보다 앞에 있어야 한다.  

```js
const numbers = [10, 3, 8, 4, 1];
function compare(a, b) {
	return a - b;
}
numbers.sort(compare); //output == [1, 3, 4, 8, 10]

//numbers.sort(function(a, b) {
//return a - b;
//})

//numbers.sort((a, b) => a - b);
```

<u>a 에는 3</u>이 들어가고, <u>b에는 10</u>이 할당된다. 그래서 3 - 10 은 <span class="forestgreen">-7 이라는 결과</span>가 나오고 <u>0보다 작을 경우</u> <span class="mediumblue">a 가 b 보다 앞에</span> 있어야 하기 때문에 3 이 10 보다 앞으로 정렬된다.

# 🔴 응용
## 🟠 Object 정렬
```js
const market = {
  name: "이마트",
  fruits: [
    {
      name: "Banana",
      price: 1000
    }, {
      name: "Apple",
      price: 500
    }, {
      name: "Cherry", 
      price: 100
    }
  ]
};

market.fruits.sort(({ price: a }, { price: b }) => a - b);

console.log(market);
// [
//   { name: 'Cherry', price: 100 },
//   { name: 'Apple', price: 500 },
//   { name: 'Banana', price: 1000 }
// ]
```

## 🟠 조건부 정렬
compareFunction 내부에 if 문을 사용하여 정렬 조건을 직접 정의할 수 있다.  

```js
const numbers = [0, 0, 0, 3, 2, 1];

numbers.sort(function(a, b) {
  if(a === 0) { return 1; } 
  else if(b === 0) { return -1; } 
  else { return a - b; }
})

console.log(numbers); //output == [1, 2, 3, 0, 0, 0]
```

## 🟠 다중 조건 정렬
비교 함수에 조건을 추가하여 다중 조건으로 sort를 사용할 수 있다.  

```js
// 번호, 몸무게, 승률, 우승횟수
const list = [
  [1, 60, 33.333333, 3],
  [2, 80, 33.333333, 1],
  [3, 60, 66.666666, 3],
  [4, 80, 66.666666, 2],
  [5, 70, 66.666666, 2],
  [6, 70, 66.666666, 2],
];

// 정렬 : 승률 높은 순 > 우승횟수 높은 순 > 몸무게 높은순 > 번호 낮은 순
list.sort((a, b) => {
  if(a[2] > b[2]) return -1;
  else if(a[2] < b[2]) return 1;
  else if(a[3] > b[3]) return -1;
  else if(a[3] < b[3]) return 1;
  else if(a[1] > b[1]) return -1;
  else if(a[1] < b[1]) return 1;
  else if(a[0] > b[0]) return 1;
  else if(a[0] < b[0]) return -1;
})
console.log(list);
// 0: [3, 60, 66.666666, 3]
// 1: [4, 80, 66.666666, 2]
// 2: [5, 70, 66.666666, 2]
// 3: [6, 70, 66.666666, 2]
// 4: [1, 60, 33.333333, 3]
// 5: [2, 80, 33.333333, 1]
```

<!-- <span style="color:royalblue"> -->

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
