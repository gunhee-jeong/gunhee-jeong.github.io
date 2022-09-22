---
layout: single
title: "Array.prototype -> find and findIndex"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Array.prototype] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-26T21:00:00+09:00
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

# Array.prototype -> find and findIndex
# 🔴 find
`find` method는 <u>주어진 판별 함수를 만족하는</u> <span class="crimson">첫 번째 요소의 값을 반환</span>한다.

```js
const array1 = [5, 12, 8, 130, 44];
const found = array1.find(element => element > 10);

console.log(found); //output == 12
```

<u>10보다 큰 element로는 12, 130, 44</u>가 있지만 <span class="mediumblue">10을 넘는 첫 번째 element 만을 바로 반환</span>한다. 그렇게 <span class="forestgreen">element를 찾았다면 메서드를 종료</span>하게 된다. find method는 주어진 <u>판별 함수에 true가 없다면 <span class="crimson">undefined</span>를 반환</u>한다.

callback(element, array, index)를 사용할 수 있다.

```js
let array = [1, 3, 5, 4, 4, 8];

console.log(array.find((element, index) => index == 2)); //output == 5
```

## 🟠 예제
find student with the score 90  

```js
function Student (name, age, enrolled, score) {
  this.name = name;
  this.age = age;
  this.enrolled = enrolled;
  this.score = score;
}

const students = [
  new Student('A', 29, true, 45),
  new Student('B', 28, false, 80),
  new Student('C', 30, true, 90),
  new Student('D', 40, false, 66),
  new Student('E', 18, true, 88),
];

const result = students.find((student, index) => student.score == 90)

//const result = students.find(function (student, index) {
//	return student.score == 90;})

console.log(result); //output == Student {name: 'C', age: 30, enrolled: true, score: 90}
```

`find 메서드`는 filter 메서드와 같이 <span class="mediumblue">배열의 모든 인덱스를 순회</span>하면서 <u>판별함수를 만족하는 element를 찾으면</u> <span class="mediumblue">배열의 순회를 그 자리에서 중지</span>한다. <u>"includes"와 "indexOf" 와는 다르게</u> filter 함수와 같이 find 함수는 <span class="forestgreen">배열을 순회하는 것</span>이 특징이다.

위의 find 메서드의 특징을 살려, 배열을 순회하면서 <span class="mediumblue">판별 함수의 조건에 해당하는 element를 반환하여 변수로 선언</span>하고 이 <u>선언된 변수를 이용</u>하여 <span class="forestgreen">filter 함수에 boolean을 반환</span>하여 배열에서 <u>해당 element를 제거</u>할 수도 있다. 활용의 예시는 아래의 코드와 같다.

```js
let n = 5;
let lost = [2, 4];
let reserve = [3];

function solution(n, lost, reserve) {      
  return n - lost.filter(loster => {
    const reserveMan = reserve.find(reserver => Math.abs(reserver - loster) === 1);

    reserve = reserve.filter(reserver => reserver !== resereMan);

    if(!reserveMan) return true;
  }).length;
}

solution(n, lost, reserve );
```

# 🔴 findIndex
`findIndex 함수`는 주어진 <u>판별 함수의 결과가 true</u> 인 <span class="crimson">첫 번째 element의 index를 반환</span>한다.

```js
let array = [1, 3, 5, 4, 4, 8];

console.log(array.findIndex((element, index) => element == 4)); //output == 3
```

`find` 메서드와 `findIndex` 메서드는 -> <span class="mediumblue">판별 함수가 true</span>인 경우 <span class="crimson">더이상 진행하지 않는다</span>!

<u>find 메서드와 다른 점</u>이라고 할 수 있는 것은, <span class="forestgreen">판별 함수가 false일 경우</span>이다. 판별 함수가 false 일 경우 `find` 함수는 <span class="mediumblue">undefined</span>를 반환하고 `findIndex`의 경우에는 <span class="mediumblue">-1</span>을 반환한다.

callback(element, index, array)를 사용할 수 있다.

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
