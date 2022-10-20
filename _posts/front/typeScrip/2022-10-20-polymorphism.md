---
layout: single
title: "Polymorphism"
# categories: Git
categories:
  - TypeScript # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [노마드코더, 다형성] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-10-20T22:00:00+09:00
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

# polymorphism
```jsx
type SuperPrint = {
  (arr: number[]): void,
  (arr: boolean[]): void,
  (arr: boolean[]): string,
};

const superPrint: SuperPrint = (arr) => {
  arr.forEach(i => console.log(i));
};

superPrint([1, 2, 3, 4]);
superPrint([true, false, true]);
```

위의 코드와 같이 superPrint 함수를 실행할 때 SuperPrint 라고 하는 call signatures 를 만들어주었고 이를 이용해서 superPrint 함수를 호출할 수 있다. 하지만 superPrint 함수의 인자로 들어오는 배열에 string 등의 형식으로 배열이 구성된다면 call signatures 로 모든 상황을 다 적어주는 것은 옳은 방법이 아니다. 그래서 이때는 polymorphism 을 사용할 수 있다.

generic 이란, 타입의 placholder 와 같은 것이다. 아래의 코드와 같이 superPrint 함수의 인자로 전달되는 배열에 number 타입과 boolean 타입이 섞여있다. 그러면 이 부분은 제대로 동작하지 못한다. 왜냐하면 그 부분에 대한 call signature 가 없기 때문이다.

```jsx
type SuperPrint = {
  (arr: number[]): void,
  (arr: boolean[]): void,
  (arr: boolean[]): void,
};

const superPrint: SuperPrint = (arr) => {
  arr.forEach(i => console.log(i));
};

superPrint([1, 2, 3, 4]);
superPrint([true, false, true]);
superPrint([1, 2, true, false]); // 제대로 동작하지 못한다.
```

우리가 원하는 것은 superPrint 라는 함수가 어떤 타입의 데이터가 오더라도 superPrint 가 정상적으로 동작하는 것이다. 이것을 다시 해결하고 싶다면 아래와 같이 코드를 작성할 수 있다.

```jsx
type SuperPrint = {
  (arr: number[]): void,
  (arr: boolean[]): void,
  (arr: boolean[]): void,
  (arr: (number | boolean)[]): void, // 이 부분이 추가
};

const superPrint: SuperPrint = (arr) => {
  arr.forEach(i => console.log(i));
};

superPrint([1, 2, 3, 4]);
superPrint([true, false, true]);
superPrint([1, 2, true, false]); // 이제는 동작한다.
```

위의 방법으로 아까의 문제가 해결되었지만 이렇게 문제를 해결하는 방법은 좋지 않다. 왜냐하면 <span class="forestgreen">모든 가능성을 다 조합</span>해야하기 때문이다. 이 때문에 아까 위에서 언급했던 <span class="crimson">generic</span> 을 사용하여 이러한 문제들을 해결할 수 있다. generic 을 사용하면 타입스크립트가 그 타입을 유추할 수 있게 된다. 우리가 call signature 를 작성할 때, <span class="mediumblue">여기에 들어올 확실한 타입을 모를 때</span> generic 을 사용하게 된다.

generic 을 사용하는 방법은, 우선 타입스크립트에게 generic 을 사용하고 싶다고 알려야 한다.

```jsx
type SuperPrint = {
  <TypePlaceholder>(arr: TypePlaceholder[]): void,
};

const superPrint: SuperPrint = (arr) => {
  arr.forEach(i => console.log(i));
};

superPrint([1, 2, 3, 4]);
superPrint([true, false, true]);
superPrint([1, 2, true, false]);
```

위의 코드에서 "&lt;TypePlaceholder&gt;(arr: TypePlaceholder[]): void," 이 부분이 바로 타입스크립트에게 call signature 가 제네릭을 받는다는 걸 알려주는 방법이다. `제네릭`은 기본적으로 <u>placeholder 를 사용해서</u> 내가 <span class="mediumblue">작성한 코드의 타입 기준으로 타입을 바꿔준다</span>. 즉 <span class="crimson">타입스크립트가 코드를 보고 타입을 추론</span>하게 되는 것이다.

이제 superPrint 함수를, 반환 값으로 배열 안의 요소를 리턴하는 함수로 바꾸기 위해 아래의 코드를 살펴보자.

```jsx
type SuperPrint = {
  <TypePlaceholder>(arr: TypePlaceholder[]): TypePlaceholder,
};

const superPrint: SuperPrint = (arr) => arr[0];

const a = superPrint([1, 2, 3, 4]);
const b = superPrint([true, false, true]);
const c = superPrint(['a', 'b', 'c']);
const d = superPrint([1, 2, true, false, "hello"]);
```

