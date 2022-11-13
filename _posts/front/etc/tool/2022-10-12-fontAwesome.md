---
layout: single
title: "리액트에서 Font Awesome 사용하기"
# categories: Git
categories:
  - Tool # HTML CSS JavaScript Server Algorithm Wecode Programmers CS vsCode
tag: [FontAwesome] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-10-12T11:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.crimson {
  color: crimson;
  font-weight: bold;
}

.mediumblue {
  color: mediumblue;
  font-weight: bold;
}

.forestgreen {
  color: forestgreen;
  font-weight: bold;
}

.black {
  color: black;
  font-weight: bold;
}
</style>

# 리액트에서 폰트어썸 사용하기
(DaleSeo) : [React 에서 Font Awesome 사용하기](https://www.daleseo.com/react-font-awesome/)

# 🔴 Font Awesome 의 SVG
Font Awesome 5 부터는 SVG 기반 아이콘을 지원하고 있다. SVG 기반의 아이콘은 성능적인 측면에서 유리한 점이 많다.

> SVG?  
SVG 는 "Scalable Vector Graphics" 의 약자로 각 위치 값을 표시하는 벡터와 같은 방식의 2차원 그래픽용 XML 기반 형식이다. SVG 는 어떤 디바이스 크기에도 깨지지 않고, 마크업 언어로 이루어져 CSS 와 JavaScript 로 수정이 가능하며 우리가 웹상에서 보는 움직이는 텍스트와 아이콘은 모두 SVG 아이콘이다.

기본적으로 PNG 와 SVG 아이콘을 비교하면 PNG 는 테두리가 흐릿하지만 SVG 는 선명한 이미지를 갖는다.

PNG 나 JPG 는 비트맵 기반의 이미지로 각 항목에서 하나 이상의 정보 비트를 가지고 있고, 반면에 SVG 는 벡터 기반으로 각 좌표에 점을 이어서 만들어진다. 벡터 기반의 아이콘은 확대나 축소에도 깨지지 않고 선명하게 보이는 것이 이러한 이유 때문이다.

# 🔴 패키지 설치
```bash
npm i @fortawesome/fontawesome-svg-core
```

먼저 위의 명령어와 같이 Font Awesome 의 SVG 기반 아이콘을 활성화 시키기 위한 기본 패키지를 설치하게 된다.

```bash
npm i @fortawesome/free-solid-svg-icons @fortawesome/free-regular-svg-icons @fortawesome/free-brands-svg-icons
```

그리고 위의 명령어와 같이, Font Awesome 에 아이콘에 관한 패키지를 설치한다. Solid, Regular 등과 같이 여러 개의 패키지들이 존재한다. 위의 명령어에서는 Solid, Regular, Brands 이렇게 3개의 카테고리에 대한 패키지를 설치했지만 3개를 모두 설치할 필요는 없다. 자신이 사용하게 될 아이콘이 속한 카테고리만을 설치해도 상관없다.

```bash
npm i @fortawesome/react-fontawesome
```

마지막으로 위의 명령어와 같이 Font Awesome 을 React 컴포넌트 형태로 사용할 수 있도록 해주는 패키지를 설치하면 된다.

# 🔴 Font Awesome 아이콘 임포트 하기
웹에서 바로 Font Awesome 을 사용하면 일반적으로 수천개의 아이콘을 모두 로드해야하므로 이는 매우 비효율적이다. 그러나 React 에서는 특정 카테고리에서 필요한 아이콘만을 임포트할 수 있으므로 큰 장점을 가진다.

@fortawesome/react-fontawesome 패키지를 사용하기 때문에 직접 &lt;svg/&gt; 태그를 사용할 필요가 없다. 대신에 이 패키지에서 제공하는 FontAwesomeIcom 컴포넌트 위에서 임포트한 Font Awesome 아이콘을 icon prop 으로 넘겨주어야 한다.

```jsx
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faChair } from '@fortawesome/free-solid-svg-icons';

export default function FooterPage() {
  return (
    <>
      <div>footer</div>
      <FontAwesomeIcon icon={faChair} size="2x" />
    </>
  );
}

// const SIZES = ["xs", "sm", "lg", "2x", "3x", "5x", "7x", "10x"];
```

<!-- ⓵ ⓶ ⓷ ⓸ ⓹ ⓺ ⓻ ⓼ ⓽ ⓾ -->

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
