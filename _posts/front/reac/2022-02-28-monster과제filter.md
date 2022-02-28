---
layout: single
title: "filter를 사용한 monster 필터 기능"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [wecode, 구조분해할당] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

## flow

<span style="color:red">Monster.js</span>  
&nbsp; <span style="color:orange">SearchBox.js</span>  
&nbsp; <span style="color:orange">CardList.js</span> -> <span style="color:yellow">Card.js</span>

### Monster.js

<span style="color:red">Monster.js</span>에서 `fetch 함수`를 이용하여 const <u>monsters에 array를</u> 전달  
&nbsp; 여기서 setMonsters를 통해 할당된 monsters를 ->  
&nbsp; <span style="color:green"><CardList monsters={monsters} /></span>에 전달함

### CardList.js

##### <span style="color:green">function CardList({ monsters }) {}</span>

Monster.js에서 전달받은 monsters={monsters}은  
<span style="color:green">function CardList({ monsters }) {}</span>를 통해, props를  
<u>구조분해할당</u>하여 const monsters에 props를 할당했다.  
<span style="color:green">function CardList(props) {}</span>를 할 경우,  
console.log(`props`);를 해보면 `{monsters: Array(10)}`가 담긴다.  
&nbsp; `{monsters: [{...}, {...}, {...}......]}`  
&nbsp; <span style="color:green">function CardList({ monsters }) {}</span>는 `const { monsters } = props;`  
&nbsp; 라는 것이 <u>생략된 표현</u>이다.

```js
//CardList.js
function CardList({ monsters }) {
  // console.log(props); output == {monsters: Array(10)}
  // {monsters: [{...}, {...}, {...}......]}
  return (
    <div className="cardList">
      {monsters.map((monster) => {
        return (
          <Card
            key={monster.id}
            id={monster.id}
            name={monster.name}
            email={monster.email}
          />
        );
      })}
    </div>
  );
}
```

##### <span style="color:green">{monsters.map((monster) =></span>

<span style="color:red">Monster.js</span>에서 전달받은 monsters를 `map 함수`를 사용하면 ->  
<u>monster</u>에는 몬스터의 정보가 담긴, <u>하나의 object 씩</u> 정보를 <span style="color:yellow">Card.js</span>에  
보내주게된다.  
&nbsp; 좀 더 정확히 말하면 -> array의 0번 index(object 타입)부터  
&nbsp; 각각의 id, name, email의 정보를 Card.js에 넘겨준다.

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
