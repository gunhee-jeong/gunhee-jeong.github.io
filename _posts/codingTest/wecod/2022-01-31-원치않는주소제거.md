---
layout: single
title: "wecode 코딩테스트, 원치 않는 주소 제거하기"
categories: coding test 
tag: [blog, coding, JavaScript, front-end, front, coding test] #tag는 여러개 가능함
categories:
  - Wecode # CSS HTML JavaScript React Programmers Wecode CS Github vsCode Blog (파일이름으로 설정함)
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
  # nav: "docs" #네비게이션에 있는 docs를 의미함
---

# 문제설명

- address는 String 타입의 변수
- 함수를 return시 "경기도 분당구 중앙공원로 53"을 반환받아야함
- address에 '도'와 '시'는 딱 한번만 포함되어 있어야 합니다
- 주어진 함수

  ```javascript
  let address = "경기도 성남시 분당구 중앙공원로 53";

  function sliceCityFromAddress(address) {
    return result;
  }

  console.log(sliceCityFromAddress(address));
  ```

# 문제풀이

- 나의 코드

  ```javascript
  const address = "경기도 성남시 분당구 중앙공원로 53";

  function sliceCityFromAddress(address) {
    return address
      .split(" ")
      .filter((x) => (x[2] == "시" ? false : true))
      .join(" ");
  }

  console.log(sliceCityFromAddress(address));
  ```

  - address의 String을 ['경기도', '성남시', '분당구', '중앙공원로', '53']의 **array 형태로** 바꾸기 위해서 <span style="color:red">split(" ")</span>을 사용함
  - ['경기도', '성남시', '분당구', '중앙공원로', '53']<span style="color:red">.filter</span>를 사용하였고 <u>x의 2번 index</u>에 **'시'가 있다면 false를 전달**하는 방식으로  
    '성남시'를 제거하여 ['경기도', '분당구', '중앙공원로', '53']이 반환되도록 만들었다!
  - 마지막으로 ['경기도', '분당구', '중앙공원로', '53']<span style="color:red">.join(' ')</span>를 사용하여 정답인 '경기도 분당구 중앙공원로 53'를 완성했다!

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