위의 코드를 살펴보면 call signature 로 TypePlaceholder 중 하나를 리턴받로록 설정했다. 이렇게 변수 a 의 타입은 number, b 의 타입은 boolean, c 의 타입은 string, d 의 타입은 number, boolean, string 이 되었다. 그리고 이것이 바로 polymorphism(다형성) 이다. superPrint 함수는 다양한 형태의 call signatures 를 가지고 있다.

```ts
type SuperPrint = <T>(a: T[]) => T;

const superPrint: SuperPrint = (arr) => arr[0];

const a = superPrint([1, 2, 3, 4]);
const b = superPrint([true, false, true]);
const c = superPrint(['a', 'b', 'c']);
const d = superPrint([1, 2, true, false, "hello"]);
```

위의 코드를 살펴보면 SuperPrint 를 선언할 때 T 는 배열에서 오고, 함수의 첫 번째 파라미터에서 오는 거라고 타입스크립트에게 알려주는 것이다. 타입스크립트는 이것을 기반으로 해당 부분의 코드를 살펴봐야 한다는 것을 알게 된다. 그렇게 <u>타입스크립트는 placeholder 를 통해</u>서 <span class="forestgreen">superPrint 함수를 호출할 때마다</span> 각각의 <span class="meidumblue">코드에 맞는 call signature 를 생성</span>해준다.

그러면 여기서 제네릭과 any 는 그럼 어떤 차이점이 있는지 궁금해질 것이다. any 를 사용하면 더이상 개발자를 지켜주지 않게 된다. 아래의 코드를 한 번 살펴보자.

```ts
type SuperPrint = (a: any[]) => any;

const superPrint: SuperPrint = (arr) => arr[0];

const a = superPrint([1, 2, 3, 4]);
const b = superPrint([true, false, true]);
const c = superPrint(['a', 'b', 'c']);
const d = superPrint([1, 2, true, false, "hello"]);

d.toUpperCase(); // 에러가 발생하지 않는다.
```

변수 d 에는 numer 1 이 담긴다. 1 에는 toUpperCase() 를 사용할 수 없지만 any 를 사용했기 때문에 에러를 잡아내지 못하는 것이다. 이때 any 가 아닌 제네릭을 사용하게 되면 코드를 실행하기도 전에 에러를 잡아낸다. 이렇게 타입스크립트의 보호를 받게 되는 것이다. 제네릭은 내가 요구한대로 signature 를 생성해주는 도구인 것이다.

이제 SueperPrint 타입 제네릭을 하나 더 추가해보자.

```ts
type SuperPrint = <T, M>(a: T[], b: M) => T;

const superPrint: SuperPrint = (arr) => arr[0];

const a = superPrint([1, 2, 3, 4], 'x');
const b = superPrint([true, false, true], 1);
const c = superPrint(['a', 'b', 'c'], false);
const d = superPrint([1, 2, true, false, "hello"], []);
```

위의 코드를 살펴보면 placeholder 에 M 이 추가되었다. 그리고 두 번째 인자가 제네릭이 되었다는 것을 알 수 있다. 타입스크립트는 <u>제네릭을 처음 인식했을 때</u>와 <u>제네릭의 순서</u>를 기반으로 제네릭의 타입을 알게 된다. 다시 한 번 말하지만 any 와는 명확히 다르다. 제네릭을 사용하면 타입스크립트가 우리의 요청에 따라 call signature 를 생성하기 때문이다.

```ts
function superPrint<T>(a: T[]) {
  return a[0];
}

const a = superPrint([1, 2, 3, 4]);
const b = superPrint([true, false, true]);
const c = superPrint(['a', 'b', 'c']);
const d = superPrint([1, 2, true, false, "hello"]);
```

위의 코드는 이전의 type SuperPrint 를 직접 만들었을 때와 같은 결과를 보여준다. SuperPrint 를 만들지 않고도 위의 코드와 같은 방법으로 제네릭을 사용할 수 있다.

```ts
type Player<E> = {
  name: string,
  extraInfo: E,
};

const gunhee: Player<{favFood: string}> = {
  name: "gunhee",
  extraInfo: {
    favFood: "kimchi",
  }
};
```

위의 코드는 아래의 코드와 같다.

```ts
type Player<E> = {
  name: string,
  extraInfo: E,
};

type GunheePlayer = Player<{favFood: string}>;

const gunhee: GunheePlayer = {
  name: "gunhee",
  extraInfo: {
    favFood: "kimchi",
  }
};
```

그리고 아래의 코드도 위으 코드들과 정확히 같은 코드이다.

```ts
type Player<E> = {
  name: string,
  extraInfo: E,
};

type GunheeExtra = {
  favFood: string,
};

type GunheePlayer = Player<GunheeExtra>;

const gunhee: GunheePlayer = {
  name: "gunhee",
  extraInfo: {
    favFood: "kimchi",
  }
};

const gildong: Player<null> = {
  name: "gildong",
  extraInfo: null,
};
```

```ts
function printAllNumbers(arr: Array<number>) {
  // 
}
```

위의 코드는 "number[]" 를 다르게 쓸 수 있는 방법이다.

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
