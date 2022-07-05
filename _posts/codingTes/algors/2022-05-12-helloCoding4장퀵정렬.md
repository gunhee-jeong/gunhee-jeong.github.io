---
layout: single
title: "Hello Coding-> 4장 퀵 정렬"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-23T20:50:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 4장 퀵 정렬
## 1. 분할 정복
분할 정복 전략은 문제를 푸는 새로운 방식을 제시한다.  

아래의 토지를 정사각형으로 나누고자 한다.  
<img src="https://user-images.githubusercontent.com/87808288/177139817-0faf82e7-c480-40c9-af75-dc875a5af7ad.png" width="400">  
<u>정사각형으로 나누면서 그중 가장 큰 정사각형을 구하려고</u> 한다면 분할 정복을 사용해볼 수 있다.  

우선 쉽게 생각해보면, 가로가 50m 세로가 25m라고 가정해보자.  
그러면 가장 큰 정사각형을 만들 수 있는 것은 25 * 25이다.  

`분할 정복`으로 생각해보면 <span style="color:blue">재귀 함수를 호출할 때마다 문제를 작게 나누어야</span> 한다.  
우선 조건에 맞는 <span style="color:tomato">가장 큰 상자를 알아내는 것부터</span> 시작이다.  
<img src="https://user-images.githubusercontent.com/87808288/177140747-9bba975f-de74-4b05-9fcb-d3f9766a26cc.png" width="400">  
한 변의 길이가 640m인 두 개의 정사각형 토지는 만들 수 있지만, 토지가 남게 된다.  
원래는 <u>1680 * 640m 크기를 가진 토지를 나누는 것으로 시작</u>했지만  
이제는 <span style="color:red">640 * 400의 토지를 나누는 문제를 푸는 것</span>이다.  
<u>남은 토지 크기에 맞는 정사각형을 찾는다면</u> <span style="color:blue">이 정사각형으로 전체 농장을 나눌 수 있게</span> 된다.  
이렇게 1680 * 640에서 <span style="color:royalblue">640 * 400으로 그 대상이 바뀌었다</span>.  

다시 위와 같은 알고리즘으로,  
<u>640 * 400의 크기를 가진 토지</u>로 시작하여 <span style="color:blue">가장 큰 정사각형의 크기는 400 * 400</span>이다.  
남은 부분은 400 * 240이다.  
<img src="https://user-images.githubusercontent.com/87808288/177141773-6aa3b105-60da-402a-a881-fc5a3c07b773.png" width="250">  
그리고 같은 방법으로 진행하면 240 * 160이고  
<img src="https://user-images.githubusercontent.com/87808288/177142371-f1c523f7-1113-489a-b3d5-512422c81562.png" width="400">  

이제 토지를 나눌 수 있는 가장 큰 정사각형이 80 * 80m 라는 사실을 알게 되었다.  
<img src="https://user-images.githubusercontent.com/87808288/177142728-b65d6a54-5a7a-46be-a414-2cf7f8e77178.png" width="300">  



## 2. 퀵 정렬
```js
function quickSort (array) {
  if (array.length < 2) {
    return array;
  }
   
  const pivot = [array[0]];
  const left = [];
  const right = [];
  
  for (let i = 1; i < array.length; i++) {
    if (array[i] < pivot) {
      left.push(array[i]);
    } else if (array[i] > pivot) {
      right.push(array[i]);
    } else {
      pivot.push(array[i]);
    }
  }
  console.log(`left: ${left}, pivot: ${pivot}, right: ${right}`);
  return quickSort(left).concat(pivot, quickSort(right));
}

const sorted = quickSort([5, 3, 7, 1, 9]);
console.log(sorted);
```

<img src="https://user-images.githubusercontent.com/87808288/169823347-8612951b-23d6-4781-b942-3060682a25eb.png" width="400">  



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
