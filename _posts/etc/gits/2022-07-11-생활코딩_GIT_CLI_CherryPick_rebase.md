---
layout: single
title: "생활코딩 -> GIT CLI - Cherry-pick 그리고 rebase"
# categories: Git
categories:
  - Github # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [생활코딩, git] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-11T12:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 1장 Cherry-pick
<img src="https://user-images.githubusercontent.com/87808288/178238484-7fa1f656-d156-4e41-a0aa-6a2554b8ba1d.png" width="500">  
현재 상황을 살펴보면   
`topic branch`에는 <u>t1, t2, t3</u>라고 하는 파일들을 가지고 있고  
`main branch`에는 <u>m1, m2</u> 파일을 가지고 있다.  
그런데 여기서 main branch에 t2라는 파일만을 merge 하고 싶다면 어떤 방법을 사용해야할까?  
이럴때는 바로 cherry-pick이라는 방법을 사용할 수 있는 것이다.  

우선 <u>main branch에 서있어야</u>하기 때문에 "<span style="color:green">git checkout main</span>"을 <u>HEAD -> main</u> 으로 이동시켜준다.  
그리고 t2 파일을 가지고 있는 commit인 235b762를 <span style="color:tomato">cherry-pick</span> 해야한다.  

```bash
git cherry-pick 235b762
```

그렇게 main branch에 어떤 파일이 들어있는지 확인해보면 -> m1, m2, t2 파일이 들어있는 것을 확인할 수 있다.  
<img src="https://user-images.githubusercontent.com/87808288/178280428-98e01e6b-3ef3-4b18-bd9b-5bc9f9b32a37.png" width="500">  

## 1. Cherry-pick 충돌


# 2장 rebase
`base`는 기본적으로 <span style="color:blue">버전이 갈라지는 뿌리가 되는 commit</span>을 나타내는 git의 용어이다.  
<img src="https://user-images.githubusercontent.com/87808288/178281413-ee317cbf-866d-4511-bac0-746a67464351.png" width="500">  
위의 그림에서 <u>master의 base</u>는 <span style="color:blue">C</span>가 되는 것이다.  
그래서 `rebase`는 쉽게 말해 이 <u>base(뿌리가 되는 commit)를 rebase</u> -> <span style="color:tomato">다시 base를 놓는다</span>는 것을 말한다.  

<img src="https://user-images.githubusercontent.com/87808288/178282759-20001678-7dfd-4386-adf5-2ac74297594f.png" width="500">  
main branch의 base를 t2 commit으로 rebase하면 위의 그림으로 변화한다.  

다시 아래의 이미지와 같은 branch가 존재한다고 하자.  
<img src="https://user-images.githubusercontent.com/87808288/178283442-a20d7170-b5fb-4d4f-aa46-a5e956765b33.png" width="500">  

main(master) branch는 위의 이미지로 볼 때 현재 base가 0042743 commit 이다.  
그런데 main의 base를 8c032e9로 하고자 한다.  
쉽게 말해 그래프 상 t1 -> t2 -> t3 -> m1 -> m2 commit의 순서대로 진행한 것처럼 보이게 하고 싶은 것이다.  

우선 이동하려는 brach로 checkout 해야하므로 "git checkout main"  
그리고 "git rebase topic"을 진행하면 ->  
main branch의 base를 topic이 가리키는 commit으로 rebase 하겠다는 것을 의미한다.  
<img src="https://user-images.githubusercontent.com/87808288/178285580-849f419a-7104-434a-b0e3-d82db1ec926c.png" width="500">  

<img src="https://user-images.githubusercontent.com/87808288/178286346-7658d828-7704-4cdc-9342-94f1e41bc150.png" width="700">  
위의 그림에서 <u>rebase 부분의 그림</u>을 보면  
<u>main branch</u>와 <u>topic branch</u>는 <span style="color:royalblue">base인 C commit 을 공통적으로</span> 가지고 있다.  
그리고 <u>HEAD -> main</u>에서 "<span style="color:green">git rebase topic</span>"을 하면  
<u>main branch의 base를</u> <span style="color:tomato">topic의 t2 commit 으로 rebase</span> 하게 된 것이다.  
그리고 결과적으로 <u>rebase 전의 m1 commit</u>과 <u>rebase 후의 m1 commit</u>은 <span style="color:tomato">워킹 카피가 달라지게</span> 된다.  
rebase 전의 m1은 m1 파일만을 가지고 있지만, rebase 후의 m1은 t1, t2, m1의 파일을 가지고 있다.  

한가지 주의할 것은 <span style="color:red">push 하기 전의 단계(local)에서만 rebase를 사용</span>해야한다는 것이다.  
또한 <u>merge의 결과</u>와 <u>rebase의 결과</u>는 <span style="color:red">무조건 같아야</span> 한다.  

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
