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
### (1) &lt;input&gt;
&lt;input&gt; 안의 속성인 type이 &lt;input&gt;의 작동 방식을 바꾸는 역할을 한다.  
또한 &lt;input&gt;는 닫는 태그가 존재하지 않으며 그래서 두 태그 사이에 내용을 넣지 않는다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Forms Demo</title>
</head>

<body>
  <h1>Forms Demo</h1>

  <form action="/tacos">
    <input type="text" placeholder="user Id">
    <input type="password" placeholder="passoword">
    <input type="color">
    <input type="number">
  </form>
</body>
```

위의 코드와 같이 &lt;input&gt;의 type 속성으로 다양한 속성을 사용할 수 있다.  

`placeholder 속성`은 입력란의 <u>임시 텍스트를 지정하는 속성</u>이다.  
원래의 입력란은 뭔가를 입력하기 전이라 비워져 있지만,  
placeholder를 사용하는 순간 비어져있는 공간에 text를 입력할 수 있게 된다.  
그렇다고해서 placeholder가 모든 type에서 사용할 수 있는 것은 아니다.  
이렇게 placeholder는 <span style="color:blue">무엇을 입력하는지 알려준다는 점에서 중요</span>하다.  

## 7. 가장 중요한 레이블
&lt;`label`&gt;은 <span style="color:blue">접근성</span>과 <span style="color:blue">폼을 쓰기 편하게 한다는 점</span>에서 중요한 태그이다.  
&lt;label&gt;은 <u>시각적으로 텍스트를 보여주는 것 이상의 기능을</u> 한다.  

보이지 않지만 <span style="color:tomato">체크박스와 연결</span>되어 있기 때문이다.  
또한 <u>Form control 및 텍스트와 직접적으로 연결</u>되어 있고,  
두 요소를 연결 시 <span style="color:royalblue">레이블 자체를 클릭할 수 있게도</span> 해준다.  
&lt;label&gt;을 통해 질문을 만들고 이를 체크박스와 연결했다면,  
&lt;label&gt;을 클릭하더라도 체크박스를 동작하게 만들 수 있다.  

&lt;label&gt;를 사용하기 위해서는  
<u>&lt;input&gt;</u>안에 <span style="color:blue">id 속성</span>을 추가해야한다.  
그리고 <u>똑같은 id의 값</u>을 <span style="color:blue">&lt;label&gt;의 for 속성</span>으로 지정해주어야한다.  
아래의 코드를 보면, &lt;input&gt;의 id 속성(cheese)와 &lt;label&gt;의 for 속성(cheese)가 같은 것을 알 수 있다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Forms Demo</title>
</head>

<body>
  <h1>Forms Demo</h1>

  <div>
    <label for="cheese">Do you like cheese?</label>
    <input type="checkbox" name="cheese" id="cheese">
  </div>
</body>
```

위의 코드와 같은 결과를 만들 수 있는 방법이 하나 더 있는데,  
그것은 &lt;label&gt;안에 &lt;input&gt;를 중첩하여 넣어주는 것이다.  
이렇게 구성하면 for 속성과 id 속성이 없더라도 위와 같은 결과를 만들 수 있으나, 자주 쓰이지는 않고 있다.  
개인적으로도 가독성적인 측면에서 아래의 코드보다는 위의 코드가 보기 좋은 것 같다.  
그리고 CSS를 통해 스타일을 주더라도 태그들이 따로따로 분리되어있어야 편리하기 떄문인 것 같다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Forms Demo</title>
</head>

<body>
  <h1>Forms Demo</h1>

  <div>
    <label>Do you like cheese?
      <input type="checkbox" name="cheese">
    </label>
  </div>
</body>
```

## 8. HTML 버튼
&lt;button&gt;는 여는 태그와 닫는 태그로 구성된다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Forms Demo</title>
</head>

<body>
  <h1>Forms Demo</h1>
  <button>Outside form</button>

  <form action="/tacos">
    <button type="button">Please do not submit the form</button>
    <input type="text" placeholder="user Id">
    <input type="password" placeholder="passoword">
    <button>In the middle</button>
    <input type="color">
    <input type="number">

    <button>Submit</button>
  </form>
</body>
```

폼에 버튼이 포함되어 있는데 이때 버튼을 누르면  
폼을 제출하지 않겠다고 따로 명시해놓지 않았다면 폼이 제출된다.  

"Outside form" 버튼을 클릭해도 해당 버튼은 &lt;form&gt; 밖에 위치하기 때문에 아무일도 일어나지 않는다.  
&lt;form&gt;안에 버튼이 있다면 기본값으로 -> 해당 폼을 제출하게 된다.  

