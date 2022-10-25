---
layout: single
title: "Interfaces"
# categories: Git
categories:
  - TypeScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [노마드코더, 객체지향 프로그래밍] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-10-24T09:20:00+09:00
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

# Interfaces

```ts
type Words = {
    [key: string]: string,
};

class Dict {
    private words: Words;

    constructor() {
      this.words = {}
    }

    add(word: Word) { // 이 파라미터가 이 클래스의 인스턴스이기를 원하면 이렇게 사용할 수 있다.
    // 이렇게 클래스를 타입처러 사용할 수 있다.
      if (this.words[word.term] === undefined) {
        this.words[word.term] = word.def;
      }
    }

    getDefine(term: string) {
      return this.words[term];
    }

    deleteWord(term: string) {
        if (this.words[term] !== undefined) {
            delete this.words[term];
        }
    }

    update(term: string, def: string) {
        if (this.words[term] !== undefined) {
            this.words[term] = def;
        }
    }

    showAll() {
        Object.entries(this.words).forEach(([name, recap]) => console.log(`${name}(은)는 ${recap} 입니다`));
    }

    count() {
        return Object.keys(this.words).length;
    }
}

class Word {
  constructor(
    public readonly term: string, // readonly 를 통해 읽기 전용으로 만듦
    public readonly def: string,
  ) {}
}

const kimchi = new Word("kimchi", "한국의 음식");
const bulgogi = new Word("bulgogi", "한국의 전통 음식");
const bibimbap = new Word("bibimbap", "한국의 건강한 음식");

kimchi.def = "xxx" // error

const dictionary = new Dict();
dictionary.add(kimchi);
dictionary.add(bulgogi);
dictionary.add(bibimbap);
```

위의 코드에서 class Word 는 redaonly 를 통해서 읽기 전용으로 사용한다. 따라서 <u>kimchi.def = "xxx"</u> 를 사용하여 수정하는 것에 있어서 에러를 발생시켜 데이터를 보호한다.

```ts
type Player = {
  nickname: string,
  healthBar: number,
};

const gunhee: Player = {
  nickname: "gunhee",
  healthBar: 10,
};

// 위의 타입을 아래와 같이 사용할 수도 있다.

type Nickname = stirng;
type Health = number;
type Friends = Array<string>
type Player = {
  nickname: Nickname,
  healthBar: Health,
};

//

type Food = string;

const kimchi: Food = 'delicious';
```

아래의 코드와 같이 타입을 지정된 옵션으로만 제한할 수도 있다.

```ts
type Team = "red" | "blue" | "yellow";
type Health = 1 | 5 | 10;

type Player = {
  nickname: string,
  team: Team,
  health: Health,
};

const gunhee: Palyer = {
  nickname: "gunhee",
  team: "pink", // error
};
```

인터페이스(Interface) 란 오브젝트의 모양을 설명하는 한 방법을 말한다. 아래의 코드를 살펴보자.

```ts
type Team = "red" | "blue" | "yellow";
type Health = 1 | 5 | 10;

// type Player = {
interface Player { // Interface
  nickname: string,
  team: Team,
  health: Health,
};

const gunhee: Palyer = {
  nickname: "gunhee",
  team: "pink", // error
};
```

기본적으로 타입은 우리가 원하는 모든 것이 될 수 있다. 그러나 위의 코드에서 보이는 interface 는 오직 한 가지의 용도만을 가진다. 그리고 그것은 오브젝트의 모양을 특정해주는 것이다.

타입스크립트에게 오브젝트의 모양을 알려주는 방법에는 두 가지가 있다. 하나는 type 을 사용하여 오브젝트의 모양을 써주는 방법이고, 다른 하나가 바로 인터페이스 이다. 이 두 가지 방법은 오브젝트의 모양을 결정한다는 같은 역할을 한다.

하지만 다른 점은, `type` 은 interface 키워드에 비해 <u>더 다양하게 활용</u>할 수 있다. `interface` 는 <span class="mediumblue">오로지 오브젝트의 모양을 타입스크립트에게 설명</span>해 주기 위해서만 사용되는 키워드이다.

```ts
// 인터페이스를 사용한 모습
interface User {
  name: string,
}

interface Player extends User {
}

const gunhee: Player = {
  name: "gunhee",
};

// 타입을 사용한 모습
type User = {
  name: string,
}

type Player = User & {
}

const gunhee: Player = {
  name: "gunhee",
};
```

