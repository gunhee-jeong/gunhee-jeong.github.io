---
layout: single
title: "slice와 splice의 차이점"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Array.prototype] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-16
last_modified_at: 2022-08-06
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.red {
  color: crimson;
}

.blue {
  color: mediumblue;
}

.green {
  color: forestgreen;
}

.grey {
  color: #696871;
}
</style>

📌 글의 목적: slice와 splice 메서드의 차이점에 대해서 다른 사람들에게 정보를 제공하기 위해 작성한 글

slice 메서드와 splice 메서드 모두, <span class="green">첫 번째 파라미터</span>는 <span class="blue">start로 잘라낼 인덱스의 시작점</span>을 의미한다.

```jsx
slice(begin, end);
slice(start: 추출을 시작할 인덱스, end: 추출을 끝낼 인덱스);

splice(start, deleteCount);
splice(start: 자르기 시작할 인덱스, deleteCount: start부터 몇 개를 삭제할 것인지에 대한 값);
```

위의 코드와  같이 <span class="green">splice 메서드</span>의 <span class="blue">deleteCount</span> 파라미터는 <span class="red">start부터 n 개를 삭제하겠다는 값</span>을 의미한다. <span class="green">slice 메서드</span>의 <span class="blue">end</span> 파라미터는 지정된 인덱스를 포함하지 않고 지정한 <span class="red">end의 앞에서 추출을 끝낸다</span>.

```jsx
const numberList = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

let sliceResult = numberList.slice(3, 4 + 1);

let spliceResult = numArray.splice(3, 4);

console.log(sliceResult); // [3, 4]
console.log(spliceResult); // [3, 4, 5, 6]
```

<span class="green">slice 메서드</span>는 <span class="red">원본 배열을 변형시키지 않는다</span>.

```jsx
const array = [1, 2, 3, 4, 5];

const result = array.slice(2, 5); //outcome = (3) [3, 4, 5]

const result2 = array.slice(-2); //output == [4, 5]

console.log(array); //outcome = (5) [1, 2, 3, 4, 5]
```

위의 코드와 같이 array의 값인 배열은 변형되지 않았다.

slice 메서드와는 달리 <span class="green">splice</span>는 <span class="red">원본 배열을 변형</span>시킨다.

```jsx
const fruits = ["🍎", "🍌", "🍓", "🍑", "🍋"];

console.log(fruits.splice(1, 1)); // [ '🍌' ]

console.log(fruits); // ['🍎', '🍓', '🍑', '🍋']
```

위의 코드와 같이 원본 배열인 fruits를 살펴보면 🍌<span class="blue">가 삭제</span>되어 <span class="red">원본 배열이 변형</span>된 것을 볼 수 있다. 

그리고 <span class="green">splice 메서드</span>는 원본 배열의 <span class="blue">value를 삭제하고 데이터를 새롭게 추가</span>할 수 있다.

```jsx
const fruits = ["🍎", "🍌", "🍓", "🍑", "🍋"];

fruits.splice(1, 1, "🍏", "🍉");

console.log(fruits); // ['🍎', '🍏', '🍉', '🍓', '🍑', '🍋']
```

위의 코드를 살펴보면, `splice(1, 1)`를 통해서 🍌<span class="green">를 삭제</span>하고, 그 이후에 🍏, 🍉은 <span class="blue">삭제한 value의 자리에 추가</span>된 것을 확인할 수 있다.

💡 <span class="grey">MDN: [Array.prototype.splice()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)</span>

💡 <span class="grey">MDN: [Array.prototype.slice()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)</span>

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
