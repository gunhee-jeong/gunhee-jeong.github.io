---
layout: single
title: "filter와 map을 활용한 test"
# categories: Git
categories:
  - codingTest # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [map, filter] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-27T10:20:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1. 문제
[50점이 넘는 학생들의 점수만을 가져와서, 이를 string 타입으로 반환하시오.]  

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
const result = students.filter(student => student.score >= 50).map(student => student.score).join()

console.log(result); //'66,80,88,90'
```

# 2. 문제
[level이 'hard'인 과목들로만 이루어진 새로운 배열을, 해당과목만으로 이루어진 문자열로 반환하시오.]  

```js
let courses = [
  {level:'easy', subject: "English" }, 
  {level:'hard', subject: "Mathmatic" }, 
  {level:'medium', subject: "Literature" }, 
  {level:'hard', subject: "Science" }, 
  {level:'medium', subject: "Socialogy" }
  ];
```

```js
const result = courses.filter(x => x.level === 'hard').map(ele => ele.subject).join(',');
result; //'Mathmatic,Science'
```

# 3. 중복된 재료를 뺀 전체 재료 반환하기

```js
// 중복된 재료를 뺀 전체 재료 
// [ 'tomato', 'basil', 'onion', 'chicken', 'cheese', 'olive', 'beef' ]

// Assignment
let pasta = ['tomato', 'basil', 'onion','chicken'];

let pizza = ['tomato', 'cheese', 'onion','olive','beef'];

// 아래 함수를 작성해주세요. 
function totalIngredients () {
}
```

```js
// 아래 함수를 작성해주세요. 
function totalIngredients () {
  const total = pasta.concat(pizza);
  const result = total.filter((ele, ind) => total.indexOf(ele) === ind);
  return result;
}

totalIngredients();
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
