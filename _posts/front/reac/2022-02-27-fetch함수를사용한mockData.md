---
layout: single
title: "fetch 함수를 이용한 mockData 연결"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [instagram, map] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

## fetch 함수를 이용한 instagram 피드 연결

```java
//Main.js
import { useEffect, useState } from "react";
import Nav from "../../../components/Nav/Nav";
import Feeds from "./Feeds";
......

const Main = () => {
  const [FeedsList, setFeedsList] = useState([]);

  useEffect(() => {
    fetch("http://localhost:3000/data/FeedData.json", {
      method: "GET",
    })
      .then((respose) => respose.json())
      .then((data) => setFeedsList(data));
  }, []);

  return (
    <>
      <div className="Main">
        <Nav />
        <div>
          <main>
            {FeedsList.map((feed, index) => {
              return (
                 <Feeds
                    key={feed.id}
                    num={index}
                    feedsName={feed.userName}
                    feedsContent={feed.content}
                />
              );
            })}
          </main>
          <Aside />
        </div>
      </div>
    </>
  );
};

export default Main;

arr1.map(() => {
  return
})
```

<u>Main component안에</u> child로 `Feeds component`가 위치하고 있다.  
<u>mock data 파일인 FeedData.json</u>를 `fetch함수`를  
통해 Feeds에 보내기 위해서는 <u>Feeds의 UI를 구성하는 태그들이 정의되어있어야</u> 한다.  
&nbsp; 또한 <span style="color:blue">피드의 태그들은 구성이 모두 동일</span>하면서, 그 구성의 `내용물만 바뀌기 때문`에  
&nbsp; <span style="color:red">Feeds는 component로 만들어 관리</span>하는 것이 좋다.

##### <span style="color:green">const [FeedsList, setFeedsList] = useState([]);</span>

<u>fetch 함수를 통해 mock data를 받게</u>되면 -> Feed의 리스트들을 받기 위해  
위의 코드가 필요하다.  
&nbsp; fetch 함수를 통해 <u>array의 형태도 전달받은 Feed의 리스트</u>들은  
&nbsp; `const FeedsList에 배열로` 담긴다.

##### <span style="color:green">{FeedsList.map((feed) => {return <Feeds key={feed.id} num={index} name={feed.userName} feedsContent={feed.content} />;</span>

Main component의 return 안에, child component인 Feeds component를  
정의해야한다.  
그런데 <u>const FeedsList에 피드들이 array의 형태로</u> 담겨있기 때문에  
이를 `하나씩 꺼내어 전달하기위해` <span style="color:red">map 메소드</span>를 사용한다.  
&nbsp; <span style="color:green">FeedsList.map((feed) =>)</span>을 통해 FeedsList에 담긴 0번째 index의 value부터  
&nbsp; feed에 담긴다.  
&nbsp; 그래서 `<Feeds>` component에 FeedsList에서 필요한 data를 물려주기 위해서  
&nbsp; <span style="color:green"><Feeds key={feed.id} num={index}
feedsName={feed.userName}  
&nbsp; feedsContent={feed.content} /></span>  
&nbsp; 이렇게 <u>key</u>, <u>num</u>, <u>feedsName</u>, <u>feedsContent</u>라는 <span style="color:blue">속성을 추가</span>해준다.

```java
//Feeds.js
import { useState, useEffect } from "react";
import CommentList from "./CommentList";
......
const Feeds = (props) => {
  const [comment, setComment] = useState("");
  const [commentList, setCommentList] = useState([]);
  const isCheckComment = comment.length > 0;
  ......

  return (
    <div className="feeds">
      ......
      <article className={props.num}>
            <span>{props.feedsName}</span>
              <span className="commentText">{props.feedsContent}</span>
      ......
          <CommentList
            key={comments.id}
            num={index}
            author={comments.author}
            comment={comments.comment}
          />
          <form id="chat-form" onSubmit={addComment}>
            <input
              onChange={getComment}
              type="text"
              placeholder="댓글 달기..."
              value={comment}
            />
            <button className="post">게시</button>
            {/* form 안의 button은 default로 submit을 하는데 type을 button으로 주변, 그 default가 작동X*/}
          </form>
      ......
</div>
  )
}
```

