---
layout: single
title: "Spread Operator를 이용한 Instagram 로그인 & 비밀번호 value 저장"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [회원가입, 로그인, instagram, 전개연산자] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

```java
//Login Component
function Login() {
  const [loginValues, setLoginValues] = useState({ email: '', password: '' });
  const navigate = useNavigate();

  const handleInput = e => {
    const { name, value } = e.target;
    setLoginValues({ ...loginValues, [name]: value });
  };
  const handleBtn = !(loginValues.email.includes('@') && loginValues.password.length > 4);

  const pwInput = useRef();

  const focusPw = e => {
    if (e.code === 'Enter') {
      pwInput.current.focus();
    }
  };

  return (
    ...
    <div>
      <form>
        <input
          name="email"
          value={loginValues.email}
          className="inputBox"
          type="text"
          placeholder="전화번호, 사용자 이름 또는 이메일"
          onChange={handleInput}
          onKeyUp={focusPw}
          autoFocus
        />
        <input
          name="password"
          value={loginValues.password}
          className="inputBox"
          type="password"
          placeholder="비밀번호"
          ref={pwInput}
          onChange={handleInput}
        />
        <button
          name="data"
          type="button"
          className="log-btn"
          disabled={handleBtn}
          onClick={goToMain}
          style={ { cursor: handleBtn ? 'default' : 'pointer' } }
        >
          로그인
        </button>
      </form>
    <div/>
    ...
  )
}
```

form 태그 안의 <u>id를 입력하는 input 태그</u> 안에는  
attribute로 `name`과 `value`를 만들어준다.

##### <span style="color:green">name="email"</span>

key name의 값으로는 `"email"`을 넣어주었다.

##### <span style="color:green">const [loginValues, setLoginValues] = useState({ email: '', password: '' });</span>

<u>ID의 input과 PW의 input의 값</u>을 저장하기 위해 `useState`를 사용했다.  
화면이 rendering되면서 loginValues에 담기는 초기값은  
{ email: ‘’, password: ‘’ }으로 <u>property의 키를 설정</u>하는 역할을 한다.  
이제 <u>form 태그 안에 위치한 ID와 PW</u>에 `onChange 이벤트`가 감지되면 ->  
<span style="color:red">handleInput 함수</span>가 작동된다.

##### <span style="color:green">const { name, value } = e.target;</span>

ID를 입력하면 그 키값이 e.target의 property 키인 value에 담기는데,  
이를 이용하여 <u>const { name, value }</u>에 <span style="color:red">분해구조할당</span>을 하게 된다.  
e.target의 property 키에는 위에서 input 태그에 <u>직접 지정한 키 name</u>과  
`키보드에서 입력한 value`가 담긴 <u>키 value</u>가 존재한다.  
<span style="color:red">e.target은 object</span> 타입이고, object의 분해구조할당은 index가 아닌  
`key name을 기준으로` 하기 때문에 정렬 순서와는 상관이 없다.  
그렇게 <u>const name에는 "email"</u>이 할당되고, <u>value에는 "입력값"</u>이 할당된다.

##### <span style="color:green">setLoginValues({ ...loginValues, [name]: value });</span>

이제 위에서 정의된 const **name**과 **value**를 가지고 useState를 사용한다.  
<span style="color:red">...loginValues</span>는 -> <u>ID와 PW모두가 loginValues에</u> `중첩되지 않은`  
`object 타입으로 할당되야하므로` 이를 위해 사용된 코드이다.  
화면이 rendering되면서 loginValues에는 <span style="color:blue">{ email: "", password: "" }</span>이 할당된다.  
<span style="color:red">전개 연산자</span>를 사용했으므로, 키보드로 ID를 입력하는 순간 ->  
기존의 loginValues의 property들이 spread되고 ->  
<u>{ email: “”, password: “”, email: "h" }</u>로 property의 키인 email이  
중복되므로 `{email: ‘hello’, password: “”}`으로 할당된다.

만약에 코드가 <span style="color:green">setLoginValues({ loginValues, [name]: value })</span> 였다면  
loginValues는 `중첩된 object가 형성`된다.  
&nbsp; ID input창에 "h"를 입력하는 순간 ->  
&nbsp; <u>setLoginValues({ { email: “”, password: “” }, email: h })</u>으로  
&nbsp; `중첩된 object`가 형성된다.

그리고 <span style="color:red">[name]: value</span>이 사용된 이유는 const name의 값은 "email"로 ->  
<span style="color:red">name이 변수</span>(식별자명)이기 때문이다!  
&nbsp; 우리는 name의 문자 그 자체가 아닌, <u>변수 name에 저장된 "email"</u>이 필요하기 때문이다.  
&nbsp; object의 `마침표 연산자`는, 객체의 property 키에 접근할 수 있지만  
&nbsp; <u>일반 변수에는 접근할 수 없다</u>. 반면에 <span style="color:red">대괄호 연산자</span>는 `변수에도 접근할 수`  
&nbsp; 있으므로 대괄호 연산자를 사용한 것이다.

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
