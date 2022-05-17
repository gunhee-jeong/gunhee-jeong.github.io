---
layout: single
title: "block과 inline에 관하여"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [inline, block] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Block과 Inline

## Block

<span style="color:red">block</span>은 `content가 존재하지 않아도` <u>화면에는 box가 형성</u>된다.  
`div 태그`가 대표적인 **block** 형식의 tag이다. 그래서 <u>한 줄에 하나씩 box</u>가 형성된다.  
<img src="https://user-images.githubusercontent.com/87808288/152723573-52f7deca-9d2e-423e-9e1b-c0802c7c5cf1.png" width="300" height="200">

- <u>div 태그에 width 100%;를 부여하지 않도록</u> 주의해야한다!  
  <span style="color:red">div 태그 자체가 block 형식</span>의 tag이므로, `한 칸 전체를 모두 자치`한다.  
  때문에 *width 100%;를 주는 것*은 <span style="color:blue">중복하여 div 태그를 설정하는 것</span>이 된다.

## inline

tag가 <span style="color:red">inline</span>이라면, 그 `칸에 빈 공간만 있다면 같은 칸에 여러 개가` 만들어진다.  
그리고 <u>content의 크기 만큼 공간을 형성</u>하므로 -> <span style="color:red">content를 담는 상자</span>라고 생각할 수 있다!
<img src="https://user-images.githubusercontent.com/87808288/152724646-82a7284c-aafc-449d-83b6-0bf4056c36ed.png" width="500" height="200">  
span 태그는 content를 담는 상자이기 때문에 -> `span 태그 안의 content가 없다면`,  
<span style="color:blue">span 태그는 화면에도 표시되지 않는다</span>.

## inline-block

<img src="https://user-images.githubusercontent.com/87808288/152725325-a5a5c67a-990b-4c21-bc72-9516453085cd.png" width="350" height="200">  
`div 태그 안에는 content가 존재하지 않는데`, display 설정을 <span style="color:red">display: inline-block;</span>으로  
<u>inline의 특성과 block의 특성 두 가지를</u> 가질 수 있게 설정하였다.  
inline이기 때문에 한 칸에도 여러 개의 상자를 가지고, 또한 block이기 때문에 content가 없지만  
화면에 표현되고 있다.

<!-- tcp스쿨 -->
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