&lt;input&gt; 처럼 &lt;button&gt;도 type이라는 속성을 가진다.  
&lt;form&gt; 안에 있는 "Please do not submit the form" 버튼의 속성 type을 "button"으로 주게되면  
&lt;button&gt;를 클릭해도 폼을 제출하지 않고 button으로만 사용된다.  
반대로 &lt;button&gt;의 type을 "submit"으로 설정하면 다시 폼을 제출한다.  

## 9. 이름 속성 
&lt;`input`&gt; 안의 <span style="color:blue">name이라는 속성</span>의 값은 &lt;form&gt;가 제출되었을 때  
<u>&lt;form&gt;의 action 속성</u>에 저장되어있는 <span style="color:royalblue">url로 보내지는 값</span>이다.  
이렇게 name 속성은 중요한 역할을 한다.  
결국 <span style="color:blue">서버로 데이터를 전송할 때 사용</span>하게 된다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Forms Demo</title>
</head>

<body>
  <h1>Forms Demo</h1>

  <form action="/tacos">
    <p>
      <label for="username">Enter a UserName</label>
      <input id="username" type="text" placeholder="user Id" name="username">
    </p>
    <button>Submit</button>
  </form>
</body>
```

## 10. 구글과 레딧 검색하기
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <!-- google form -->
  <form action="https://www.google.com/search">
    <label for="userName">Searching</label>
    <input type="text" id="userName" name="q" placeholder="무엇이든 입력하세요">
    <button>Search Google</button>
  </form>
  <!-- https://www.google.com/search?q=tocos -->

  <!-- youtube form -->
  <!-- https://www.youtube.com/results?search_query=dog -->
  <form action="https://www.youtube.com/results">
    <label for="youtubeSearch">Searching</label>
    <input type="text" id="youtubeSearch" name="search_query" placeholder="무엇이든 입력하세요">
    <button>Search Youtube</button>
  </form>
</body>
</html>
```

<u>&lt;form&gt;, &lt;label&gt;, &lt;input&gt;, &lt;button&gt;</u>등을 사용하여 구글과 유튜브 등과 연결하여 검색할 수 있다.  
&lt;<span style="color:royalblue">form</span>&gt;의 <span style="color:blue">action 속성</span>에는, 폼이 제출되었을 때 <span style="color:tomato">데이터를 보낼 위치와 시간등을 지정</span>하게 된다.  
&lt;<span style="color:blue">label</span>&gt;와 &lt;<span style="color:blue">input</span>&gt;는 <span style="color:tomato">id 속성</span>과 <span style="color:tomato">for 속성</span>으로 연결하였고  
&lt;input&gt;의 <span style="color:red">name 속성</span>은 폼이 제출되었을 때 -> <u>&lt;form&gt;의 action 속성에 저장되어있는 url로 보내지는 값</u>인데  
"q"와 "search_query"로 저장하여 사용할 수 있다.  

## 11. 라디오 버튼, 체크박스와 선택창
### (1) 체크박스
`체크박스`는 꼭 <u>&lt;label&gt; 처리를</u> 해야한다.  
&lt;label&gt;로 관리하지 않으면 나중에 checkbox의 설정이 점점 복잡해진다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <form action="/birds">
    <input type="checkbox" name="agree_tos" id="agree">
    <label for="agree">I agree to everything</label>
  </form>
</body>
```

그리고 <u>체크박스가 처음부터 체크되어 있도록</u> 만들 수도 있다.  
그럴때는 <span style="color:royalblue">&lt;input&gt;의 속성</span>으로 <span style="color:blue">checked</span>를 넣어주면 된다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <form action="/birds">
    <input type="checkbox" name="agree_tos" id="agree" checked>
    <label for="agree">I agree to everything</label>
    <button>Submit</button>
  </form>
</body>
```

위 코드에서 Submit 버튼을 누르면 -> &lt;input&gt;의 속성으로 checked가 되어있으므로 체크박스가 체크되어있고  
따라서 /birds?agree_tos=on으로 이동한다.  
체크가 해지되어있다면  /birds로 이동한다.  

### (2) 라디오 버튼
라디오 버튼이 체크박스와 다른 것은 그룹에서 딱 하나만 선택이 가능하다는 것이다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <form action="/birds">
    <label for="xs">XS</label>
    <input type="radio" name="size" id="xs">
    <label for="s">S</label>
    <input type="radio" name="size" id="s">
    <label for="m">M</label>
    <input type="radio" name="size" id="m">
    <button>Submit</button>
  </form>
