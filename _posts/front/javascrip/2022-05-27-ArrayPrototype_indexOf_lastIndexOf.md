---
layout: single
title: "Array.prototype -> 'indexOf' and 'lastIndexOf'"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Array.prototype] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-27T06:20:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1. indexOf
`indexOf`는 <span style="color:tomato">searchValue가 처음으로 탐색되는 index를 반환</span>하고 <span style="color:red">존재하지 않으면 -1을 반환</span>한다.  

<u>findIndex와의 차이점</u>으로는 <span style="color:royalblue">find, findIndex</span> 메서드는 <span style="color:blue">판별 함수가 true이냐 false이냐</span>로 판단한다면  
<u>indexOf와 includes</u>는 <span style="color:blue">searchValue</span>를 갖는다는 것이다.  

```js
let hi = 'Hello world';

console.log(hi.indexOf('e')); //output == 1
console.log(hi.indexOf('Z')); //output == -1
console.log(hi.indexOf('l')); //output == 2
```

문자열에서 <span style="color:royalblue">탐색을 시작하는 위치는 기본적으로 0</span>으로 설정된다.  
fromIndex가 4이기 때문에 -> 변수 'hi'에서 4번째 indexdls 'o world'에서 부터 'l'을 탐색하기 시작한다.  

```js
let hi = 'Hello world';

console.log(hi.indexOf('l', 4)); //output == 9
```

[Quiz]  
변수 'array1'의 값과 변수 'array2'의 값에서 중복되는 숫자는 제거하여 array로 반환해라.  

```js
let array1 =  [1,2,3,4,5];

let array2 = [3,4,5,6,7];

let result = array1.concat(array2);
console.log(result); //output == [1, 2, 3, 4, 5, 3, 4, 5, 6, 7]    

let eraseDuplicates = result.filter((el,index)=> 
result.indexOf(el)===index); //첫번째 3은 index가 2임, 두번째 3은 index가 5임

console.log(eraseDuplicates); //output == [1, 2, 3, 4, 5, 6, 7]

//3을 보면 3은 중복된 값으로 result.indexOf(3)은 2가 나온다.
//처음 3은 index[2]로 조건을 만족하지만 두번째 3은 index[5]로 조건을 만족하지 않아서 통과되지 못한다. 
//그래서 두번째 3은 지워지게 되는 것이다. 이런식으로 중복된 3, 4,5가 지워지고 하나만 남게된 것입니다!
```

# 2. lastIndexOf
```js
const fruits = ['🍎', '🍏', '🍉', '🍑', '🍋'];

fruits.push('🍎');

console.log(fruits);//outcome = (6) ['🍎', '🍏', '🍉', '🍑', '🍋', '🍎']

console.log(fruits.indexOf('🍎'));//outcome = 0

console.log(fruits.lastIndexOf('🍎'));//outcome = 5
```

<span style="color:green">fruits.push</span>로 인해서 <u>🍎가 fruits의 앞과 뒤에 중복</u>되어 생성되었다.  
`indexOf`는 <span style="color:blue">맨 앞의 index를</span> 알려주고, `lastIndexOf`는 <span style="color:blue">가장 마지막에 있는 index를</span> 알려주게 된다.  

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
