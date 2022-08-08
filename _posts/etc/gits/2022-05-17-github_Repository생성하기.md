---
layout: single
title: "Github repository(저장소) 생성"
# categories: Git
categories:
  - Github # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [Github Tutorial] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함  
date: 2022-05-17T09:50:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# local 프로젝트를 github 서버로
우선 Github에 접속해서 <u>repository를 생성</u>한다 ->  
아래로 내리다보면 페이지에 <span class="royalblue">...or create a new repository</span>가 있는데  
거기서 "<span class="tomato">git remote add origin 주소</span>"로 되어있는 것을 <u>복사하여 터미널에 붙여넣는다</u> ->  

정상적으로 등록이 되었는지 확인하기 위해 터미널에서 <span class="tomato">git remote</span>를 입력해서 <u>origin이 나오면 성공</u> ->  
git hist로 살펴보면 아직 server로는 올라가있지 않기 때문에   
"<span class="tomato">git push</span>"를 통해 local의 commit들을 server로 올려야 한다.  


# 2. fork 받아 사용하기
<span class="blue">먼저 PR을 보내고 싶은 repository를 fork</span>한다.  
그러면 <span class="royalblue">자신의 계정의 GitHub에 동일한 repository가 복사</span>된다.  

이제 <span class="blue">Code</span>를 클릭하고 주소를 <span class="royalblue">repository 주소를 복사</span>한다.  

```bash
git clone <내 계정에 fork된 repository 주소>

git remote add upstream <PR을 보낼 원격 repository 주소>
```

PR을 보내는 과정에서 <span class="red">원격 저장소</span>는 <span class="tomato">upstream</span>과 <span class="tomato">origin</span> 이렇게 2개가 필요하다.  
로컬에서는 내 계정의 repository도 원격이고, upstream의 repository도 원격이기 때문이다.  
그리고 "<span class="darkorange">git remote -v</span>"를 통해 origin과 upstream이 같은지 확인할 수 있다.  
만약 origin이나 upstream이 잘못 설정되어 있다면  
"<span class="darkorange">git remote remove origin</span>"을 통해서 설정을 삭제할 수 있다.  

```bash
git fetch upstream

git rebase upstream/main

git switch -c xunxee upstream/main
```

<style>
.red {
  color: red;
  font-weight: bold;
}

.tomato {
  color: tomato;
  font-weight: bold;
}

.blue {
  color: blue;
  font-weight: bold;
}

.royalblue {
  color: royalblue;
  font-weight: bold;
}

.forestgreen {
  color: foresgreen;
  font-weight: bold;
}

.darkorange {
  color: darkorange;
  font-weight: bold;
}
</style>

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
