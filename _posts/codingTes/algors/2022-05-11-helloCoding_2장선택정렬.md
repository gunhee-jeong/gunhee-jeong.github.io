---
layout: single
title: "Hello Coding-> 2장 선택 정렬"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-05-11T06:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 2장 선택 정렬
## 1. 메모리가 동작하는 방법
메모리에 무언가를 저장하려할 때, 컴퓨터에게 그 공간을 요청하게 된다.  
그러면 컴퓨터는 무언가를 저장할 수 있는 주소를 알려준다.  
<img src="https://user-images.githubusercontent.com/87808288/176622624-26b4fdaf-704b-422c-9357-df80cbc452d9.png" width="500">  

## 2. 배열과 연결 리스트
할 일 목록을 관리하는 앱을 만든다고 한다면  
이때는 배열을 사용해야할까 아니면 연결 리스트를 사용해야할까?  

일단 `배열`로 할 일 목록을 나타내보면  
배열을 사용하면 <span style="color:blue">할 일들을 메모리에 차례대로 붙여서 저장</span>한다.  
이제 <u>네 번째 할 일을 추가하려고</u> 한다.  
<span style="color:tomato">그런데 벌써 다음 서랍을 누군가가 사용하고</span> 있다.  
<img src="https://user-images.githubusercontent.com/87808288/176623201-497305b6-e07e-4476-85ce-0743db462172.png" width="500">  

위의 상황은 마치 극장에 가서 자리에 앉는 것과 비슷하다.  
극장에서 우연히 친구를 만났다고해서, 나의 옆자리에 사람이 있는 데  
친구를 옆에 앉힐 수는 없는 것이다.  
이런 경우에는 <u>컴퓨터에게 4개의 자리가 있는 다른 메모리 공간을 요청</u>해야한다.  
그리고 <span style="color:blue">4개의 할 일을 모두 그 자리로 옮겨야</span> 한다.  

그런데 <u>만약 또 다른 친구가 온다면</u> -> <span style="color:blue">다시 자리가 모자라</span>기 때문에 또 <span style="color:red">전원이 자리를 같이 옮겨야</span> 한다.  
마찬가지로 <span style="color:royalblue">배열에 새 원소를 추가하는 것은 쉽지 않은 일</span>이다.  

### (1) 연결 리스트
`연결 리스트`를 사용하면 <span style="color:tomato">원소를 메모리 어느 곳에나 둘 수</span> 있다.  
<img src="https://user-images.githubusercontent.com/87808288/176624899-e3d92f41-f723-4285-85d4-d58836534e47.png" width="500">  
<u>각 원소에는</u> 목록의 <span style="color:tomato">다음 원소에 대한 주소가 저장</span>되어 있다.  
그로인해 <u>여러 가지 메모리 주소들</u>이 <span style="color:blue">하나의 목록으로 연결될 수</span> 있는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/176625570-d3909eed-c884-4cab-b8f6-d211501c3d53.png" width="600">  
첫 번째 주소로 가면 그곳에 -> 다음 주소는 123!, 그래서 123이라는 주소로 가면 -> 다음 주소는 847!  
이렇게 연결 리스트를 사용하면 <span style="color:tomato">원소를 옮길 일이 없어진다</span>.  

### (2) 배열
인기 순위 10개를 보여주는 웹 사이트가 있는데,  
이곳에서는 한 페이지에 10개를 모두 보여주는 것이 아니라  
"다음" 버튼을 눌러서 하나씩 확인하게 할 수도 있다.  
<img src="https://user-images.githubusercontent.com/87808288/176626376-0e0d064f-7420-4113-8f32-8e03d3f00203.png" width="300">  
1번 악당을 보는 것이 아니라, 가장 마지막의 악당을 보고 싶다면 마지막에 나오는 악당까지  
차례대로 "다음" 버튼을 눌러야 한다.  

`연결 리스트`에서 위와 같은 문제가 발생한다.  
연결 리스트에서 <span style="color:tomato">마지막 원소를 보고 싶다면 바로 읽을 수가 없다</span>.  
왜냐하면 <span style="color:red">주소를 알지 못하기 때문</span>이다.  

