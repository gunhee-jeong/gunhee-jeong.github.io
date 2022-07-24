---
layout: single
title: "Hello Coding-> 6장 너비 우선 탐색"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [Hello Coding] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-06-16T11:40:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 6장 너비 우선 탐색
## 1. 시작하기에 앞서
너비 우선 탐색을 사용하면 두 항목 간의 최단 경로를 찾을 수 있다.  
- 체커 게임에서 가장 적은 수로 승리할 수 있는 방법을 계산하는 인공지능
- 맞춤법 검사기
- 가장 가까운 의사 찾기 등  

## 2. 그래프의 소개
<img src="https://user-images.githubusercontent.com/87808288/179681987-f9a0e025-18d0-40f2-8170-4595ee60856a.png" width="500">  
트윈 픽스에서 금문교까지 가고자 할 때, 버스로 가지만 최대한 적게 갈아타고자 한다면?  

### (1) 그래프란 무엇인가?
친구들과 포커를 치고 있다.  
누가 누구에게 돈을 빚지고 있는지 모형화한다면 아래의 그림과 같이 표현할 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/179682840-87d44464-1c59-4284-aba1-593021e381ef.png" width="350">  

알렉스는 라마에게 빚을 지고, 톰은 아디트에게 빚을 지고 있다.  
그래프는 `정점(node)`과 `간선(edge)`으로 이루어진다.  
<img src="https://user-images.githubusercontent.com/87808288/179683096-9cdfa72a-74cb-4fa2-91ea-51735846d004.png" width="300">  

## 3. 너비 우선 탐색
우리가 망고 농장의 주인이라고 생각해보자.  
우리의 망고를 팔아줄 판매상을 찾고 있는데,  
페이스북 친구 중에 망고 판매상이 있는지 확인하고자 한다.  
우선 찾아볼 친구 목록을 만든다.  
그리고 이 목록에서 각각의 사람이 망고 판매상인지 확인하면 된다.  
<img src="https://user-images.githubusercontent.com/87808288/179683703-b6c12620-48fe-4264-aeb4-1882db78b0cb.png" width="400">  

결과적으로 우리의 친구 중에 망고 판매상이 존재하지 않았다.  
이제는 친구의 친구를 살펴볼 차례이다.  
<img src="https://user-images.githubusercontent.com/87808288/179683998-ee7dc404-eb76-48df-87d7-dbf1a4a450d7.png" width="400">  
만약 앨리스가 망고 판매상이 아니면 앨리스의 친구도 목록에 올려야 한다.  
그러면 결과적으로 그녀의 친구, 그녀 친구의 친구, 이런 식으로 망고 판매상에 도달할 때까지 전체 네트워크를 탐색하게 된다.  
이러한 알고리즘이 바로 너비 우선 탐색이다.  

### (1) 최단 경로 찾기
너비 우선 탐색은 두 가지 질문에 답할 수 있다.  
- 정점 A에서 정점 B로 가는 경로가 존재하는가?(우리의 네트워크에 망고 판매상이 있는가?)
- 정점 A에서 정점 B로 가는 최단 경로는 무엇인가?(누가 가장 가까운 망고 판매상인가?)  

<img src="https://user-images.githubusercontent.com/87808288/179684953-96462517-d4dc-4569-8805-ca4ed2f6075f.png" width="400">  
1촌 관계에서 망고 판매상이 없을 경우 2촌 관계를 탐색하게 된다.  
너비 우선 탐색이 진행될수록 탐색 범위는 출발점에서 멀어진다.  

다른 방법은 탐색 목록에 2촌 관계를 추가하기 전에 1촌 관계부터 모두 추가하는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/179685481-c22ee9a9-d7e3-420f-92e7-7af549f29a58.png" width="180">  
목록의 위에서부터 차례대로 망고 판매상이 있는지 확인한다면,  
1촌 관계에 있는 망고 판매상을 2촌 관계에 있는 망고 판매상보다 먼저 찾을 수 있다.  
너비 우선 탐색은 단순히 A에서 B로 가는 경로를 찾는 것이 아니라 최단 경로를 찾을 수 있다.  

### (2) 큐
<img src="https://user-images.githubusercontent.com/87808288/179686352-df9307c8-37f9-4e46-9d38-b03f0098c0a7.png" width="300">  
친구와 버스 정류장에서 줄을 서고 있다고 가정해보자.  
우리들이 친구 앞에 서있다면 버스를 먼저 탑승하게 될 것이다.  
`큐`도 마찬가지이다.  
<u>큐 안의 원소에 임의로 접근할 수 없다</u>는 점에서 스택과 비슷하다.  
큐에는 삽입과 제거라고 하는 두 가지 연산이 있다.  

<u>목록에 두 개의 항목을 삽입하면</u> 두 번째로 삽입된 항목보다 <span style="color:royalblue">첫 번째로 삽입된 항목이 먼저 제거</span>된다.  
큐를 사용하면 목록에 먼저 추가된 사람들을 먼저 꺼내서 탐색하게 된다.  
따라서 큐를 <span style="color:blue">선입 선출 자료구조</span>라고도 부른다.  

## 4. 그래프의 구현
<img src="https://user-images.githubusercontent.com/87808288/179696356-35a2d637-169d-429b-bd22-75c9966c1071.png" width="250">  
우선 코드로 그래프를 구현해야 한다.  
그래프는 몇 개의 정점으로 이루어진다.  
그리고 각각의 정점은 이웃하는 정점과 연결된다.  
"여러분" -> "밥"과 같은 관계를 어떻게 코드로 표현할 수 있을까?  
바로 해시 테이블을 이용할 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/179696995-a48f39fc-a867-4e2d-bba1-14e2b3c8300a.png" width="200">  

<img src="https://user-images.githubusercontent.com/87808288/179697343-307c1769-ec4c-4613-8aaf-3804907ae443.png" width="400">  
위의 그래프를 코드로 구현하면  

```js
const graph = {
  you: ["alice", "bob", "claire"],
  bob: ["anuj", "peggy"],
  alice: ["peggy"],
  claire: ["thom", "jonny"],
  anuj: [],
  thom: [],
  jonny: []
};
```

해시 테이블은 순서를 가지지 않기 때문에 키/ 값 쌍을 어떤 순서로 추가하든 상관없다.  

## 5. 알고리즘의 구현
<img src="https://user-images.githubusercontent.com/87808288/179698923-68976cf1-b6e1-441c-8ea3-1a736a9ca077.png" width="500">  

```js
const list = {
  you: ["alice", "bob", "claire"],
  bob: ["anuj", "peggy"],
  alice: ["peggy"],
  claire: ["thom", "jonny"],
  anuj: [],
  thom: [],
  jonny: []
};

let queue = [...list.you];

function searchM(x) {
  if (x[x.length - 1] === 'm') return true;
  else return false;
}

while (queue.length) {
  if (searchM(queue[0])) {
    console.log(`${queue[0]} is a mango seller!`);
    break;
  } else {
    if (list[queue[0]] !== undefined) {
      queue.push(...list[queue[0]]);
      queue = queue.filter(ele => queue[0] !== ele);
      queue = [...new Set(queue)];
    } else queue = queue.filter(ele => queue[0] !== ele);
  }
}
```

<!-- <span style="color:white;background:royalblue;"> -->

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
