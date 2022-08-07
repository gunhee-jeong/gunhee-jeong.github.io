---
layout: single
title: "e.preventDefault()"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [preventDefault, enter, submit] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

<u>a 태그</u>나 `form 태그 안의 button 태그`를 통해 버튼을 누르면 화면이 <span style="color:red">새로고침</span>된다.  
이때 이 <span style="color:red">새로고침을 막기 위해서</span> `preventDefault()가 사용`된다!  
&nbsp; 나또한 form 태그 안의 submit 역할을 하는 button을 눌렀을때도 새로고침이 막고자  
&nbsp; 이 기능을 찾아보게 되었다.

```java
const addComment = (e) => {
    if (isCheckComment) {
      setCommentList(
        commentList.concat(
          {
            author: "gunhee_jeong",
            comment: comment,
          },
        )
      );
      e.preventDefault();
      setComment("");
    } else {
      e.preventDefault();
    }
  };
```

const `isCheckComment`는 <u>boolean 타입의 데이터를 갖는 변수</u>로  
댓글이 1자 이상이면 true, 0자 이면 false를 갖는다.

##### <span style="color:green">if (isCheckComment) {}</span>

if문의 조건식이 true일 때 -> 코드블록이 실행된다.  
&nbsp; const `commentList`에는 <u>배열의 형태로 댓글들이 저장</u>되어있고  
&nbsp; commentList의 `배열 가장 마지막 index로 새로운 댓글이 추가`되어야하므로  
&nbsp; <span style="color:red">concat 메소드</span>를 사용하여 const commentList에 추가한다.  
그렇게 <u>추가된 commentList의 내용</u>이 `rendering되면서 UI로 반영`되고 -> 화면이  
<u>새로고침되기 전에 <span style="color:red">e.preventDefault();</span>를 통해 새로고침을 막게</u>된다!

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
