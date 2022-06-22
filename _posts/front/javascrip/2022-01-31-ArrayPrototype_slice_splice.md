---
layout: single
title: "Array.prototype -> 'slice' and 'splice'"
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

# 1. slice
**splice method** 와는 다르게 <span style="color:red">slice method</span>는 <span style="color:blue">원본 배열을 변형시키지 않음</span>  

```javascript
const array = [1, 2, 3, 4, 5];

const result = array.slice(2, 5); //outcome = (3) [3, 4, 5]

const result2 = array.slice(-2); //output == [4, 5]

console.log(array); //outcome = (5) [1, 2, 3, 4, 5]
```

  위의 코드에서 보는 것과 같이 const **array의 배열**은 <span style="color:red">변형되지 않았다</span>!  
  <span style="color:green">array.slice(2, 5)</span>는 **array에서 3번째 value인 3부터 5까지**를 반환한다  
  그리고 <span style="color:green">array.slice(-2)</span>에서 **-2**는 <u>배열의 마지막에서 두 번째 요소를</u> 나타내고 4, 5를 반환한다

# 2. splice
- slice method 와는 다르게 <span style="color:red">splice</span>는 <span style="color:blue">원본 배열을 변형</span>시킴!

  ```javascript
  const fruits = ["🍎", "🍌", "🍓", "🍑", "🍋"];

  console.log(fruits.splice(1, 1));
  console.log(fruits); //output == ['🍎', '🍓', '🍑', '🍋']
  ```

  <span style="color:green">fruits.splice(1, 1)</span>를 통해서 **🍌가 반환**되었고,  
  **원본 배열인 fruits**를 살펴보면 <span style="color:red">🍌가 삭제되어 원본 배열이 변형</span>된 것을 확인할 수 있다!

- splice method는 **원본 배열의 value를 삭제**하고 <span style="color:red">데이터를 새롭게 추가할 수도</span> 있음!
  ```javascript
  const fruits = ["🍎", "🍌", "🍓", "🍑", "🍋"];
  fruits.splice(1, 1, "🍏", "🍉"); //outcome = (6) ['🍎', '🍏', '🍉', '🍓', '🍑', '🍋']
  ```
  splice(1, 1)을 통해 <u>🍌를 삭제한 것 까지는 다른 것들과 비슷</u>하지만,  
  그 이후에 **"🍏", "🍉"**은 <span style="color:red">삭제한 value의 자리에 새롭게 추가</span>한 것을 볼 수 있다
  
  <span style="color:green">splice(4, 2)</span> 라고 한다면 -> <span style="color:red">index 번호 4부터 시작</span>하여 <span style="color:red">2개를 원본에서 삭제</span>하고  
  빼낸 2개의 원소를 반환하게 된다.  

- **댓글 삭제 기능**을 구현할 때 splice 메서드를 사용하게됨!

<span style="color:red">원본 배열</span>의 <span style="color:tomato">중간에 요소를 추가하거나 중간에 있는 요소를 제거</span>하는 경우 splice 메서드를 사용한다.  
splice 메서드는 <span style="color:blue">3개의 매개변수</span>가 있으며 <span style="color:royalblue">원본 배열을 직접 변경</span>한다.  
- `start`: 원본 배열의 요소를 제거하기 시작할 인덱스이다.  
start만 지정하면 원본 배열의 start부터 모든 요소를 제거한다.  
start가 음수인 경우 배열의 끝에서의 인덱스를 나타낸다.  
만약 -1이면 마지막 요소를 가리키고 -n이면 마지막에서 n번째 요소를 가리킨다.  
- `deleteCount`: 원본 배열의 요소를 제거하기 시작할 인덱스인 start부터 제거할 요소의 개수다.  
deleteCount가 0인 경우 아무런 요소도 제거되지 않는다.  
- `item`: 제거한 위치에 삽입할 요소들의 목록이다. 생략할 경우 원본 배열에서 요소들을 제거하기만 한다.  

```js
const arr = [1, 2, 3, 4];

//원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입한다.
const result = arr.splice(1, 2, 20, 30);

//제거한 요소가 배열로 반환된다.
console.log(result); //[2, 3]
//splice 메서드는 원본 배열을 직접 변경한다.
console.log(arr); //[1, 20, 30, 4]
```

<img src="https://user-images.githubusercontent.com/87808288/170851398-60d09f26-2ea3-4f39-a89f-acb7c1367592.png" width="500">  

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
