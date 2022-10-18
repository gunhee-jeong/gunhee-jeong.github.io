---
layout: single
title: "Types of TS"
# categories: Git
categories:
  - TypeScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [노마드코더] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-10-18T09:30:00+09:00
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
</style>

# Types of TS
```jsx
let a : number = 1;
let b : string = "hi";
let c : boolean[] = [true];
```

```ts
const player : {
    name: string,
    age?: number,
} = {
    name: 'gunhee',
};

console.log(palyer.age); // undefined

if (player.age && player.age < 10) {

}
```

위의 코드에서 <u>player 라는 객체</u>는 name 이라는 프로퍼티 키는 <span class="mediumblue">required</span> 로 설정했고, age 라는 프로퍼티 키는 <span class="mediumblue">optional</span> 로 사용한다고 설정했다. 

```jsx
type Player = {
  name: string,
  age?: number,
};

const gunhee: Player = {
  name: 'gunhee',
};

const gildong: Player = {
  name: 'gildong',
};
```

위의 코드와 같이 Player 라는 타입을 만들어서 중복되는 부분을 줄일 수 있다. 이렇게 <span class="crimson">aliases</span> 를 만들면 <u>타입을 재사용</u>할 수 있게 된다.

```jsx
type Age = number;

type Player = {
  name: string,
  age?: Age,
};

const gunhee: Player = {
  name: 'gunhee',
};

const gildong: Player = {
  name: 'gildong',
};
```

또한 위의 코드와 같이 더 많은 alias 를 만드 수도 있다.

```jsx
type Age = number;

type Player = {
  name: string,
  age?: Age,
};

function playerMaker(name: string) : Player {
  return {
    name
  }
}

const playerMaker = (name: string) : Player => ({name}); // 화살표 함수 사용시 타입 설정방법

const gunhee = playerMaker("gunhee");
gunhee.age = 2;
```

# 🔴 readonly
```jsx
type Age = number;

type Player = {
  readonly name: string,
  age?: Age,
};

const playerMaker = (name: string) : Player => ({name});
const gunhee = playerMaker("gunhee");

gunhee.age = 12;
gunhee.name = "gildong"; // error
```

```jsx
const number: readonly number[] = [1, 2, 3, 4];
number.push(5); // error
```

위의 코드에서 readonly 로 설정된 프로퍼티는 수정할 수 없게 된다.

```jsx
const player: [string, number, boolean] = ["gunhee", 1, true];

const player: readonly [string, number, boolean] = ["gunhee", 1, true];
player[0] = "hi"; // error
```

# 🔴 any
`any` 는 타입스크립트에서 <u>아무 타입이나 가져올 수</u> 있게 된다. any 는 <span class="forestgreen">타입스크립트를 빠져나올 수</span> 있게 하는 방법이다. any 를 사용하면 타입스크립트의 모든 보호장치를 비활성화 시킨다.

```jsx
const a: any[] = [1, 2, 3, 4];
const b: any = true;

a + b
```

# 🔴 unknown
```jsx
let a: unknown;

if (typeof a === 'number') {
  let b = a + 1;
}

if (typeof a === 'string') {
  let b = a.toUpperCase();
}
```

# 🔴 void
`void` 는 <u>아무것도 return 하지 않는 함수</u>를 대상으로 사용하게 된다.

```jsx
function hello() {
  console.log('x');
}
```

위의 코드에서 hello 함수는 타입이 void 이다.

# 🔴 never
never 는 함수가 절대 반환하지 않을 때 발생한다.

```jsx
function hello(): never {
  throw new Error("xxx");
}
```

```jsx
function hello(name: string || number) {
  if (typeof name === "string") {
    name // string
  } else if (typeof name === "number") {
    name // number
  } else {
    name // never
  }
}
```

<!-- <span style="color:mediumblue"> -->

<!-- ① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨-->

<!-- 메소드 위에 변수 선언, 메소드  안에 메소드, 메소드 끝나고 리턴 -->

<!-- ### 2. Link 넣기

```

유형 1: (설명어를 입력) : [gunhee's coding blog](https://gunhee-jeong.github. io/)
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
<span style="color:crimson">빨간 글씨</span> -> 글자색
이것이 `인라인` 입니다 -> 인라인 코드
```

**진하게** -> 볼드
_기울여서_ -> 이탤릭체
~~취소선~~ -> 취소선
<u>밑줄넣기</u> -> 밑줄
<span style="color:crimson">빨간 글씨</span>
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
</details> -->
