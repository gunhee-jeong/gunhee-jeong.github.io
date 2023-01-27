---
layout: single
title: "TypeError: (0,  _utils.default) is not a function"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [모달창, 클릭 이벤트] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2023-01-27
last_modified_at: 2023-01-27
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.red {
  color: crimson;
}

.blue {
  color: mediumblue;
}

.green {
  color: forestgreen;
}
</style>

🔥 **글의 목적**: 이 에러를 다시 마주칠 나 자신을 위해 그리고 위의 에러로 인해 고생할 다른 개발자를 위해 에러 해결 방법을 공유하고자 글을 작성한다.

<img src="https://user-images.githubusercontent.com/87808288/214998127-012207c9-6d96-4a85-b76a-c98722ac6b64.png" width="70%">

<span class="green">test code</span>를 짜면서 위의 이미지와 같은 에러를 마주했다. 며칠이나 위의 버그의 원인을 찾기 위해 개인적으로 고생을 많이 했다. 처음에는 위의 에러 메시지 자체를 <span class="blue">구글링할 생각을 하지 못했다</span>…… 아니 왜 구글링부터 안 했을까라고 어이가 없을 수 있겠지만 개인적으로는 테스트 코드를 Redux 환경에서만 사용해 보다가 useState를 사용하기 위해 처음 테스트 코드를 작성했기 때문에 당연히 <span class="red">내가 테스트 코드를 잘못 짜서 생기는 에러라고</span> 나도 모르게 확신했던 것이 문제였다. 그리고 내가 useState를 테스트하는 방법에도 실제로 문제가 있었다.

다시 에러의 해결로 돌아와서 이 에러는 결론적으로, 파일 어딘가에 있는 <span class="red">import 문을 잘못 사용한 것이 원인</span>이었다. 아래의 코드를 살펴보자.

```jsx
// utils.js
export function get({ page, key }) {
  return (obj) => obj[page][key];
}

export function updateSlide({ targetName, isMotion }) {
  if (targetName === 'previousArrow') {
    return ({ number }) => ({
      number: number - 1,
      isMotion,
    });
  }

  return ({ number }) => ({
    number: number + 1,
    isMotion,
  });
}
```

```jsx
// ProductDetail/ProductWrapper.jsx

// ......

// 잘못된 import 문
import updateSlide from '../utils';

// 에러를 잡기 위해 올바르게 수정한 import 문
import { updateSlide } from '../utils';
// ......
```

ProductWrapper.jsx에서는 utils.js의 updateSlide 함수를 import 하여 사용하게 된다. 그런데 ‘<span class="green">잘못된 import 문</span>’의 경우, <span class="blue">중괄호({})를 사용하지 않았다</span>. 중괄호로 묶지 않는 경우는 <span class="red">export default 문을 사용한 함수</span>를 import 할 때 유효한 문법이다. utils.js에는 다를 함수들도 export되어 있기 때문에 중괄호로 묶어서 updateSlide 함수를 import 해야 한다.

내가 모르고 있던 문법이었다면 속이 덜 상했을 텐데, 이미 잘 사용하고 있던 부분에서 에러가 발생했고 이를 빠르게 디버깅하지 못해 개인적으로 너무 아쉬웠다. 분명… 확인했던 부분 같은데, 이 당시 온 신경이 테스트 코드에 가있어서 애먼 코드를 계속 고쳤다. 이 한 줄로 인해 거의 3일이라는 시간 동안 useState와 관련된 테스트 코드를 수정하고 있었다. 이제 이 에러를 마주해도, 내가 작성한 이 글을 읽으며 10초 안에 에러를 해결할 테니 그만 속상해해야겠다.

<!-- ① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨-->

<!-- ### 2. Link 넣기

```

유형 1: (설명어를 입력) : [gunhee's coding blog](https://gunhee-jeong.github.io/)
유형 2: (URL 자동연결) : <https://gunhee-jeong.github.io/>
유형 3: (동일 파일 내 '문단으로 이동') : [1. Header로 이동](###-1-header)

```

```bash
.next/static
        ├── AbmKMg9BFeVUuJ7lsQ1w8
        ├── chunks                 // 여러 페이지에서 공통으로 사용되는 번들 파일
        │       └──  pages         // 각 페이지의 번들 파일
        ├── runtime                // 웹팩과 next의 런타임과 관련된 번들 파일
        ├── css                    // 애플리케이션의 모든 페이지에 대한 글로벌 CSS 파일
        └── media                  // 정적으로 가져온 이미지 next/image가 여기에 해시 및 복사
```

<details>
<summary class="black">코드</summary>
<div markdown="1">

```jsx
// helloWorld!
const hello = 'hi';
```
</div>
</details>

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
 -->
