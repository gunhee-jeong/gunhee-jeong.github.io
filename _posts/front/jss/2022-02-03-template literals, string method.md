---
layout: single
title: "template literals and string method"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [blog, coding, javascript] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# template literals

ES6에서 추가된 문법 중 하나가 바로 <span style="color:red">template literal</span>!  
원래 <u>String을 작성할 때 따옴표""</u>를 사용했지만, **back tick``**으로도 사용이 가능하다

```javascript
//""작성법
const name = "정건희";
//``작성법
const name = `정건희`;
```

**back tick``**은 그 안에 <span style="color:blue">변수를 넣어서 표현</span>이 가능!

```javascript
const hi = "안녕하세요. 저는 " + name + " 입니다.";
const hi = `안녕하세요. 저는 ${name} 입니다`;
```

# string method

그 동안 string에서 <u>특정 string을 찾기 위해</u> **indexOf**를 사용했고  
ES6에서는 3가지의 method가 추가로 생겨났다  
(startsWith, endsWith, includes)

```javascript
const email = "kyle4619@naver.com";

console.log(email.startsWith("ky")); //output == true
console.log(email.endsWith("com")); //output == true
console.log(email.includes("@naver")); //output == true
```

# assignment

## 문제설명

handleEdit 함수를 구현해주세요

- 이 함수는 nickname, interests라는 두 string을 인자로 받습니다
- nickname은 유저의 닉네임을, interests는 유저의 관심사를 의미한다
- interests에는 여러 관심사를 적을 수 있습니다. 그때 그 관심사의 구분을 콤마를 이용합니다
- 예를 들어서 입력 값이 nickname = "뚜비" , interests = "방탈출,테니스,멍 때리기"라고 할 때,  
  아래와 같은 Object를 리턴해야 합니다

  ```javascript
  {
  nickname: "뚜비",
  interests: ["방탈출","테니스","멍 때리기"],
  bio: "제 닉네임은 뚜비입니다. 취미는 방탈출,테니스,멍 때리기입니다."
  }
  ```

- 주어진 코드

  ```javascript
  let nickname = "뚜비";
  let interests = "방탈출,테니스,멍 때리기";

  const handleEdit = (nickname, interests) => {};
  ```

## 문제풀이

- 나의 풀이

  ```javascript
  const handleEdit = (nickname, interests) => {
    const result = {
      nickname: nickname,
      interests: interests.split(","),
      bio: "제 닉네임은 뚜비입니다. 취미는 방탈출,테니스,멍 때리기입니다.",
    };
    return result;
  };
  ```

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
