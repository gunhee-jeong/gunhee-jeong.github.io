---
layout: single
title: "Code Refactoring"
# categories: Git
categories:
  - Memo # HTML CSS JavaScript Server Algorithm Wecode Programmers CS vsCode
tag: [wecode, code refactoring, bottom-up, 회고록] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Refactoring

코드는 한 번의 작성으로 끝나는 것이 아니다. 계속되는 추가와 수정을 겪게 된다.  
그렇기 때문에 `유지보수`를 용이하게 하기 위해서 <u>코드의 가독성과 확장성</u>이 좋아야한다.

리팩토링이란, 코드의 가독성과 확장성을 좋게 만드는 작업을 의미한다.  
리팩토링은 `소프트웨어의 겉보기 동작은 그대로 유지`한 채,  
<span style="color:red">코드를 이해하고 수정하기 쉽도록 내부 구조를 변경</span>하는 기법'이다.

`단순히 많은 기능을 구현할 줄 안다고하여 좋은 개발자가 아니다!`  
<span style="color:red">효율적이고 확장성</span> 있는 코드 그리고 <span style="color:red">유지보수가 용이한 코드</span>를 작성할 수 있도록 노력해야한다.  
<span style="color:red">하나의 기능을 구현하더라도 좋은 코드가 무엇인지 충분히 고민하고 code를 작성해나가자!</span>

## console.log 지우기

code에서 테스트가 지난 console.log는 지우자.  
테스트를 할 때는 필수적으로 사용하지만, 최종 결과물에 있어서는 포함되지 않도록 살피자.

## #id, .class명, 변수명, 함수명을 직관적으로 드러나도록 작성하자

<img src="https://user-images.githubusercontent.com/87808288/153696436-bbeab699-272a-4cda-9abc-afe9e68e4a1c.png" width="400" height="200">  
개발자에게 `'이름 짓기'`란 힘들어하는 대표적인 것들 중 하나이다.  
하지만 이들 <span style="color:red">식별자명을 직관적으로 드러나도록</span> 작성하는 것이 중요하다.

```java
// bad
let value = "Tom";
let value2 = "Cruise"

// good
let firstName = "Tom"
let lastName = "Cruise"
```

사실 기능적인 것에 있어서는 전혀 문제가 없다.  
하지만 내가 짠 <u>code를 타인들과 공유하고, 그리고 이것을 다시 볼 미래의 나를 위해서</u>라도  
직관적으로 알 수 있는 이름 짓기에 고민하고 작성해야한다.

## 들여쓰기

프로그래밍 언어에서 <u>규칙성이 있는 들여쓰기</u>는 가독성 측면에서 아주 중요한 부분이다.

## semantic tag의 사용

HTML에는 다양한 tag가 존재하고, 그중에서도 `Semantic tag`를 적절하게 사용하는 것은  
<span style="color:red">가독성 + SEO 측면</span>에서 너무나 중요하다.

## img tag의 alt 속성을 반드시 부여하자

`img 태그`를 사용할 때는 <spna style="color:red">반드시 alt 속성을 부여</span>해야한다.

- 이미지가 로딩되지 않을 경우 alt 속성에 적힌 값이 보여진다
- 시각장애인의 경우 alt 속성을 통해 어떤 이미지가 보여지는지 알 수 있다
- SEO 검색엔진 최적화에서 어떤 img인지 인식하는 코드는 alt 속성이다

## 불필요한 style 속성 작성 지양

- block element에 불필요하게 display: block;를 부여하는 것
- block element에 불필요하게 width: 100%를 부여하는 것

위의 두가지 경우처럼 불필요한 style 속성을 부여할 필요가 없고, 주의해야한다.  
<u>div, article 등 많은 element</u>들은 기본으로 <span style="color:red">display: block;을 default로</span> 적용하고 있다.  
block element들은 기본적으로 <span style="color:red">부모 element의 너비를 모두 차지하고</span> 있다!  
<img src="https://user-images.githubusercontent.com/87808288/153697111-507a6637-5025-42d0-9e4a-d79def4b32d6.png" width="300" height="200">  
&nbsp; 위의 사진처럼 `div태그는 부모 element의 넓이를 모두 차지`하고,  
&nbsp; span 태그와 같은 `inline의 경우에는 content의 길이 만큼만 차지`하고 있다!

## 레이아웃을 bottom-up 방식으로!

레이아웃을 구성할 때 부모 element의 높이를 미리 정해놓고  
자식 element의 크기를 정하는 top-down 방식이 아닌,  
`자식 element의 높이에 따라 부모 element 높이가 유동적으로` 결정되는 방식을 구성해야한다.

레이아웃을 구성할 때 `부모 element의 크기를 고정적으로 정해둔다면`,  
자식 element의 크기가 변함에 따라 <span style="color:red">부모 element의 크기가 유동적으로 변하지 못한다</span>.

- 이런 경우, 자식 element의 크기가 변해야 한다면, 부모 element의 css도 같이 수정해야한다는 불편함이 있다.

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
