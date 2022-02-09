---
layout: single
title: "git과 github 그리고 명령어"
# categories: Git
categories:
  - Github # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [git, github, terminal] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Git 그리고 Github

<u>git은 버전관리를 도와주는 시스템</u>이고,  
`github`은 그런 <u>git을 통해서 server에 버전을 관리하는 호스팅 서비스</u>이다.

## git?

`local`에서 관리하는 <span style="color:red">버전 관리 시스템</span>(VCS: Version Control System)을 말한다.  
git을 사용하면 <u>소스의 수정에 따라 버전을 관리</u>해준다!

## github?

<span style="color:red">클라우드 방식으로 관리</span>되는 버전 관리 시스템을 말한다.

<u>Github는 단순히 코드를 백업하는 것에서 그 기능을 다하는 것이 아니라</u>,  
`전세계의 오픈소스 프로젝트`들이 모두에게 공유되고  
이를 바탕으로 개발자들의 세계를 확장시켜주는 커뮤니티의 공간이다.

`다른 사람들과 협업하고`, 오픈소스를 `공유하고` 다른 사람들의 의견을 듣는 모든 과정의 중심에 Github가 위치한다.

# 명령어

## ls

현재 위치의 파일 및 디렉토리의 리스트를 보기위해서는

```bash
ls
```

파일과 디렉토리의 목록을 보여준다. (d = 디렉토리, r = 파일)

```bash
- ls -l
```

숨겨진 파일과 디렉토리를 부여준다.

```bash
- ls -al
```

## pwd

현재 위치하고 있는 디렉토리의 위치를 알려주는 명령어

```bash
pwd
```

## mkdir

mkdir을 사용하면 파일을 만들 수 있음

```bash
mkdir
```

## cd

디렉토리를 이동할 때 사용함

```bash
cd 파일의이름
```

이전 디렉토리로 이동하고 싶을 때

```bash
cd -
```

처음 디렉토리로 이동하고 싶을 때

```bash
cd ~
```

## rm

파일을 삭제하고 싶을 때는

```bash
rm 파일의이름.txt
```

디렉토리를 삭제하고 싶을 때는

```bash
rm -r 파일의이름
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