</body>
```

위의 코드에서 <u>라디오 버튼을 클릭하고 Submit 버튼을 누르면</u> <span style="color:royalblue">size=on이 제출</span>된다.  
우리는 사용자가 어떤 사이즈를 선택했는지 알고 싶은 것인데 -> <span style="color:royalblue">on이라는 정보가 제출된 것</span>이다.  
그래서 아래의 코드와 같이 &lt;input&gt;의 <span style="color:red">속성으로 value를 추가</span>하여 작성해주어야 한다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <form action="/birds">
    <label for="xs">XS</label>
    <input type="radio" name="size" id="xs" value="xs">
    <label for="s">S</label>
    <input type="radio" name="size" id="s" value="s">
    <label for="m">M</label>
    <input type="radio" name="size" id="m" value="m">
    <button>Submit</button>
  </form>
</body>
```

<span style="color:red">value라는 속성</span>은 form을 제출했을 때 <u>서버에 전송되는 값</u>인 것이다.  
&lt;label&gt;의 텍스트로 작성한 것은 사용자에게 보여지는 용도이며,  
이 <span style="color:blue">값을 전달하는 유일한 수단</span>은 &lt;input&gt;의 <span style="color:tomato">value 속성</span>인 것이다.  

### (3) &lt;select&gt;
&lt;`select`&gt;는 &lt;<span style="color:blue">option</span>&gt;와 함께 사용하여 드롭박스를 만들 수 있다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>
  <label for="meal">Please Select an Entree</label>
  <select name="meal" id="meal">
    <option value="fish">Fish</option>
    <option value="veg">Vegetarian</option>
    <option value="steak">Steak</option>
  </select>
<body>
</body>
```

체크박스와 마찬가지로 특정 &lt;option&gt;의 속성으로 <span style="color:blue">selected</span>를 주면 -> 드롭박스에서 자동으로 선택되도록 한다.  

## 12. 범위 및 텍스트 영역
### (1) range 속성
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <p>
    <label for="cheese"">Amount of Cheese:</label>
    <input type="ragne" id="cheese" min="1" max="100" value="50" step="7" name="cheese_level">
  </p>
</body>
```

위의 코드에서 &lt;input&gt;의 type 속성으로 range를 설정하면 -> 범위 선택을 할 수 있다.  
&lt;input&gt; range의 value 속성은, 체크박스에서 checked와 비슷한 역할을 한다.  
value를 미리 설정해두면 초기값으로 사용된다.  
step 속성은 설정한 값의 크기만큼 value가 조정된다.  

### (2) num 속성
아래의 코드와 같이 &lt;input&gt;의 속성으로 number를 주면 커머스에서 자주 사용되는 개수 선택 기능을 만들 수 있다.  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <label for="num">개수 선택</label>
  <input type="number" id="num" name="numbers" min="1" max="10" step="2">
</body>
```

### (3) &lt;textarea&gt;
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
  <p>
    <label for="requests">Any Special Requests?</label>
    <br>
    <textarea id="requests" name="requests" placeholder="Type something here" rows="10" cols="40"></textarea>
  </p>
</body>
```

&lt;textarea&gt;는 기본적으로 2줄을 제공하지만  
rows 속성을 사용하면 원하는 기본값으로 줄을 제공할 수 있다.  

<!-- ## 13. HTML5 폼의 유효성 검사 -->

<img src="https://user-images.githubusercontent.com/87808288/177025447-1835b031-d35c-48ea-a0a5-bcf7e9ee6741.png" width="500">  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1>Race Registration!</h1>
  <form action="">
    <div>
      <label for="firstN">First Name</label>
      <input type="text" id="firstN" name="firstName" required>
      <label for="lastN">Last Name</label>
      <input type="text" id="lastN" name="lastName" required>
    </div>
    <p>Select a Race:</p>
    <div>
      <input type="radio" id="fun" name="marathon" value="fun">
      <label for="fun">Fun Run 5K</label>
    </div>
    <div>
      <input type="radio" id="half" name="marathon" value="half">
      <label for="half">Half Marathon</label>
    </div>
    <div>
      <input type="radio" id="full" name="marathon" value="full">
      <label for="full">Full Marathon</label>
    </div>
    <div>
      <label for="email">Email</label>
      <input type="email" id="email" required>
      <label for="password">password</label>
      <input type="password" id="password" required>
    </div>
    <div>
      <label for="age">Select Age Group</label>
      <select id="age" name="ageGroup">
        <option value="18">18 이하</option>
        <option value="35">18 ~ 35</option>
        <option value="60">36 ~ 60</option>
      </select>
    </div>
    <button>Register!</button>
  </form>
</body>
</html>
```

<!-- <span style="color:royalblue"> -->

<!-- ### 2. Link 넣기

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title></title>
</head>

<body>
</body>
```

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