반면 `배열`에서는 <span style="color:blue">모든 원소의 주소를 알고 있다</span>.  
배열은 배열 안의 <span style="color:tomato">어떤 원소든 바로 이동할 수</span> 있다.  
<img src="https://user-images.githubusercontent.com/87808288/176627350-0ff7c3ac-04b3-47f6-b8a0-2305adbf97e6.png" width="500">  

### (3) 리스트의 가운데에 삽입하기
<u>원소를 배열이나 리스트의 중앙에 삽입</u>한다면,  
<span style="color:blue">리스트는 이전 원소가 무엇을 가리키는지 바꾸기만 하면</span> 되므로 <span style="color:tomato">리스트에 삽입하는 것이 훨씬 쉽다</span>.  
<img src="https://user-images.githubusercontent.com/87808288/176989120-3ed9ac00-7572-4ec8-bae5-9303be6c656e.png" width="700">  
하지만 배열에서는 다음에 오는 모든 원소의 위치를 바꾸어야 한다.  
<img src="https://user-images.githubusercontent.com/87808288/176989175-9d7300e5-d576-4304-9854-a1cbad00ebb1.png" width="400">  
<u>만약 공간이 부족하면</u> <span style="color:tomato">모든 원소를 새로운 장소로 복사해야</span> 한다.  
그래서 중간에 원소를 삽입하려면 <span style="color:red">리스트가 훨씬 좋은 선택</span> 방법이다.  

### (4) 삭제하기
이 경우에도 <span style="color:tomato">이전 원소가 가리키는 위치만 바꾸면</span> 되기 때문에 <span style="color:red">리스트가 더 좋은</span> 선택이다.  
아래는 배열과 연결 리스트의 연산에 대한 실행 시간표이다.  
<img src="https://user-images.githubusercontent.com/87808288/176989332-6f85dbca-b16e-4244-be42-578db9d0e7d3.png" width="350">  

자료에 접근하는 방식에는 `임의 접근`과 `순차 접근`이 있다.  
<span style="color:red">순차 접근</span>은 <u>원소를 첫 번째부터 하나씩</u> 읽는 것을 뜻한다.  
<span style="color:tomato">연결 리스트</span>는 순차 접근밖에 할 수 없다.  
연결 리스트에 있는 10번 째 원소를 읽으려면 그 앞의 9개의 원소를 모두 읽어서 10번 째 원소로 가는 길을 찾아야 한다.  

## 3. 선택 정렬
<img src="https://user-images.githubusercontent.com/87808288/176989490-02ba148b-3518-4de2-8cf7-ab4d1e47e911.png" width="400">  
위의 그림에서 가장 많이 들은 음악 목록과 가장 적게 들은 것 순서로 정렬하고자 한다.  

한 가지 방법은 <span style="color:blue">리스트의 모든 항목을 살펴보고</span> 가장 많이 연주된 가수를 찾아 <u>새로운 리스트에 기록하는</u> 것이다.  
<u>모든 원소를 한 번씩 건드린다</u>는 것은 <span style="color:tomato">O(n)</span>의 시간이 걸린다는 것이다.  
연주 횟수가 가장 많은 가수를 찾기 위해서는 <span style="color:blue">목록의 모든 항목을 점검해야</span> 한다.  
그렇게 <u>O(n) 실행 시간이 걸리는 연산을 n번 해야</u>한다.  
모두 합해서 O(n * n), 즉 <span style="color:red">O(n<sup>2</sup>)</span> 시간이 걸린다.  
<img src="https://user-images.githubusercontent.com/87808288/176989756-8610249a-0970-47c3-a418-16b9067a06a8.png" width="550">  

```js
let arr = [5, 3, 6, 2, 10];
let length = arr.length;
let smallest = arr[0];
let numIndex = 0;

function findSmallest(arr) {
  smallest = arr[0];
  numIndex = 0;
  
  for (let i = 0; i < arr.length; i++) {
    if (smallest > arr[i]) {
      smallest = arr[i]
      numIndex = i;
    }
  }
  return smallest;
}

function selectionSort(arr) {
  let newArr = [];
  
  for (let i = 0; i < length; i++) {
    findSmallest(arr);
    newArr.push(smallest);
    arr.splice(numIndex, 1);
  }
  return newArr;
}

selectionSort(arr);
```

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
