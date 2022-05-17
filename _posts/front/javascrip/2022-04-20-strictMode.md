---
layout: single
title: "strict mode"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [엄격모드] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# strict mode  
strict 모드는 ES5(ECMA Script5)에서 추가된 키워드이다.  
strict는 <u>JS가 기존에 묵인했던 error들을 발생</u>시키게된다.  
쉽게 말해서 `엄격하게 JS의 문법을 검사`한다는 개념이라고 할 수 있다.  

strict 모드는 <u>문법과 런타임 동작을 모두 검사</u>하며, 실수를 error로 변환하고 ->  
<span style="color:blue">변수 사용을 단순화</span> 시켜준다.  
<u>JS는 error를 어느 부분 무시하고 넘어갈 1수 있다</u>.  
이런 점이 coding을 편하게 해주지만 -> 이 점으로 인해 때때로 <span style="color:red">심각한 버그</span>를 만들게 된다.  
strict 모드는 이러한 `실수를 error로 변환`하여 즉시 수정할 수 있도록 처리한다.  

## strict 모드의 선언  
스크립트의 시작 혹은 함수의 시작 부분에서 "<span style="color:blue">use strict</span>"를 선언하면 strict 모드를 시작할 수 있다.  

## strict 모드의 사용  
### 선언하지 않고, 전역 변수를 만들 수 없다.  
```js
'use strict'
test = 4; //-> error
```  

### 읽기 전용 객체에 쓰는 것이 불가능하다  
```js
'use strict'

let testObj = Object.defineProperties({}, {
  prop1: {
    value: 10,
    writable: false
  },
  prop2: {
    get: function() {
    }
  }
});

testObj.prop1 = 20; //-> error
testObj.prop2 = 30;
```  

### get으로 선언된 객체는 수정할 수 없다  
```js
'use strict'

let obj = { get x() { return 17; } };
//console.log(obj) == { x: [Getter] }
//console.log(obj.x) == 17

obj.x = 5; //-> error
```  

### extensible 특성이 false로 설정된 객체에 속성을 확장 할 수 없다  
```js
'use strict'

let testObj = new Object();
Object.preventExtensions(tsetObj);
testObj.name = 'gunhee'; //-> error
```  



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
