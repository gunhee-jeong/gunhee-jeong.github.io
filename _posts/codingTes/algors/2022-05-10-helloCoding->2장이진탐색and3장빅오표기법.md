---
layout: single
title: "Hello Coding-> 2장 이진 탐색, 3장 빅오 표기법"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-10T06:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 2장 이진 탐색
이진 탐색은 알고리즘이다.  
이진 탐색이 어떻게 동작하는지 예를 들어보자면, 1과 100 사이의 숫자를 하나 생각한다.  
이제 가능한 한 가장 적은 횟수의 추측으로 이 숫자를 알아내야 한다고 가정하자.  
한 번 추측할 때마다 그 숫자가 너무 작은지, 너무 큰지, 맞는 숫자인지 알 수 있다.  

## 더 좋은 탐색 방법
100의 중간, 즉 50부터 시작하는 것이다.  
"50이 너무 작다"는 대답 하나로 숫자의 절반이 답이 아니라는 것을 알 수 있게 된다.  
1부터 50까지의 숫자는 너무 작다고 하니 -> 이번에는 남은 51과 100까지의 숫자 중 중간에 속하는 75로 추측하자.  
"75가 너무 크다"는 대답으로 75보다 같거나 큰 숫자들은 제외할 수 있게 되었다.  

이진 탐색에서는 매번 남은 숫자 중의 가운데 숫자를 말하고 대답에 따라 그보다 큰 숫자 작은 숫자들을  
한꺼번에 없앨 수 있다.  

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const item = 10;

let low = 0;
let high = arr.length - 1; //탐색의 끝점 -> 9
let mid = 0;
let guess = 0;

while(true) {
  mid = parseInt((low + high) / 2); //parseInt(4.5) -> 4
  guess = arr[mid]; //2
  console.log(`mid-> ${mid}`); //'mid-> 4' 'mid-> 7' 'mid-> 8' 'mid-> 9'
	console.log(guess); //5 8 9 10
  if(guess === item) break;
  else if(guess > item) high = mid;
  else if(guess < item) low = mid + 1;
}

```

## 실행시간
위의 상황에서 <u>1번부터 차례로 1 2 3 4 5... 10</u> 이렇게 순차적으로 정답을 유추하는 방법으로  
걸리는 시간을 <span style="color:red">선형 시간</span>이라고 한다.  
배열안에 100개의 숫자가 담겨있다면 100번을 유추해야하고, 40억 개의 숫자가 담겨있다면 40억 번을 유추해야하는 것이다.  

하지만 <span style="color:red">이진 탐색</span>은 다르다.  
<u>100개의 숫자</u>가 담겨있다면 -> `7번`, <u>40억 개</u>라고 해도 -> <span style="color:blue">32번만 유추하면 정답을</span> 찾을 수 있는 것이다.  

# 3장 빅오 표기법

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
