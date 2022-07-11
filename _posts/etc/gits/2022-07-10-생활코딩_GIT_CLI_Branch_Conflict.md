---
layout: single
title: "생활코딩 -> GIT CLI - Branch & Conflict"
# categories: Git
categories:
  - Github # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [생활코딩, git] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-10T22:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1장 브랜치의 사용법
branch를 추가하고자 할 때는

```bash
git branch 브랜치이름
```

위의 명령어를 통해 branch를 생성할 수 있다.  

```bash
git checkout 브랜치이름
```

위의 명령어를 통해 다른 branch로 이동할 수 있다.  

```bash
git log --all --graph --oneline
```

위의 명령어를 통해서는 git log를 그래프를 사용해 한 눈에 알아볼 수 있도록 터미널에서 UI를 제공해준다.  

# 2장 브랜치 병합
현재 1번 이라는 공통된 내용을 가지고  
A라는 branch와 main branch가 있을 때 ->  
1번 내용을 기점으로 A branch와 main branch는 각각의 버전을 형성했다.  
이때 main branch로 A branch 내용들을 merge 하고자 한다면  

```bash
git checkout main
```

우선 위의 명령어처럼 최종적으로 merge할 branch로 이동하고(head -> main)  

```bash
git merge A
```

위의 과정을 거치면 main branch에 A branch 내용들이 merge 된다.  

# 3장 3 way merge

# 4장 reset VS checkout
`checkout` 이라는 것은 결국 <span style="color:blue">HEAD를 바꾸는 행동</span>이다.  
또한 checkout 은 branch를 가리키지 않고 -> commit을 직접적으로 가리칠 수도 있다.  
이를 detached 상태에 있다고 표현한다.  
<img src="https://user-images.githubusercontent.com/87808288/178180251-ab0f5d39-9107-495d-ae3f-32b2e414399a.png" width="400">  

checkout 과 reset의 차이점을 알아보면  
checkout은 HEAD를 제어하고  
"<span style="color:green">git checkout main</span>"을 명령어로 사용한다면 아래의 그림과 같이 `HEAD`는 <span style="color:tomato">main(master)</span>을 가리키게 된다.  
(main(master)은 2번 commit을 가리킨다.)  
<img src="https://user-images.githubusercontent.com/87808288/178180801-feeafd9d-03fa-4133-bbad-cbd97f586651.png" width="400">  

이제 우리는 google branch에 checkout된 상태이다.  
(<u>HEAD -> google</u>)  
그리고 `reset`은 <span style="color:royalblue">HEAD를 바꾸는 것이 아니고</span>, <span style="color:red">branch(google)을 바꾸는 행위</span>이다.  
이제 "<span style="color:green">git reset main</span>"이라고 하는 명령어는  
<u>main이 가리키고 있는 2번 commit</u>을  
현재 checkout된 google에게(<u>HEAD -> google</u> -> <span style="color:tomato">3번 commit</span>)  
이제 <span style="color:blue">main이 가리키고 있는 2번 commit으로 가리키라</span>고 하는 것과 같다.(<u>HEAD -> google</u> -> <span style="color:tomato">2번 commit</span>)  
<img src="https://user-images.githubusercontent.com/87808288/178182224-779d4da7-fe20-4347-ac91-038596618511.png" width="500">  

<!-- # 6장 시간여행
## 1. revert -->
 
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
