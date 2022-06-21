---
layout: single
title: "Array.prototype -> 'filter' and 'map'"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Array.prototype] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-27T09:20:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1. filter
`fiter` 메서드는 배열 각 요소에 대하여 주어진 <span style="color:royalblue">함수의 결과값이이 true인 요소를 모아</span> <span style="color:tomato">새로운 array를 반환</span>하는 메서드이다.  
<span style="color:red">true일 경우</span>에만 filter 메서드의 element를 <span style="color:tomato">새로운 array의 index에 값으로 추가</span>한다.  
<span style="color:royalblue">false일 경우에는 새로운 array의 index에 추가되지 않는다</span>.  
(이때 기존의 array를 변형시키지 않고, 새로운 array를 반환한다.)  

`map`이 <u>내부 함수</u>의 <span style="color:royalblue">리턴 값에 문자, 숫자, 배열 등으로 다양한 타입</span>이 가능하다면  
`filter`는 <span style="color:tomato">오직 boolean 타입만 반환</span>이 가능하다.  

filter 메서드와 map 메서드는 크게 filter(callbackFunc, thisArg) 2개의 인자를 가진다.  
callbackfunc 안에서 3개의 인자 -> element, index, array를 가지는데  
첫 번째 부분인 element 인수만 필수로 지정되어야하고 나머지는 선택적이다.  

## Quiz
make an array of enrolled students

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
```

```js
const result = students.filter(student => student.enrolled);
console.log(result);

//const result = students.filter(function(student) {
//	return student.enrolled;
//})
```

# 2. map
`map` 메서드는 <u>내부 함수의 리턴 값</u>이 <span style="color:red">문자, 숫자, 배열 등으로 다양한 타입이 가능</span>하다.  

```js
let list = [1, 2, 3, 4, 5, 6, 7];

console.log(list.filter(a => a > 4)); //output == [5, 6, 7]
console.log(list.map(a => a > 4)); //output == [false, false, false, false, true, true, true]
```

## Quiz
make an array containing only the student's score(result should be: [45, 80, 90, 66, 88])

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
```

```js
//const result = students.map(function(student) {
//	return student.score
//	})

const result = students.map(student => student.score);
console.log(student) //output == A and B and C .......

console.log(result)
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