##### <span style="color:green">const Feeds = (props) => {}</span>

이제 `Main component에서 전달받은 데이터`를 사용하기 위해서 <span style="color:red">props</span>를 사용한다.  
props는 properties를 의미하는데 ->  
단어의 뜻 그대로 <u>component의 속성값</u>이다.  
&nbsp; <span style="color:green">console.log(props)</span>를 해보면 -> <span style="color:red">object</span> 데이터타입으로  
&nbsp; {num: 0, feedsName: 'Hello_name', feedsContent: 'wecome hello hi bye'}  
&nbsp; 으로 Main component에서 `FeedsList.map`을 사용하였기 때문에  
&nbsp; 배열인 <u>FeedsList의 element 하나씩</u> console.log에 출력된다.

## fetch 함수를 이용한 instagram 댓글 연결

mock data 파일인 <u>commentData.json</u>을 `fetch 함수`를 통해  
CommentList에 보내기 위해서는 `CommentList의 UI`를  
구성하는 <u>태그들이 정의되어 있어야</u>한다.  
&nbsp; 댓글 tag들도 피드와 마찬가지로, 내용물만 바뀌기에  
&nbsp; <span style="color:red">CommentList도 component로</span> 관리하는 것이 좋다.

```java
//Feeds.js
import { useState, useEffect } from "react";
import CommentList from "./CommentList";
......
const Feeds = (props) => {
  const [comment, setComment] = useState("");
  const [commentList, setCommentList] = useState([]);
  const isCheckComment = comment.length > 0;
  ......
  useEffect(() => {
    fetch("http://localhost:3000/data/commentData.json", {
      method: "GET",
    })
      .then((response) => response.json())
      .then((data) => setCommentList(data));
  }, []);

  return (
    <div className="feeds">
      ......
      <article className={props.index}>
            <span>{props.name}</span>
              <span className="commentText">{props.content}</span>
      ......
          {commentList.map((comments, index) => {
            return (
              <CommentList
                key={comments.id}
                num={index}
                author={comments.author}
                comment={comments.comment}
              />
            );
          })}
          <form id="chat-form" onSubmit={addComment}>
            <input
              onChange={getComment}
              type="text"
              placeholder="댓글 달기..."
              value={comment}
            />
            <button className="post">게시</button>
            {/* form 안의 button은 default로 submit을 하는데 type을 button으로 주변, 그 default가 작동X*/}
          </form>
      ......
</div>
  )
}
```

##### <span style="color:green">.then((data) => setCommentList(data));</span>

`fetch 함수`를 통해 json 파일을 -> js로 변환받았고, 이를  
<u>setCommentList를 통해</u> `commentList에 array 데이터` 타입으로 할당했다.

##### <span style="color:green">{commentList.map((comments, index) => {return (<CommentList key={comments.id} num={index} author={comments.author} comment={comments.comment}/>)})};</span>

const <u>commentList</u>에 댓글들이 `array 형태로` 담겨있기 때문에 이를  
<u>하나씩 꺼내서 전달하기 위해</u> 댓글도 마찬가지로 <span style="color:red">map 메소드</span>를 활용한다.  
&nbsp; <span style="color:green">commentList.map((comments, index) =></span>를 통해서  
&nbsp; commentList에 담긴 <u>0번째 index의 value부터 comments에</u> 담긴다.  
&nbsp; `<CommentList>` component에 commentList에서 필요한 <u>data를 물려주기 위해</u>  
&nbsp; <span style="color:green"><CommentList key={comments.id} num={index} author={comments.author}</span>  
&nbsp; <span style="color:green">comment={comments.comment}/></span>  
&nbsp; 이렇게 key, num, author, comment라는 속성을 추가했다.

##### <span style="color:green">const CommentList = (feedsProps) => {}</span>

```java
//CommentList.js
const CommentList = (feedsProps) => {
  return (
    <li className={feedsProps.num}>
      <span>
        {feedsProps.author} {feedsProps.comment}
      </span>
      <span>&nbsp;</span>
      <span className="trashIcon">
        <i className=""></i>
      </span>
    </li>
  );
};
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
