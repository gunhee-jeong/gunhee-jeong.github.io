---
layout: single
title: "input 태그, label 태그, select 태그"
# categories: Git
categories:
  - CSS # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [input, 라벨 태그] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---
# input 태그  
## input 태그의 속성  
input 태그의 속성에는 type, name, readonly, maxlength, required,  
autofocus, placeholder, pattern 등이 있다.  
### type  
<u>input 태그의 모양</u>을 다양하게 변경시킬 수 있는 속성이다.  
- type에는 text, radio, checkbox, password, button, hidden, fileupload,  
submit, reset 등을 지정할 수 있다.  

#### checkBox  
체크박스는 클릭하면 선택되고, 재클릭시 선택이 해제되는 기본 구조를 가진다.  
```html  
<input type="checkbox" name="xxx" value="yyy" checked />  
```  
[name]  
전달한 값의 이름이다.  

[value]  
전달될 값이 담긴다.  

#### required  
<span style="color:blue">필수 입력 필드의 지정</span>으로 -> input 칸의 내용이 `빈칸이면 넘어가지 않도록 설정`할 수 있다.  

#### email  

#### range  

#### text  
한 줄짜리 텍스트를 입력할 수 있는 텍스트 상자이다.  

#### submit  

#### reset  
사용자가 입력한 모든 정보를 지울 수 있다.  

#### file  
<u>파일을 첨부</u>할 수 있는 버튼으로, <span style="color:blue">accept 속성</span>을 사용하여 <u>제출 가능한 파일의 양식을 지정</u>할 수 있다.  
```html
<input type="file" accept=".doc, .docx">
```  

#### number  
```html
<input type="number" name="quantity" min="2" max="10" step="2" value="2">
```  
<img src="https://user-images.githubusercontent.com/87808288/164394446-360f7b50-4da9-4754-b502-f5be0b721036.png" width="100" height="200">   

## input 태그와 관련된 문제해결  

### input 테두리 색상 변경하기  


<img src="https://user-images.githubusercontent.com/87808288/152899593-19485d54-fddd-4fb7-a4be-d88330a4ff9d.png" width="300" height="200">  
위의 사진에서 전화번호와 비밀번호에 해당하는 것은 `input 태그`이다.  
사진에서는 border의 색상이 black이지만 이를 -> #dbdbdb 색상으로 바꾸어야한다.  
input 태그의 <span style="color:red">border 색상</span>을 바꾸기 위해서는 border를 사용하면 된다!

```css
input {
  border: 1px solid #dbdbdb;i
}
```

  <img src="https://user-images.githubusercontent.com/87808288/152901423-6f3f012d-9f88-4b75-990c-dede904e8389.png" width="300" height="200">  

### 클릭시 색상 변경을 없애는 방법   

```css
input:focus {
  outline: none;
}
```

# label 태그  
`label 태그`가 하는 일은 <u>input 태그를 제어</u>하여 <span style="color:blue">상태값을 변경하도록 돕는</span> 것이다.  

## label 태그의 역할  
[사용성의 확대]  
체크박스를 사용할 때에도 <span style="color:blue">클릭의 영역</span>이 단순히 체크박스에 국한되는 것이 아니라  
label 태그의 사용으로 -> `텍스트까지 선택영역의 범위가 넓어`지게된다.  

## input 태그와 label 태그의 연결  
input 태그와 label 태그의 연결은 크게 2가지로 나눌 수 있다.  
<span style="color:blue">명시적</span>(explicit) 연결과 <span style="color:blue">암시적</span>(implicit) 연결로 나뉜다.  

### 명시적 연결  
명시적 연결은 <u>label 속성의 for</u>와 <u>input 태그의 id 속성</u>을 연결하는 것을 말한다.  
```html
<label for="user-id">아이디
  <input type="text" id="user-id" />
</label>
```  

### 암시적 연결  
암시적 연결은 input 요소를 label 요소로 감싸 연결하는 방법이다.  
```html
<label>아이디 <input type="text" /></label>
```  

# select 태그  
select 태그는 항목을 선택할 수 있는 태그다.  
<img src="https://user-images.githubusercontent.com/87808288/164389244-c18ab2a5-0c6b-4931-bd8c-7de99a881a96.png" width = "250" height = "200">  

```html
<form>
  <select name = 'city'>
    <optgroup label = '서울'>
      <option value = "songpa-gu">송파구</option>
      <option value = "gangnam-gu">강남구</option>
      <option value = "seocho-gu">서초구</option>
      <option value = "junggu-gu">중구</option>
    </optgroup>
  </select>
    <optgroup label = '경기도'>
    </optgroup>
  </select>
</form>
```  
## select 태그의 속성   
### size  
size 속성은 한 번에 표시할 수 있는 <span style="color:blue">항목의 수</span>를 나타낸다.  

### multiple  
multiple 속성은 <span style="color:blue">다중선택을 허용할 것인지</span>를 지정하는 속성이다.  

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
