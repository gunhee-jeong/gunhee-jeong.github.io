---
layout: single
title: "생활코딩 -> git flow model"
# categories: Git
categories:
  - Github # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [생활코딩, git] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-18T20:40:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<img src="https://user-images.githubusercontent.com/87808288/179507525-46031d8d-518e-4749-8184-ccc5845ce5e6.png" width="700">  
`main branch`는 <span style="color:blue">언제나 실행 가능한 환경</span>이어야 한다.  
그리고 이런 <u>언제나 실행 가능한 main을 위해</u> <span style="color:tomato">develop branch</span>에서 작업을 하게 된다.  

feature/short branch에서 작업 중인 추가 사항을 1.0이라는 이름으로 출시하고자 한다면  
feature/short을 develop branch와 merge해야한다.  

```bash
git checkout develop
git merge --no --ff feature/short
```

fast foward merge를 하면 commit 기록이 남지 않으므로  
--no --ff 옵션을 사용해 commit message를 일부로 만들어주게 된다.  
그리고 merge 했기 때문에 feature/short branch는 삭제한다.  

```bash
git branch -d feature/short
```

그리고 이제 release/1.0 branch를 만들고 버그 등을 수정하며 commit 하게 된다.   

```bash
git checkout -b release/1.0
```

develop branch에서는 계속해서 개발을 진행해야하므로 우선 merge해줘야 한다.  
그리고 main branch에서도 merge 해야한다.  

```bash
git checkout develop
git merge --no --ff release/1.0
git checkout main
git merge --no --ff release/1.0
git tag 1.0
```

그리고 이제 더이상 release/1.0 branch는 필요하지 않기 때문에 삭제한다.  

```bash
git branch -d release/1.0
```

그러다가 긴급한 것이 발생하면 hotfixes branch를 만들어 급하게 작업해야한다.  
버그를 수정하고 commit 까지 진행한다.  

```bash
git checkout -b hotfixes/1.1
git add hotfix1_1.txt
git commit -am "hotfix 1.1"
```

```bash
git checkout develop
git merge --no --ff hotfixes/1.1
git checkout main
git merge --no --ff hotfixes/1.1
git tag 1.1
git branch -d hotfixes/1.1
```

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
