---
layout: single
title: "Instagram 댓글 기능"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [preventDefault, concat] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

```java
//Main Component
const Main = () => {
  ......
  const [comment, setComment] = useState('');
  const [commentList, setCommentList] = useState([]);
  const isCheckComment = comment.length > 0;

  const getComment = (e) => {
    setComment(e.target.value);
  };

  const addComment = (e) => {
    if (isCheckComment) {
      setCommentList(
        commentList.concat({
          author: "gunhee_jeong",
          comment: comment,
        })
      );
      e.preventDefault();
      setComment("");
    } else {
      e.preventDefault();
    }
  };

  useEffect(() => {
    fetch("http://localhost:3000/data/commentData.json", {
      method: "GET",
    })
      .then((response) => response.json())
      .then((data) => setCommentList(data));
  }, []);

  return (
    ......
    <CommentList newCommentList={commentList} />
      <form id="chat-form" onSubmit={addComment}>
        <input
          onChange={getComment}
          type="text"
          placeholder="댓글 달기..."
          value={comment}
        />
        <button className="post">게시</button>
        {/* form 안의 button은 default로 submit을 하는데 type을 button으로 주면, 그 default가 작동X*/}
      </form>
    ......
  )
}
```

우선 `useState`를 어떤 용도를 위해 사용할지 생각해야했다.  
&nbsp; input 태그를 사용해 -> <u>value를 입력하면 이것을 담을 변수</u>가 필요하고  
&nbsp; 그리고 "댓글 mock data"에 <u>입력된 value를 집어 넣어야</u>했다.

##### <span style="color:green">const [comment, setComment] = useState('');</span>

input 태그를 통해 댓글을 입력하면 -> setComment를 통해,  
comment에 값을 할당한다.

##### <span style="color:green">const [commentList, setCommentList] = useState([]);</span>

그리고 위에서 받은 comment를 setCommentList를 통해  
`commentList에 추가되도록` 값을 할당한다.

##### <span style="color:green">const getComment = (e) => {setComment(e.target.value);};</span>

input 태그를 통해 <u>댓글을 입력하면</u> `getComment 함수`가 실행된다.  
<u>댓글을 입력하면</u> 그 value를 setComment를 통해 -> `변수 comment에 저장`한다.

##### <span style="color:green">const addComment = (e) => {}</span>

그리고 `form 태그`에서 submit이 되면(enter or button)  
<u>onSubmit={addComment}</u>이 실행된다.  
<span style="color:green">const isCheckComment = comment.length > 0;</span>에서 form 태그 안의 input에  
<u>아무것도 적지 않은 상태에서 submit 되지 못하도록</u> `boolean 타입의 데이터`가  
들어가는 변수를 만들었다.  
&nbsp; 댓글의 글자수가 1개 이상이면 <u>isCheckComment에는 true가 할당</u>되고 ->  
&nbsp; 조건문의 코드블록을 실행하면서, `setCommentList를 통해서 댓글이 추가`되지만  
&nbsp; 조건식이 <u>false라면 아예 댓글이 추가되지 못한다.</u>

##### <span style="color:green">if (isCheckComment) {}</span>

addComment 함수가 실행되고, 그 안의 if문의 조건식까지 ture라면 코드블록이  
실행된다.  
<u>const commentList</u>에는 `배열의 형태로 댓글들이 할당`되어있고,  
commentList의 <span style="color:red">배열 가장 마지막 index로 새로운 댓글이 추가되어야</span>하므로  
<span style="color:red">concat 메서드</span>를 사용하여 const commentList에 추가한다.  
&nbsp; 그렇게 <u>추가된 commentList의 내용이 rendering되면서 UI로 반영</u>되고 ->  
&nbsp; 화면이 새로고침되기 전에 `e.preventDefault();`를 통해 <u>새로고침을 막게</u>된다.

<!-- 메소드 위에 변수 선언, 메소드 안에 변수 선언, 메소드 안에 메소드, 메소드 끝나고 리턴 -->

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
