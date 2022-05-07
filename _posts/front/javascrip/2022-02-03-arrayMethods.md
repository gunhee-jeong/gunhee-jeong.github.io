---
layout: single
title: "map"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [array method] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# map 메서드

# forEach

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
