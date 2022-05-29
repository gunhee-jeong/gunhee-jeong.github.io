---
layout: single
title: "배열-> 'forEach'"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [배열] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# forEach
함수형 프로그래밍은 순수 함수와 보조 함수의 조합을 통해  
로직 내에 존재하는 <span style="color:red">조건문과 반복문을 제거</span>하여 복잡성을 해결하고 <span style="color:red">변수의 사용을 억제</span>하여  
상태 변경을 피히려는 프로그래밍 패러다임이다.  

조건문이나 반복문은 로직의 흐름을 이해하기 어렵게 한다.  
특히 `for문`은 <u>반복을 위한 변수를 선언해야</u> 하며,  
<span style="color:royalblue">조건식과 증감식으로 이루어져 있어서 함수형 프로그래밍이 추구하는 바와 맞지 않는다</span>.  

```js
const numbers = [1, 2, 3];
const pows = [];

//for문으로 배열 순회
for (let i = 0; i < numbers.length; i++) {
  pows.push(numbers[i] ** 2);
}

console.log(pows); //[1, 4, 9]
```

`forEach 메서드`는 <u>for문을 대체할 수 있는 고차 함수</u>다.  
forEach 메서드는 자신의 내부에서 반복문을 실행한다.  
즉, forEach 메서드는 반복문을 추상화한 고차 함수로서 내부에서 반복문을 통해 자신을 호출한 배열을  
순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다.  
위의 예제를 forEach 메서드로 구현하면 아래와 같다.  

```js
const numbers = [1, 2, 3];
const pows = [];

//forEach 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.
numbers.forEach(item => pows.push(item ** 2));
console.log(pows); //[1, 4, 9]
```

위 예제의 경우 forEach 메서드는 numbers 배열의 모든 요소를 순회하며 콜백 함수를 반복 호출한다.  
<span style="color:royalblue">numbers 배열의 요소가 3개이므로 콜백 함수도 3번 호출</span>된다.  
다시 말해, forEach 메서드는 콜백 함수를 호출할 때 3개의 인수,  
즉 forEach 메서드를 호출한 <span style="color:blue">배열의 요소값</span>과 <span style="color:blue">인덱스</span>, forEach 메서드를 <span style="color:blue">호출한 배열(this)</span>을 순차적으로 전달한다.  

```js
[1, 2, 3].forEach((item, index, arr) => {
  console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
});
// '요소값: 1, 인덱스: 0, this: [1,2,3]'
// '요소값: 2, 인덱스: 1, this: [1,2,3]'
// '요소값: 3, 인덱스: 2, this: [1,2,3]'
```

forEach 메서드는 원본 배열을 변경하지 않는다. 하지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.  

```js
const numbers = [1, 2, 3];

numbers.forEach((item, index, arr) => { arr[index] = item ** 2; });
console.log(numbers); //[1, 4, 9]
```

forEach 메서드의 콜백 함수는 일반 함수로 호출되므로 콜백 함수 내부의 this는 undefined를 가리킨다.  
<u>this가 전역 객체가 아닌 undefined를 가리키는</u> 이유는  
<span style="color:royalblue">클래스 내부의 모든 코드에는 암묵적으로 strict mode</span>가 적용되기 때문이다.  

forEach 메서드의 콜백 함수 내부의 this와 multiply 메서드 내부의 this를 일치시키려면  
forEach 메서드의 두 번째 인수로 forEach 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달한다.  
아래 예제의 경우 forEach 메서드의 두 번째 인수로 multiply 메서드 내부의 this를 전달하고 있다.  

```js
class Numbers {
  numberArray = [];

  multiply(arr) {
    arr.forEach(function (item) {
      this.numberArray.push(item * item);
    }, this); //forEach 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달
  }
}

const numbers = new Numbers();
numbers.multiply([1, 2, 3]);
console.log(numbers.numberArray); //[1, 4, 9]
```

더 나은 방법은 `화살표 함수`를 사용하는 것이다.  
<span style="color:royalblue">화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다</span>.  
따라서 화살표 함수 내부에서 <span style="color:blue">this를 참조하면 상위 스코프</span>, 즉 multiply 메서드 내부의 this를 그래도 참조한다.  

```js
class Numbers {
  numberArray = [];

  multiply(arr) {
    arr.forEach(item => this.numberArray.push(item * item));
  }
}

const numbers = new Numbers();
numbers.multiply([1, 2, 3]);
console.log(numbers.numberArray); //[1, 4, 9]
```

