---
layout: single
title: "npm VS npx VS yarn"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [명령어] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# npm  
npm(Npde Package Manager: <span style="color:blue">노드 패키지 매니저</span>)은 JS 프로그래밍 언어를 위한 <u>패키지 관리자</u>이다.  
자바스크립트 런타임 환경 Node.JS의 기본 패키지 관리자이다.  

[npx]  
- Execute NPM Package Binaries  
- <u>NPM에 속해있는 NPM 패키지</u> 실행도구  

## 기능  
- 오픈 소스 Ndoe.js 프로젝트 게시를 위한 온라인 Repository    
- 패키지 설치, 버전 관리 및 종속성 관리를 지원하는 리포지토리와 상호 작용을 위한 명령줄 유틸리티   

## 명령어  
[npm init]  
package.json을 생성(package.json은 패키지에 대한 정보와 의존중인 버전에 관한 정보를 담고있음)  
[npm install]  
현재 프로젝트에 package를 설치함  
[npm start]  
package.json의 script에 있는 start 속성에 지정된 임의의 명령을 실행함  

# yarn  
yarn(Yet Another Resource Negotiator)도 npm과 마찬가지로 자바스크립트 프로그래밍 언어를 위한  
패키지 관리자이다.  
yarn은 페이스북에서 개발되었고 -> <span style="color:blue">npm의 성능과 보안문제를 해결하기 위해서</span> 개발되었다.  

## npm과 yarn의 공통점  
npm과 yarn은 <u>프로젝트의 의존성을 관리해주기위한 패키지 관리자</u>이다.  
의존성은 프로젝트가 의지하는 것처럼 들리지만 -> 프로젝트가 적절하게 실행되기위해 필요한 소스의 조각을 의미한다.  
프로젝트가 커지면 <span style="color:blue">의존성을 관리하는 것이 어렵기 때문에</span> 패키지 관리자를 필요로 한다.  
종속성을 관리한다는 것은 중속성을 포함, 포함 해제 및 업데이트하는 것을 의미한다.  

[Lock file -> 패키지 잠금 파일: package-lock.json or yarn.lock]  
<u>패키지 잠금 파일</u>은 여러 개발자들이 <span style="color:blue">서로 다른 환경에서 개발하는 것을 방지</span>하기 위해  
패키지 잠금 `파일에 기록된 버전 기준으로 패키지를 설치`한다.  

## npm과 yarn의 차이점  
[설치에서의 차이점]  
npm -> npm은 `Node.js 설치시 자동으로 설치`된다.  
yarn -> yarn은 npm으로 설치해야한다.  

[yarn의 장점]  
<span style="color:blue">yarn</span>은 npm에 비해 <u>빠르고 안정적이며 보안이 강하다</u>.  
npm은 offine mode가 없지만 yarn은 offline mode가 존재한다.  
npm은 local cache를 사용한다.  


<!-- 메소드 위에 변수 선언, 메소드 안에 메소드, 메소드 끝나고 리턴 -->

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
