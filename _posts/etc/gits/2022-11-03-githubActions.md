---
layout: single
title: "GitHub Actions의 개념"
# categories: Git
categories:
  - Github # HTML CSS JavaScript Server Algorithm Wecode Programmers CS Github Blog
tag: [gitignore] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-11-03T18:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
<style>
.crimson {
  color: crimson;
  font-weight: bold;
}

.cf {
  color: CornflowerBlue;
  font-weight: bold;
}

.teal {
  color: teal;
  font-weight: bold;
}

.forestgreen {
  color: foresgreen;
  font-weight: bold;
}
</style>

# GitHub Actions
(DaleSeo님 블로그) : [GitHub Actions의 소개와 핵심 개념](https://www.daleseo.com/github-actions-basics/)

# 🔴 GihHub Actions?
GitHub Actions는 GitHub에서 제공하는 <span class="cf">CI</span>(Continuous Integration, 지속 통합)와 <span class="cf">CD</span>(Continuous Deployment, 지속 배포)를 위한 서비스를 말한다.

GitHub Actions를 사용하면 자동으로 코드 저장소에서 어떤 이벤트가 발생했을 때 특정 작업이 일어나게 하거나 주기적으로 어떤 작업들을 반복해서 실행시킬 수 있다. 예를 들어, 누군가가 코드 저장소에서 Pull Request를 생성하게 되면 GitHub Actions를 통해 해당 코드 변경 부분에 문제가 없는지 <span class="cf">여러 검사를 진행</span>하게 할 수 있다. 또한 새로운 코드가 main 브랜치에 push되면 GitHub Actions를 통해 소프트웨어를 build하고 상용 서버에 배포할 수도 있다.

이런식으로 <span class="cf">지속적으로 수행해야하는 반복 작업</span>들을 업계에서는 소위 CI/CD라고 줄여서 부르고 있다. 사람이 매번 직접 하기에는 비효율적이고 실수의 위험도 있다보니 GitHub Actions을 통해 CI/CD를 설정해볼 수 있다.

# 🔴 Workflows
워크플로우는 repository 내에서 `.github/workflows` 폴더 아래에 위치한 YAML 파일로 설정하며, 하나의 코드 저장소에는 여러 개의 워크플로우, 즉 여러 개의 YAML 파일을 생성할 수 있다. 워크플로우는 <span class="cf">자동화 시켜놓은 작업 과정</span>을 뜻하는 것이다.

YAML 파일에는 크게 2가지를 정의하게 된다. `on` 속성은 <span class="cf">해당 워크플로우가 언제 실행되는지</span>에 관한 정의이다.

예를 들어, 코드 저장소의 main 브랜치에 push 이벤트가 발생할 때 마다 워크플로우를 실행하려면 아래의 코드와 같다.

```yml
# .github/workflows/ci.yml
on:
  push:
    branches:
      - main

jobs:
  # ...(생략)...
```

# 🔴 Jobs
GitHub Actions에서 Job(작업)이란 독립된 가상 머신 또는 컨테이너에서 돌아가는 하나의 처리 단위를 의미한다.

작업의 세부 내용으로는 여러 가지 내용을 명시할 수 있는데, 필수로 들어가야 하는 `runs-on` 속성을 통해 리눅스나 윈도우즈와 같은 <span class="cf">실행 환경을 지정</span>해줘야 한다.

에를 들어 우분투의 최신 실행 환경에서 해당 작업을 실행하고 싶다면 아래와 같이 설정하게 된다.

```yml
# .github/workflows/ci.yml
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
```

# 🔴 Steps
단순한 작업이 아닌 이상 하나의 작업은 일반적으로 여러 단계의 명령을 순차적으로 실행하게 된다. 그래서 GitHub Actions에서는 각 작업(job)이 하나 이상의 단계로 모델링 된다.

작업 단계는 단순한 <span class="cf">command나 script</span>가 될 수도 있고 action이라고 하는 좀 더 복잡한 명령일 수도 있다. command나 script를 실행할 때는 `run` 속성을 사용하며, <span class="cf">action</span>을 사용할 때는 `uses` 속성을 사용한다.

자바스크립트 프로젝트에서 테스트를 돌리려면 코드 저장소에 코드를 작업 실행 환경으로 내려 받고, 패키지를 설치한 후, 테스트 스크립트를 실행해야한다. 이 3단계의 작업은 아래의 `steps` 속성을 통해서 명시될 수 있다.

```yml
# .github/workflows/ci.yml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm install
      - run: npm test
```

워크플로우 파일 내에서 작업 단계를 명시해줄 때는 주의할 부분이 있는데, YAML 문법에서 시퀀스 타입을 사용하기 때문에 각 단계 앞에 반드시 `-`를 붙여야 한다.

# 🔴 Actions
(Marketplace) : [Actions](https://github.com/marketplace?type=actions)

액션은 GitHub Actions에서 빈번하게 필요한 반복 단계를 재사용하기 용이하도록 제공되는 일종의 작업 공유 메커니즘이다. 액션은 하나의 코드 저장소 범위 내에서 여러 워크플로우 간에서 공유를 할 수 있을 뿐만 아니라, 공개 코드 저장소를 통해 액션을 공유하면서 GitHub 상의 모든 코드 저장소에서 사용이 가능해진다.

GitHub에서 제공하는 대표적인 <span class="cf">공개 액션</span>으로 바로 위 코드에서도 사용된 체크 아웃 액션(`actions/checkout`)을 이야기할 수 있다.

그리고 GitHub Marketplace에서는 많은 벤더(vendor)가 공개해놓은 다양한 액션을 접할 수 있다.

<!-- ① ② ③ ④ ⑤ ⑥ ⑦ ⑧ ⑨-->

<!-- ### 2. Link 넣기

```

유형 1: (설명어를 입력) : [gunhee's coding blog](https://gunhee-jeong.github.io/)
유형 2: (URL 자동연결) : <https://gunhee-jeong.github.io/>
유형 3: (동일 파일 내 '문단으로 이동') : [1. Header로 이동](###-1-header)

```

```bash
.next/static
        ├── AbmKMg9BFeVUuJ7lsQ1w8
        ├── chunks                 // 여러 페이지에서 공통으로 사용되는 번들 파일
        │       └──  pages         // 각 페이지의 번들 파일
        ├── runtime                // 웹팩과 next의 런타임과 관련된 번들 파일
        ├── css                    // 애플리케이션의 모든 페이지에 대한 글로벌 CSS 파일
        └── media                  // 정적으로 가져온 이미지 next/image가 여기에 해시 및 복사
```

<details>
<summary class="black">코드</summary>
<div markdown="1">

```jsx
// helloWorld!
const hello = 'hi';
```
</div>
</details>

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
