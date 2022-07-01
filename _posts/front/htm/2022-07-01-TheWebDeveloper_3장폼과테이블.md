---
layout: single
title: "The Web Developer -> 3장 HTML 폼과 테이블"
# categories: Git
categories:
  - HTML # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [The Web Developer] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2022-07-01T15:00:00+09:00
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# 3장 HTML 폼과 테이블
## 1. HTML 테이블 개요
표는 데이터 테이블을 말한다.  

역사적으로 표는 웹 사이트의 레이아웃을 잡는 용도로 사용되었다.  
하지만 지금은 테이블을 사용할 때 -> 테이블 형식에 적합한 정보를 주는데 사용해야 한다.  

## 2. 테이블: TR, TD, Th 요소
```html
<!-- heaviest_birds.html -->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Heavies Birds Table</title>
</head>

<body>
  <h1>Heaviest Birds</h1>
  <table>
    <thead>
      <tr>
        <th>Animal</th>
        <th>Average mass [kg (lb)]</th>
        <th>maximum mass [kg (lb)]</th>
        <th>Flighted</th>
      </tr>               
    </thead>
    <tbody>
      <tr>
        <td>Ostrich</td>
        <td>104(230)</td>
        <td>156.8(346)</td>
        <td>No</td>
      </tr>               
      <tr>
        <td>Somali Ostrich</td>
        <td>90(200)</td>
        <td>130(287)</td>
        <td>No</td>
      </tr>
      <tr>
        <td>Wild Turkey</td>
        <td>13.5(29.8)</td>
        <td>39(86)</td>
        <td>Yes</td>
      </tr>
    </tbody>
  </table>

  <h2>V2</h2>
  <table>
    <thead>
      <tr>
        <th rowspan="2">Animal</th>
        <th colspan="2">Average mass</th>
        <th rowspan="2">Flighted</th>
      </tr>
      <tr>
        <th>KG</th>
        <th>LB</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Ostrich</td>
        <td>104(230)</td>
        <td>No</td>
      </tr>               
      <tr>
        <td>Somali Ostrich</td>
        <td>90(200)</td>
        <td>No</td>
      </tr>
      <tr>
        <td>Wild Turkey</td>
        <td>13.5(29.8)</td>
        <td>Yes</td>
      </tr>
    </tbody>
  </table>
</body>
```

### (1) td
td는 테이블 데이터 셀 또는 테이블 데이터를 줄인 말이다.  

### (2) tr
tr은 table row의 줄인 말로

## 3. 테이블: Thead, Tbody, Tfoot 요소

## 4. 테이블: Colspan & Rowspan
```html
<h2>V2</h2>
  <table>
    <thead>
      <tr>
        <th rowspan="2">Animal</th>
        <th colspan="2">Average mass</th>
        <th rowspan="2">Flighted</th>
      </tr>
      <tr>
        <th>KG</th>
        <th>LB</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Ostrich</td>
        <td>104(230)</td>
        <td>No</td>
      </tr>               
      <tr>
        <td>Somali Ostrich</td>
        <td>90(200)</td>
        <td>No</td>
      </tr>
      <tr>
        <td>Wild Turkey</td>
        <td>13.5(29.8)</td>
        <td>Yes</td>
      </tr>
    </tbody>
  </table>
```

<u>Animal</u>, <u>Average mass</u>, <u>Flighted</u> 이렇게 <span style="color:royalblue">3가지의 표의 제목</span>을 만들고  
`Average mass`에 속하는 <u>KG과 LB</u>를 만들고자 한다.  

<u>Animal과 Flighted에는 더이상 속하는 &lt;th&gt;가 없기 때문에</u> <span style="color:royalblue">rowspan</span> 이라는 속성을 주어서 2개의 열을 채우도록 한다.  
`Average mass`에는 <u>KG와 LB &lt;th&gt;를 넣어야 하므로</u> <span style="color:blue">colspan="2" 속성을</span> 추가한다.  

## 5. form 요소
폼 요소 자체는 사실 눈에 띄지 않는다.  
`폼`은 사실 껍데기나 <u>컨테이너</u>에 더 가깝다고 말할 수 있다.  
<span style="color:tomato">그룹화된 모든 입력을 담는 상자</span>이다.  
<span style="color:blue">입력 내용을 그룹화</span>하고 -> 작은 <span style="color:red">배송 라벨을 붙여 어떤 지정된 목적지로 제출</span>한다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Heavies Birds Table</title>
</head>

<body>
  <h1>Forms Demo</h1>

  <form action="/search/"></form>
</body>
```

&lt;form&gt;에서 `action 속성`은, 폼이 제출되었을 때  
<span style="color:blue">데이터를 보낼 위치와 시간</span>을 action 속성에 지정하게 된다.  
이 <u>action 속성에 지정된 url로</u> 폼 안에 담긴 라벨들의 값들이 전송되어 보내지게 된다.  
(조금 더 정확하게 말해보면 -> 현재 폼 태그가 있는 곳이 reddit.com이라면 <u>reddit.com</u><span style="color:royalblue">/search</span>로 전송된다.)  

## 6. 일반적인 입력 형식
## 7. 가장 중요한 레이블
## 8. HTML 버튼
## 9. 이름 속성 

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