위의 코드에서 interface 를 사용하면 class 를 사용하는 개념과 유사하다. 인터페이스는 클래스와 닮았다. 이렇게 인터페이스는 <span class="mediumblue">타입스크립트에게 오브젝트의 모양을 설명해주기 위해서 존재</span>한다. 인터페이스를 사용하는 것이 더 객체지향 프로그래밍 처럼 보여서 이해하기 더 쉽게 해준다. <u>인터페이스는 클래스가 아니지만</u> <span class="mediumblue">클래스의 모양을 특정할 수 있게 해주는 간단한 방법</span>이다

인터페이스의 또 다른 특징은 <span class="forestgreen">프로퍼티 들을 축적</span>시킬 수 있다는 것이다. 아래의 코드를 살펴보자.

```ts
interface User {
  name: string,  
}

interface User {
  lastName: string,
}

interface User {
  health: number,
}

const gunhee: User = {
  name: "gunhee",
  lastName: "jeong",
  health: 10,
};
```

이렇게 각각 인터페이스를 3번 만들었지만, 타입스크립트는 알아서 하나로 합쳐준다. type 을 가지고 이렇게 각각 3번 만들 수는 없다.

기본적으로 인터페이스는 가볍고, 인터페이스는 컴파일하면 자바스크립트로 바뀌지 않고 사라지게 된다.

```ts
// abstract class
abstract class User {
  constructor(
    protected firstName: string,
    protected lastName: string,
  ) {}

  abstract sayHi(name: string): string,
  abstract fullName(): string,
}

// interface
interface User {
  firstName: string,
  lastName: string,
  sayHi(name: string): string,
  fullName(): string,
}

interface Human { // 인터페이스를 추가
  health: number,
}

class Player implemnets User {
  constructor(
    public firstName: string,
    public lastName: string,
    public health: number, // 이 부분을 추가 작성
  ){}
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
  sayHi(name: string) {
    return `Hello ${name}. My name is ${this.fullName()}`;
  }
}
```

위의 코드에서 <span class="crimson">인터페이스는 타입스크립트에서만 존재하는 키워드</span> 이므로 <u>자바스크립트는 User 인터페이스를 추적할 수가 없다</u>. 이렇게 interface 를 사용하면 <u>파일 사이즈를 줄일 수 있게</u> 된다. 추상 클래스(abstract class)를 사용하면 자바스크립트에서는 일반적인 클래스로 바뀌는데 이는 추상 클래스로 특정 모양을 따르도록 하기 위한 용도로 사용한다면 같은 역할을 하지만 자바스크립트로 변환되지 않는 인터페이스를 사용하는 것이 더 좋다는 것이다.

인터페이스를 상속하는 것의 문제점 중 하나는 private 프로퍼티를 사용하지 못한다는 것과 인터페이스를 사용하면 constructor 가 없기 때문에 User 를 상속받으면서 constructor 를 생성해야 한다.

또한 위의 코드와 같이 interface 를 추가로 작성할 수도 있다.

```ts
type PlayerA = {
  name: string,
};

const playerA: PlayerA = {
  name: "gunhee",
};

// 인터페이스
interface PlayerB {
  name: string,
};

const playerB: playerB = {
  name: "gunhee",
};
```

위의 코드를 살펴보면 playerA 와 playerB 를 보면 어떤 것이 인터페이스인지 타입인지 구별할 수 없다. 그 이유는 타입과 인터페이스 모두 객체의 모양과 타입을 알려주는 것이 목표이기 때문이다.

그러나 타입과 인터페이스는 할 수 있는 것이 서로 다르다. <u>type 은 새 프로퍼티를 추가하기 위해 다시 선언될 수 없지만</u>, <span class="mediumblue">인터페이스는 항상 상속이 가능</span>하다는 것이다. 타입스크립트에서는 오브젝트의 모양을 알려주기 위해서는 인터페이스를 사용하고 나머지 상황에서는 타입을 사용한다.

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
|거니 | 100점 | 100점
|철수 | 100점 | 100점
```

|      |  국어 | 영어  |
| :--- | ----: | :---: |
| 거니 | 100점 | 100점 |
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
