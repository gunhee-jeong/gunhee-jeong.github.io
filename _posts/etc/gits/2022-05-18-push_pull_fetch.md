---
layout: single
title: "push와 pull & fetch"
# categories: Git
categories:
  - Github # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [github] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# Basic Flow

자신이 작업할 branch를 생성하고 -> 해당 branch의 작업환경에서 파일을 수정하고 작업함 ->  
수정사항 변경이 완료되면 git add . -> git commit -m "Add: 변경사항 수정에 대한 " ->  
git push origin feature/kyle

## git add .

## checkout과 switch의 차이?

## git pull origin master

## git checkout -

## git merge master

# 2장 pull과 fetch
"<span style="color:green">git pull</span>"의 경우 ->  
git remote 명령을 통해 서로 연결된 <span style="color:blue">origin 저장소의 최신 내용</span>을 <span style="color:royalblue">local 저장소로 가져오면서 병합</span>한다.  

"<span style="color:green">git fetch</span>"의 경우 ->  
local 저장소와 origin 저장소의 변경 사항이 다를 때 이를 비교하고  
git merge 명령어와 함께 최신 데이터를 반영하거나 충돌 문제 등을 해결한다.  

<img src="https://user-images.githubusercontent.com/87808288/178413458-5836d500-2755-4463-a88b-50caba05e210.png" width="300">  
위의 이미지와 같이 <u>origin(원격) 저장소에는 L1 버전을</u> 가지고 있고  
local의 main은 L2의 최신버전을 가지고 있다.  
이는 아직 <span style="color:royalblue">L2 버전을 origin에 push하지 않았기 때문에</span> 위의 이미지를 나타내고 있는 것이다.  
그런데 여기서 "<span style="color:green">git push</span>"를 진행하고,  
B 컴퓨터에서 "git pull"을 진행하여 origin/master를 L2 버전의 최신으로 하는 것이 아니라  
"git <span style="color:tomato">fetch</span>"를 진행한다면 아래의 이미지처럼 <u>local은 L1을 가리키게</u> 된다.  
<img src="https://user-images.githubusercontent.com/87808288/178413923-071bf077-95ab-4556-a18f-524d1cba3a84.png" width="300">  

이제 위의 local master를 최신으로 하기 위해서는  
"<span style="color:green">git merge origin/master</span>"를 진행하게되면 -> 아래의 이미지처럼 할 수 있는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/178414235-6c041690-83e0-44f3-b97b-adffaaf5bbb3.png" width="400">  

이제 여기서 A 컴퓨터로 돌아가 L3 버전을 만들고, commit 까지 진행하면 아래의 이미지와 같아진다.  
<img src="https://user-images.githubusercontent.com/87808288/178421381-b76917a0-7bd5-4206-8b24-25f399ba639f.png" width="300">  
B 컴퓨터로 돌아가 R1 버전을 만들고 마찬가지로 commit을 진행하면 아래의 이미지와 같아진다.  
<img src="https://user-images.githubusercontent.com/87808288/178421590-3b454ef9-5dac-4e2e-8e00-fb3394423641.png" width="300">  
이 상황을 한 번 정리하자면 -> <u>A 컴퓨터와 B 컴퓨터</u>는 <span style="color:royalblue">공통적으로 L1, L2</span>를 가지고 있다.  
그런데 `A 컴퓨터`에서는 <span style="color:royalblue">L3</span>를 작업했고, `B 컴퓨터`에서는 <span style="color:royalblue">R1</span>을 작업한 것이다.(같은 branch인 master에서)  

이제 여기서 A 컴퓨터에서 "git push"를 진행하고, B 컴퓨터에서는 "git <span style="color:tomato">fetch</span>"를 진행한다.  
그러면 B 컴퓨터에서는 A 컴퓨터의 push를 가지고는 오지만, merge하지는 않는 것이다.  
<img src="https://user-images.githubusercontent.com/87808288/178422654-a6323967-a600-43a3-88d2-2667f9ec463d.png" width="300">  

이제 <u>HEAD -> master</u> 상태에서 "<span style="color:green">git merge origin/master</span>"를 진행한다면 아래의 이미지와 같아진다.  
<img src="https://user-images.githubusercontent.com/87808288/178423236-bf72453d-020f-4300-913f-90200c12dcab.png" width="600">  
그리고 다시 "git push"를 진행한 후  
A 컴퓨터로 돌아가 "git pull"을 해보면 마찬가지로 위의 이미지 상태가 된다.  
하지만 이런 방법은 merge commit도 만들어지면서 버전을 한눈에 살펴보기에는 조금 어려워지게 된다.  
이럴 때에는 <span style="color:tomato">rebase</span>를 사용해볼 수 있다.  

A 컴퓨터와 B 컴퓨터는 모두 위의 이미지와 같은 상태를 가지고 있다.  
`A 컴퓨터`에서는 <u>left.txt를 수정</u>하여 <span style="color:royalblue">L4를 추가</span>하고 commit 했고,  
`B 컴퓨터`에서는 <u>right.txt를 수정</u>하여 <span style="color:royalblue">R2를 추가</span>하고 commit 했다.  
그리고 <u>A 컴퓨터가 먼저</u> "<span style="color:green">git push</span>"를 수행했다.  
때문에 <u>B 컴퓨터에서는</u> "git <span style="color:tomato">fetch</span>"를 진행해서 push된 내용을 받아오게 되었고, 이는 아래의 이미지와 같다.  
<img src="https://user-images.githubusercontent.com/87808288/178425059-ca979824-db9f-4b78-b627-e306607affb2.png" width="500">  
이때 원래라면 "git merge origin/master"를 진행해도 되겠지만,  
"git <span style="color:red">rebase</span> origin/master"를 진행한다면 ->  
<u>master의 base</u>인 <span style="color:tomato">b6de</span>를 <span style="color:red">caba commit</span><u>(origin/master)로 바꾼다는 것</u>을 의미한다.  
그리고 이로인한 결과는 아래의 이미지와 같다.  
<img src="https://user-images.githubusercontent.com/87808288/178425975-f11b8e4c-8008-4259-a1e1-f3de46005553.png" width="500">  

## (1) fetch
`fetch`는 <u>원격 저장소의 commit 들</u>을 <span style="color:royalblue">로컬 저장소로</span> 가져오게 된다.  
그리고 pull 처럼 <span style="color:royalblue">자동으로 merge하는 것이 아니라</span>, <span style="color:tomato">본인이 직접 확인을 한 후 merge하는 과정</span>을 거친다.  

## (2) pull
<span style="color:green">git pull</span>이란 <u>원격 저장소의 정보를 가져오면서</u> <span style="color:royalblue">자동으로 로컬 브랜치에 merge까지 진행</span>하는 것을 말한다.  
그러나 pull을 사용하면 원격 저장소의 commit을 가져오면서 자동으로 merge하기 때문에  
<span style="color:blue">어떤 내용이 병합되면서 바뀌는지 파악하기가 어려워</span>진다.  

# 3장 request
"pull request"의 핵심은 -> 내가 작업한 code를 다른 동료들이 검토해서 code의 품질을 높이고  
그로인해 main branch의 안정성을 높이는 것에 있다.  


## 1. 

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
