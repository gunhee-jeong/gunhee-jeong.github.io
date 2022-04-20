---
layout: single
title: "Node.append()와 Node.appendChild()"
# categories: Git
categories:
  - JavaScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [document, dom] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Node.append()

- `Node.append() method`는 <span style="color:red">Node object</span>를 사용할 수 있다  
  `append()`를 사용하여 <u>부모 노드에 자식 노드를 추가</u>할 수 있다

  ```java
  // javascript
  const parent = document.creatElement('div');
  const child = document.creatElement('p');

  parent.append(child);
  ```

  위의 코드의 결과로

  ```html
  <!-- html -->
  <div>
    <p></p>
  </div>
  ```

- `Node.append() method`는 <span style="color:red">document string</span>을 사용할 수 있다  
  `append()`를 사용하여 <u>node안의 content를 채워 넣을 수</u>도 있다
  ```java
  //javascript
  const parent = document.createElement('div');
  parent.append('append 예시');
  ```
  위의 코드의 결과는
  ```html
  <!-- html -->
  <div>append 예시</div>
  ```
- 예시

  ```java
  //javascript
  const div = document.creatElement('div');
  const span = document.creatElement('span');
  const p = document.creatElement('p');

  document.body.append(div, 'hello', span, p);
  ```

  위에서는 우선 div 태그, span 태그 p 태그를 설정하였고  
  <span style="color:green">document.body.append</span>를 통해서 <u>body 태그 안에</u> `자식 노드들을 추가`한다

  ```html
  <!-- html -->
  <body>
    <div></div>
    hello
    <span></span>
    <p></p>
  </body>
  ```

# Node.appendChild()

- <span style="color:red">appendChild()</span> 메서드는 append() 메서드와는 달리 `오직 node 객체만을 받을 수` 있다.  
   또한 append() method에서는 여러 개의 node와 string을 받을 수 있었지만,  
   `appendChild() method`는 <u>한 번에 하나의 node만 추가</u>할 수 있다.

  ```java
  // javascript
  const parent = document.creatElement('div');
  const child = document.creatElement('p');

  parent.appendChild(child);
  ```

  위의 코드의 결과로

  ```html
  <!-- html -->
  <div>
    <p></p>
  </div>
  ```

  이 부분에서는 appendChild()와 append()의 차이를 구분할 수 없다  
  그러나 appendChild()를 사용하여 `DOMString을 넣을 경우에는 error`가 발생한다

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
