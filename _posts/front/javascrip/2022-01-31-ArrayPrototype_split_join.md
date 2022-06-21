---
layout: single
title: "Array.prototype -> 'split' and 'join'"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [Array.prototype] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1. split

> Split a string into substrings using the specified separator and return them as an array.
> (지정된 구분 기호를 사용하여 문자열을 부분 문자열로 분할하고 배열로 반환합니다.)
> @param splitter An object that can split a string.

<span style="color:red">split</span>는 <span style="color:blue">String을 array로</span> 만드는 것으로 `join과 split는 반대적인` 개념이다.  

문자열이 하나로 연결된 <span style="color:blue">'문자열'</span> 형태라면 `.split('')`를 사용해서 <span style="color:red">['문', '자', '열']</span>로 만들 수 있다.  

```js
const x = '문자열';
x.splice('') //[ '문', '자', '열' ]
```

문자열이 <span style="color:blue">'문, 자, 열'</span>의 형태라면 `.split(',')`를 사용해서 <span style="color:red">['문', '자', '열']</span>로 만들 수 있다.  
그런데 이때 <span style="color:blue">.split('')</span>를 사용하면 -> [ '문', ',', &nbsp;'자', ',', '열' ]이 되므로  
<u>','</u>을 제거하기 위해 <span style="color:red">.split(',')</span>를 사용해야하는 것이다.  

```js
const y = '문,자,열';
y.split(''); //[ '문', ',', '자', ',', '열' ]
y.split(','); //[ '문', '자', '열' ]
```

```javascript
const numbers = "1234";
console.log(numbers.split("")); //output == ['1', '2', '3', '4']

//예시
const fruits = "🍎, 🥝, 🍌, 🍒";

console.log(fruits.split(",")); //output == ['🍎', ' 🥝', ' 🍌', ' 🍒']

const result = fruits.split(",", 2);
console.log(result); //output == ["🍎", " 🥝"]

const result = fruits.split(",", 3);
console.log(result); //output == ["🍎", " 🥝", "🍌"]
```

[<u>지정된 구분 기호나 문자를 입력</u>하면, <span style="color:red">해당하는 문자열은 제거하고 분할</span>하여 **배열로 반환**한다!]

```javascript
const fruits = "one4seveneight";
let arr = fruits.split("seven");
console.log(arr); //output == ['one4', 'eight']

const fruits = "one4seveneight";
let arr = fruits.split("one");
console.log(arr); //output == [ '', '4seveneight' ]
```


# 2. join

> oin(separator?: string): string;
> Adds all the elements of an array into a string, separated by the specified separator string.
> (배열의 모든 요소를 지정된 구분 기호 문자열로 구분하여 문자열에 추가합니다.)
> @param separator A string used to separate one element of the array from the next in the resulting string.  
> If omitted, the array elements are separated with a comma

[<u>array를</u> <span style="color:red">문자열로 만들고</span> 이를 반환한다(array -> string)]

  ```javascript
  const fruits = ["apple", "banana", "orange"];
  console.log(fruits.join("")); //output == applebananaorange

  const adress = ["경기도", "분당구", "중앙공원로", "53"];
  console.log(adress.join(" ")); //output == "경기도 분당구 중앙공원로 53"
  ```

  **join**을 사용하면 이렇게 <u>array로 반환되는 것이 아니라</u>, <span style="color:red">String 타입</span>으로 결과물이 반환된다!!  
  
[.join(<span style="color:red">*</span>)]  
join을 사용하면서 괄호() 안에 구분 기호 문자를 넣어서 사용하면  

```js
  const result = fruits.join("*");
  console.log(result); //output == "apple*banana*orange"
```  
<u>콤마(,)</u> 대신에 해당 <span style="color:blue">구분 기호 문자가</span> 결과로 들어가게 된다.  

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