`forEach 메서드`는 <span style="color:royalblue">for문과는 달리 break, continue 문을 사용할 수 없다</span>.  
다시 말해, 배열의 <span style="color:blue">모든 요소를 빠짐없이 모두 순회하며 중간 순회를 중단할 수 없다</span>.  

<span style="color:red">forEach</span>는 <u>for 대신 사용하는</u> <span style="color:blue">반복문</span>이다  
map과의 큰 차이는 **forEach** 함수 **자체가 return하는 것도 아무것도 없다는 것**이다  
따라서 forEach <u>함수를 탈출하고 싶을 때 return을 사용</u>하면 된다  
(map은 요소가 수정된 새로운 배열이 return되었다면, forEach는 아무것도 reture하는 것이 없다)

```javascript
let startWithNames = [];
let names = ["a", "ab", "cbb", "ada"];

names.forEach((el) => {
  if (el.startsWith("a")) {
    startWithNames.push(el);
  }
});

console.log(startWithNames); //output == ['a', 'ab', 'ada']
```

```javascript
let hasC = false;
let arr = ["a", "b", "c", "d"];

arr.forEach((el) => {
  if (el === "c") {
    hasC = true;
    return;
  }
});
```

- <u>forEach도 함수</u>이므로, **중간에 반복문을 탈출하고 싶다면** <span style="color:blue">return</span>을 사용하면 된다

# Assignment

## 1. moreThan100 함수를 구현하세요

문제설명

- 숫자로 구성된 배열을 인자로 받습니다
- 100보다 크거나 같으면 true를 100보다 작으면 false로 요소를 변경하여, 새로운 배열을 retur하세요

  ```javascript
  [100, 9, 30, 7] -> [true, false, false, false]
  ```

- 주어진 함수

  ```javascript
  const moreThan100 = (nums) => {};
  ```

문제풀이

- 나의 풀이

  ```java
  let nums = [100, 9, 30, 7];

  const moreThan100 = nums => {
    let result = [];
    nums.forEach(x => {
      if (x < 100) {
        result.push(false);
      } else if(x >= 100) {
        result.push(true);
      }
    });
    return result;
  };

  console.log(moreThan100(nums));
  ```

## 2. foramtDate 함수를 구현하세요

문제설명

- 날짜가 담긴 배열을 인자로 받습니다
- 날짜의 data type은 string이며, 보내는 날짜 타입은 'YYYY-MM-DD'입니다
- 해당 날짜의 형식을 'YYYY년 MM월 DD일'로 바꿔서 새로운 배열을 return하세요  
  dates(input)가 ['2019-03-21', '2019-04-21', '2019-05-21']이라면  
  return은 ['2019년 03월 21일', '2019년 04월 21일', '2019년 05월 21일']
- 주어진 함수

  ```java
  const formatDate = dates => {};
  ```

  문제풀이

- 나의 코드

  ```java
  let dates = ['2019-03-21', '2019-04-21', '2019-05-21'];

  const formatDate = dates => {
    return dates.map(x => `${x.split('-')[0]}년 ${x.split('-')[1]}월 ${x.split('-')[2]}일`)
  };

  console.log(formatDate(dates));
  ```

  - <u>dates는 기본적으로 array</u>이기 때문에 array method인 <span style="color:red">map</span>을 사용했다  
    **x**에는 차례대로 <u>dates의 0~2번 index의 value가</u> 들어오는데  
    ('2019-03-21' -> '2019-04-21' -> '2019-05-21')  
    이 value들은 <span style="color:blue">string 타입</span>이다
  - 이렇게 0번 index의 value인 <span style="color:green">'2019-03-21'</span>이 들어오고 이것은 **string 타입**이므로  
    <span style="color:red">split method</span>를 사용하여 <u>'-'를 제거</u>하면서, <span style="color:blue">다시 array로 반환</span>하게 된다!  
    **x.split('-')을 통해서 ['2019', '03', '21']**이라는 <span style="color:blue">array가 반환</span>되고 여기서 [0]을 통해서  
    0번 index의 value를 가져오면서 각각 년, 월, 일을 추가하여  
    최종적으로 map method의 반환 값은 ['2019년 03월 21일', '2019년 04월 21일', '2019년 05월 21일']이 된다!

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
