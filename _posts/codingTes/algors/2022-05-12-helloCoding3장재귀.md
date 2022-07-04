---
layout: single
title: "Hello Coding-> 3장 재귀"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-12T12:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 3장 재귀
## 1. 시작하기에 앞서
## 2. 재귀
재귀란 함수가 자기 자신을 호출하는 것을 말한다.  

재귀는 풀이를 더 명확하게 만들어 준다.  
재귀를 사용한다고 성능이 더 나아지는 것은 아니다.  

## 3. 기본 단계와 재귀 단계
`재귀 함수`를 사용함에 있어서 <u>언제 재귀를 멈출지 알려줘야</u> 한다.  
그래서 재귀 함수는 <span style="color:royalblue">기본 단계</span>와 <span style="color:royalblue">재귀 단계</span>라는 두 부분으로 나누어져 있다.  
재귀 단계는 함수가 자기 자신을 호출하는 부분이다.  
기본 단계는 함수가 자기 자신을 다시 호출하지 않는 경우, 즉 무한 반복으로 빠져들지 않게 하는 부분이다.  

## 4. 스택
호출 스택은 프로그램에서 중요한 개념이다.  
호출 스택은 일반적인 프로그래밍에서도 중요하지만 재귀를 사용할 때 더욱 중요하다.  

<img src="https://user-images.githubusercontent.com/87808288/177124411-65b35f48-5751-445e-9ea6-2da0a4a66acf.png" width="400">  

<img src="https://user-images.githubusercontent.com/87808288/177124669-07ba0406-60dc-417d-87ec-01dcc73005c2.png" width="500">  
위 그림의 자료구조를 <span style="color:tomato">스택</span>이라고 한다.  

### (1) 호출 스택
```js
function greet(name) {
  console.log(`Hello! ${name}!`);
  greet2(name);
  console.log(`getting ready to say bye...`);
  bye();
}

function greet2 (name) {
	console.log(`How are you, ${name}?`);
}

function bye() {
  console.log(`Ok! bye`);
}

greet("gunhee")
```

위의 코드를 실행하면,  
`Hello! gunhee`가 프린트된 후 ->  
greet2("gunhee") 명령으로 gree2 함수를 호출한다.  
<img src="https://user-images.githubusercontent.com/87808288/177127835-0e254208-d526-4acd-aa7a-6100f64d7339.png" width="400">  

<u>greet2 함수는 greet 함수 위에 올라가</u> 있는 상태이고  
How are you, gunhee? 가 프린트된다.  
이제 <span style="color:royalblue">greet2 함수는 pop 연산으로 사라지고</span>, 다시 가장 위에 있는 함수는 greet이 되었다.  
그리고 사실 <span style="color:blue">아직 greet 함수는 완료되지 않은 상태</span>이다.  
이제는 getting ready to say bye... 를 호출하고 <u>bye 함수를 호출</u>한다.  
<img src="https://user-images.githubusercontent.com/87808288/177128443-e2c9d695-0727-446a-b632-e993ceabc3c8.png" width="300">  

이제 Ok! bye를 호출하고 bye 함수는 pop되며, greet 함수로 돌아오게 된다.  
이런 방식으로 <u>여러 개의 함수를 호출하면서 함수에 사용되는 변수를 저장하는 스택</u>을 <span style="color:tomato">호출 스택</span>이라고 한다.  

### (2) 재귀 함수에서 호출 스택 사용
<span style="color:blue">factorial(5)</span>는 `5!`라는 뜻이고, 5!는 <u>5 * 4 * 3 * 2 * 1</u>로 정의된다.  

```js
function fact(x) {
  if (x === 1) return 1;
  else return x * fact(x - 1); // 1 * 2 * 3 의 순서로 계산된다.
}

fact(3);
```

<img src="https://user-images.githubusercontent.com/87808288/177137418-66037937-4d46-4164-b564-42a2182757fb.png" width="600">  
<img src="https://user-images.githubusercontent.com/87808288/177137470-83174138-8011-4466-a80b-0fc18b3a2f63.png" width="600">  

위의 내용에서 중요한 것은 <span style="color:tomato">fact 함수에 대한 각각의 호출이 자기만의 x값의 사본을 가지고 있다는 것</span>이다.  
<span style="color:red">서로 다른 함수 호출에 대한 x값에 접근할 수 없다</span>.  

이 방식을 사용하면 확인해야 할 상자의 더미를 만들고 어떤 상자를 더 확인해야 하는지 항상 알 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/177138793-f928a5bf-e376-4cff-89ed-2b2b29bfba26.png" width="400">  
<img src="https://user-images.githubusercontent.com/87808288/177138981-f1a43e32-fc86-4b19-9d68-622f6b14edda.png" width="400">  

`스택`을 사용하면 확인해야 할 <u>상자 더미를 일일이 추적하지 않아도 된다</u>.  
<span style="color:blue">스택이 일련의 동작을 알아서 실행하게</span> 된다.  

<!-- <span style="color:royalblue"> -->

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
