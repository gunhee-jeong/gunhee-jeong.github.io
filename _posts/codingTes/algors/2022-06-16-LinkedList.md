---
layout: single
title: "링크드 리스트(Linked List)"
# categories: Git
categories:
  - Algorithm # HTML CSS JavaScript Server Algorithm wecodes Programmers1 Programmers2 CS Github Blog
tag: [자료구조] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-06-16T12:40:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 배열과 리스트
이 두가지의 개념은 용어가 혼용되어 사용되기도 한다.  
하지만 차이가 발생한다.  

`배열`은 <u>메모리 상에서 연속적인 공간</u>을 할당받아 데이터를 저장하게 된다.  
배열은 원소에 접근할 때면 <span style="color:red">index</span>라는 개념을 사용하는데 -> 이는 <span style="color:tomato">원소의 데이터 주소를 가리키는 유일한 식별자</span>이다.  
이 인덱스로 인해 배열은 아주 빠르게 <span style="color:blue">내가 원하는 특정 원소에 접근할 수 있다는 장점</span>을 가진다.  
하지만 이로 인하여 중간에 <span style="color:tomato">원소를 삽입하거나 삭제할 때 느리다는 단점이 발생</span>한다.  
왜냐하면 삽입이나 삭제시 뒤에 존재하는 원소들의 모든 위치를 변경하는 작업이 필요하기 때문이다.  

`리스트`는 각 원소의 메모리 상 <u>연속적인 공간에 할당되지 않을 수 있다</u>.  
이 말은 즉, 첫 번째 원소의 주소를 알더라도 그 다음 원소의 주소를 단순히 계산할 수 없다는 의미를 가진다.  
리스트의 원소는 다음 원소를 가리키는 <span style="color:red">포인터</span>(pointer) 등을 사용하여 <u>각 원소의 순서를 구현</u>한다.  
이러한 이유들로 <span style="color:tomato">배열보다 데이터의 삽입이나 삭제가 빠른 편</span>이다. <span style="color:blue">앞 뒤 원소의 포인터만 변경하면 되기 때문</span>이다.  
하지만 <span style="color:blue">인덱스를 사용하여 특정 원소에 직접적인 접근이 불가</span>하므로 <span style="color:red">특정 원소를 찾기 위해서는</span>  
<span style="color:red">첫 번째 원소부터 선형 검색을 실시해야 한다는 단점</span>이 발생한다.  

# Linked List
<img src="https://user-images.githubusercontent.com/87808288/173994154-73c84783-55c0-4ea2-bf95-c14c4ad3a1c1.png" width="600">  
`링크드 리스트`는 <span style="color:blue">길이가 정해져 있지 않은 데이터의 연결된 집합</span>이라 할 수 있다.  
링크드 리스트에서 <u>노드</u>는 <span style="color:royalblue">데이터를 갖고 있는 데이터의 묶음</span>인데,  
위의 그림에서 처럼 노드 속에는 다음 노드를 가리키고 있는 것을 확인할 수 있다.  

링크드 리스트의 가장 큰 특징은 <span style="color:tomato">길이가 가변적</span>이라는 것이다.  
이로써 배열의 단점을 링크드리스트가 대체할 수 있게 된 것이다.  
`링크드 리스트`는 <u>다음 노드만 추가하면</u> 되므로 -> <span style="color:royalblue">많은 비용이 들지 않는다</span>.  

하지만 <u>어떠한 데이터를 찾는 경우</u> <span style="color:red">링크드 리스트의 전부를 탐색해야할 수도</span> 있다.  
그러므로 데이터가 자주 추가되며 가변적으로 변하게 될 상황에서는 링크드 리스크를,  
주로 데이터의 변경이나 탐색을 위한 것이라면 배열을 사용하는 것이다.  




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
