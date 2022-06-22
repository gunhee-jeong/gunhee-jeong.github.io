---
layout: single
title: "Array.prototype -> from & fill"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Array.prototype] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-06-22T16:50:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1장 Array.prototype.from()
`from 메서드`는 유사 배열 객체나 반복 가능한 객체(iterable object)를  
얕게 복사해 새로운 Array 객체를 만든다.  

```js
let from = Array.from({length: 5}, () => 1);
console.log(from); // [ 1, 1, 1, 1, 1 ]
```

```js
let from = Array.from([1, 2, 3], x => x + x);
console.log(from); // [ 2, 4, 6 ]
```

# 2장 Array.prototype.fill()
`fill 메서드`는 <u>배열의 시작 인덱스부터 끝 인덱스의 이전까지</u> <span style="color:tomato">하나의 값으로 채워 생성</span>한다.  
원본 배열을 직접 변경하며, 반환값은 변경된 배열이 된다.  

fill 메서드는 <u>value, start, end</u>의 3가지 인자를 가진다.  
(start, end는 선택사항이 된다.)  

```js
[1, 2, 3].fill(4); //output == [4, 4, 4]
[1, 2, 3].fill(4, 1); //output == [1, 4, 4]
[1, 2, 3].fill(4, 1, 2); //output == [1, 4, 3]
[1, 2, 3].fill(4, 1, 1); //output == [1, 2, 3]
[1, 2, 3].fill(4, 3, 3); //output == [1, 2, 3]
```

## 1. 응용
[length가 100이고 모두 3으로 채워진 배열을 만들어라.]  

```js
const arr = Array(100).fill(3);
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
