---
layout: single
title: "Design Pattern"
# categories: Git
categories:
  - React # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [디자인패턴, MVC, Flux, controller, view, model] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

# 학습 목표
- 전역 상태 관리 라이브러리로서의 Redux의 필요성을 이해한다  
  &nbsp; redux를 왜 필요로하게 되었는가?
- Action, Dispath, Reducer, Store 등 Redux의 핵심 개념을 이해한다
- React-Redux 라이브러리에서 제공하는 useSelector, useDispath hook을 사용할 수 있다

# Design Patten  

디자인 패턴은 소프트웨어 개발 도중 개발자들이 겪을 수 있는 여러 어려움들에  
대한 일종의 모범답안이라고 할 수 있다.  
## 왜 디자인 패턴을 사용해야 하는가?  
[<span style="color:blue">바퀴를 재발명하지 마라</span>(Don't reinvent the wheel)]  
대부분의 어려움은 이미 누군가가 겪어봤으니 <u>그들이 패턴화 해둔 문제 해결 방식</u>을 적용해 생산성을 높일 수 있다.  
또한 많은 사람들이 많이 사용해본 구조를 활용한다면 -> 내가 작성한 코드의 문제점에 대해서도 검증된 방법으로   
해결방안을 찾을 수 있어 `효과적으로 코드를 개선`할 수 있다는 장점을 갖는다.  

<u>큰 규모의 건축물</u>을 쌓아 올리기 위해서는 -> 규모가 작을 때보다 <u>효율적이고 체계적인 약속</u>이 필요하다.  
이런 상황에서, 디자인 패턴은 <u>복잡도가 높은 상황에서</u> -> 팀이 해야할 일을 장황하지 않게, 디테일한 설명을 다시 설명하지 않게  
<span style="color:blue">미리 약속해 둔 한 단어로 표현</span>할 수 있도록 도와준다.  
축구와 같은 스포츠의 세트피스 상황에서 팀원들끼리 사전에 약속한 포메이션으로 각각의 상황에 맞게 대처하는 것처럼 말이다.  

## MVC(Mode - View - Controller)  
대표적인 디자인 패턴들 중 하나로 <span style="color:red">MVC 패턴</span>이 있다.  
하나의 프로젝트의 구성 요소의 역할에 따라 <span style="color:red">Model</span>, <span style="color:red">View</span>, <span style="color:red">Controller</span>로 나뉘어 작성하는 패턴이다.  
`역할 분담`을 통해 -> <u>각 코드의 존재 의의를 명확히</u> 할 수 있다.  
코드들이 어떤 역할을 맡아야 하는지 `명료해진다는 건 불필요한 코드가 줄어든다`는 뜻이다.  
이러한 효과는 유지 보수 및 확장의 용이함 && 중복 코드 제거로 이어진다.  
이를 <span style="color:red">관심사의 분리</span>(`SoC`, Seperation of Concern)라고도 한다. 
컨베이어 벨트에서 각 직원이 자기에게 맡겨진 업무만을 반복적으로 수행할 수 있도록 분업화된 공장을 연상시킬 수 있다.  

> <span style="color:red">관심사 분리</span>로 `코드의 단순화` 및 `유지보수`의 더 <span style="color:blue">높은 수준의 자유</span>가 생긴다.  
관심사가 잘 분리될 때 독립적인 개발과 업그레이드 외에도 모듈 재사용을 위한 더 높은 정도의 자유가 있다.  

<img src="https://user-images.githubusercontent.com/87808288/163680209-f60b7322-f6ca-451f-a032-2d87f8e75762.png" width="800" height="500">   

|View|Controller|Model|
|:---|:---|:---|
|- <span style="color:blue">브라우저 화면</span>|- 특정 동작에 따라 <u>Model과 View를 조작</u>|- `정보`, `데이터`|
|- 사용자 인터페이스 요소|- 변경을 일으키기 위해 <u>Model과 View를 모니터링</u>|- React의 경우 <span style="color:red">state</span>|
|- <u>Controller에 변경을 통지</u>|- <span style="color:red">이벤트를 감지하고 처리</span>하는 역할||  

[기술적 한계]  
모든 개념들이 그러하듯이 MVC와 같은 패턴도 항상 옳다고 할 수 없다.  
기술을 사용할 때는 <span style="color:red">한계</span> 또한 명확히 인지하고 있어야 한다.  
- Controller -> Model -> View 눈사태  
<img src="https://user-images.githubusercontent.com/87808288/163680568-29d9abb0-1145-4946-b22b-65c133efc1c9.png" width="700" height="300">  
위의 그름은 Controller가 여러 모델에 걸쳐 데이터를 조작하고 있는 상황을 나타낸 것이다.  
Model은 여러 View를 업데이트하고 -> <u>View 또한 Controller를 통해 Model을 업데이트</u>한다.  
(<span style="color:blue">양반향 바인딩</span> Two-Way Binding)    
컨트롤러가 일으킨 조작이 정확히 어떤 요소들에 대한 업데이트를 일으켰는지 파악하기 어렵다.   

## Flux  
<u>Front-end 기술의 발달</u>로 웹 애플리케이션이 고도화되면서 -> **규모에 맞는 안정적인 상태 관리 패턴**이 필요해졌고  
Flux 패턴은 애플리케이션의 이러한 예측 불가능성을 해결하고자 했다.  

### Flux란?  
Flux는 Facebook에서 클라이언트-사이드 웹 어플리케이션을 만들기 위해 사용하는 어플리케이션 아키텍쳐다.  
<span style="color:red">단방향 데이터 흐름</span>을 활용해 View 컴포넌트를 구성하는 `React를 보완`하는 역할을 한다.  
이전까지의 프레임워크와는 달리 패턴과 같은 모습을 하고 있기 때문에 수많은 새로운 코드를 작성할 필요 없이 바로 Flux를 사용할 수 있다.  

### Flux의 구성  
Flux 어플리케이션은 `Dispatcher`, `Stores`, `Views`(React Component) 이렇게 <u>세가지 부분으로 구성</u>된다.  
(Model, View, Controller와 혼동해서는 안된다!)  
Controller도 물론 Flux 어플리케이션에 존재하지만 -> <u>Controller-Views-Views</u> 관계로 존재하고 있다.  
이 <span style="color:blue">Controller-Views</span>는 <u>Stores에서 데이터를 가져와</u> 그 데이터를 <span style="color:blue">자식에게 보내는 역할</span>을 한다.  
더불어 dispatcher를 돕는 action creator 메소드는 이 어플리케이션에서 가능한 모든 변화를 표현하는  
유의적 API를 지원하는데 사용된다. -> Flux 업데이트 주기의 4번째 부분이라고 할 수 있다.  

[<span style="color:red">단방향 데이터</span>]  
Flux는 MVC와 다르게 <u>단방향으로 데이터가 흐른다</u>.  
`React view`에서 사용자가 상호작용을 할 때, 그 View는 <u>중앙의 Dispatcher를 통해 action을 전파</u>하게 된다.  
어플리케이션의 데이터와 비지니스 로직을 가지고 있는 Store는 action이 전파되면 이 action에 영향이 있는   
모든 View를 갱신한다.  
이 방식은 특히 React의 선언형 프로그래밍 스타일 즉, View가 어떤 방식으로 갱신해야 되는지 일일이 작성하지  
않고서도 데이터를 변경할 수 있는 형태에서 편리하다.  

이 프로젝트는 파생되는 데이터를 올바르게 다루기 위해 시작되었다.  
예를 들어 현재 뷰에서 읽지 않은 메시지가 강조되어 있으면서도 읽지 않은 메시지 수를 상단 바에 표시하고 싶었다.  
이런 부분은 MVC에서 다루기 어려운데 메시지를 읽기 위한 단일 스레드에서 메시지 스레드 모델을 갱신해야하고  
동시에 읽지 않은 메시지 모델을 갱신해야하기 때문이다.  
대형 MVC 어플리케이션에서 종종 나타나는 데이터 간의 의존성과 연쇄적인 갱신은 뒤얽힌 데이터 흐름을 만들고  
예측할 수 없는 결과로 이끌게 된다.  

Flux는 `Store를 이용해` 제어를 뒤집었다. 일관성을 유지한다는 명목으로 외부의 갱신에 의존하는 방식과 달리  
<u>Store는 갱신을 받아들이고 적절하게 조화</u>한다.  
Store 바깥에 아무것도 두지 않는 방식으로 데이터의 도메인을 관리해야 할 필요가 없어져 외부의 갱신에 따른  
문제를 명확하게 분리할 수 있도록 돕는다.  
**Store는 독립적인 세계를** 가지고 있어 setAsRead()와 같은 직접적인 setter 메소드가 없는 대신  
Dispatcher에 등록한 콜백을 통해 데이터를 받게 된다.  

### Flux의 구조와 데이터 흐름  
Flux 어플리케이션에서의 <span style="color:blue">데이터는 단뱡향</span>으로 흐른다.   
<img src="https://user-images.githubusercontent.com/87808288/163743763-b253c43c-2cd4-4d4b-95b3-c21b29149164.png" width="600" heigh="300">   
<span style="color:red">단방향 데이터 흐름</span>은 <u>Flux 패턴의 핵심</u>인데 위의 사진에서 `Flux 프로그래머를 위한 제일의 멘탈 모델`이 된다.  
Dispatcher, Store와 View는 독립적인 노드로 <u>입력과 출력이 완전히 구분</u>된다.  
Action은 새로운 데이터를 포함하고 있는 간단한 객체로 type 프로퍼티로 구분할 수 있다.  
View는 사용자의 상호작용에 응답하기 위해 새로운 Action을 만들어 시스템에 전파한다.  
<img src="https://user-images.githubusercontent.com/87808288/163744080-3b5bb7d7-dcb0-41dd-b779-1974ac1cf029.png" width="600" height="300">   
<u>모든 데이터는 중앙 허브</u>인 `Dispatcher`를 통해 흐른다.  
Action은 Dispatcher에게 Action Creator 메소드를 제공하는데 <u>대부분의 Action</u>은 <span style="color:blue">View에서의 사용자  
상호작용에서 발생</span>한다.  
Dispatcher는 Store를 등록하기 위한 콜백을 실행한 이후에 Action을 모든 Store로 전달한다.  
등록된 콜백을 활용해 Store는 관리하고 있는 상태 중 어떤 액션이라도 관련이 있다면 전달해준다.  
Store는 change 이벤트를 Controller-Views에게 알려주고 -> 그 결과로 데이터 계층에서의 변화가 일어난다.  
Controller-Views는 이 이벤트를 듣고 있다가 이벤트 핸들러가 있는 Store에서 데이터를 다시 가져온다.  
Controller-Views는 스스로의 setState() 메소드를 호출하고 컴포넌트 트리에 속해 있는  
자식 노드 모두를 다시 렌더링하게 한다.  
Action Creator는 라이브러리에서 제공하는 도움 메소드로 메소드 파라미터에서 Action을 생성하고 type을  
설정하거나 Dispatcher에게 제공하는 역할을 한다.  
<u>모든 Action</u>은 <span style="color:blue">Store가 Dispatcher에 등록해둔 callback</span>을 통해 `모든 Store에 전송`된다.  
Action에 대한 응답으로 Store가 스스로 갱신을 한 다음에는 <u>자신이 변경되었다고 모두에게 알린다</u>.  
Controller-View라고 불리는 특별한 View가 변경 이벤트를 듣고 새로운 데이터를 Store에서 가져온 후   
모든 트리에 있느 자식 View에게 세로운 데이터를 제공한다.  

어플리케이션의 상태는 Store에 의해서 관리되고 어플리케이션의 다른 부분과는 완전히 분리된 상태로 남는다.  
두 Store 사이에 의존성이 나타나도 둘은 엄격하게 위계가 관리되어 Dispatcher에 의해 동기적으로 변경되는  
방법으로 관리된다.  

#### 단일 Dispatcher  
Dispatcher는 Flux 어플리케이션의 중앙 허브로 -> <span style="color:blue">모든 데이터의 흐름을 관리</span>한다.  
<u>본질적으로 Store의 콜백을 등록하는데</u> 쓰이고 Action을 Store에 배분해주는 간단한 작동 방식이다.  
Action Creator가 새로운 Action이 있다고 Dispatcher에게 알려주면 어플리케이션에 있는 모든 Store는  
해당 Action을 앞서 등록한 Callback으로 전달받는다.  
어플리케이션의 규모가 커지면 Dispacher의 역할은 더욱 필수적이다.  
바로 <span style="color:blue">Store 간에 의존성</span>을 `특정적인 순서로 Callback을 실행하는 과정으로 관리`하기 때문이다.  
<u>Store는 다른 Store의 업데이트가 끝날 때까지 선언적으로 기다릴 수 있고</u> 끝나는 순서에 따라 스스로 갱신된다.  

#### Stores  
Store는 어플리케이션의 <u>상태와 로직을 포함</u>하고 있다.  
Store의 역할은 전통적인 <u>MVC의 Model과 비슷</u>하지만 많은 객체의 상태를 관리할 수 있는데  
ORM 모델이 하는 것처럼 단일 레코드의 데이터를 표현하는 것도 아니고 Backbone의 컬랙션과도 다르다.  
Store는 단순히 ORM 스타일의 객체 컬랙션을 관리하는 것을 넘어 어플리케이션 내의 <span style="color:blue">개별적인  
도메인에서 어플리케이션의 상태를 관리</span>한다.  
위에서 언급한 것과 같이 <u>store는 자신을 Dispatcher에 등록하고 Callback을 제공</u>한다.  
이 Callback은 Action을 파라미터로 받는다. Store에 등록된 Callback의 내부에서는 Switch문을 사용한  
Action 타입을 활용해서 Action을 해석하고 Store 내부 메소드에 적절하게 연결될 수 있는 훅을 제공한다.  
여기서 결과적으로 <u>Action은 Dispatcher를 통해 Store의 상태를 갱신</u>한다.  
Store가 업데이트된 후, 상태가 변경되었다는 이벤트를 중계하는 과정으로 View에게 새로운 상태를 보여주고  
View 스스로 업데이트하게 만든다.  

#### Views와 Controller-Views  
Store에서 이벤트를 받으면 Store의 퍼블릭 getter 메소드를 통해 새로 필요한 데이터를 처음으로 요청하게 된다.  
그 과정에서 setState() 또는 forceUpdate() 메소드를 호출하게 되고 그 호출 과정에서  
자체의 render() 메소드와 하위 모든 자식의 render() 메소드를 실행한다.  

전체적인 Store의 상태를 단일 객체로 만들어 하위에 있는 View에 전달하게 되는데 다른 자식들도 필요한  
부분이라면 데이터를 사용할 수 있도록 한다.  
또한 Controller-View는 위계의 최상위에서 마치 Controller와 같은 역할을 지속적으로 수행해  
하위에 있는 View가 가능한 한 순수하게, 함수적으로 유지될 수 있도록 한다.  
또한 Store의 전체 상태를 단일 객체로 흘려 보내는데 이 방식은 관리해야 하는 프로퍼티 수를 줄이는 효과도 있다.  

내부에 Controller-View를 추가하는 것을 결정할 때에는 여러 데이터 업데이트의 흐름이  
위계와 다른 방향으로 흐르지 않도록 고려해 단순함의 균형을 유지해야한다.  
여러 데이터가 업데이트 되면 이상한 효과를 만들어 React의 렌더링 메소드가 다른 Controller-View에 의해  
반복적으로 실행되서 디버깅의 어려움을 가중할 가능성이 있다.  
내부 Controller-View를 만드는 것을 결정할 때, 데이터를 갱신하기 위해 위계에서 여러 방향으로  
흐르는 복잡성에 반해 단순한 컴포넌트의 이점에서 균형을 찾아야 한다.  
여러 방향으로의 데이터 갱신은 이상한 효과를 만들 수 있다.  

#### Actions  
Dispatcher는 Action을 호출해 데이터를 불러오고 Store로 전달할 수 있도록 메소드를 제공한다.  
Action의 생성은 Dispatcher로 Action을 보낼 때 의미있는 헬퍼 메소드로 포개진다.  

Action은 서버와 같은 다른 장소에서 올 수 있다.  
예를 들면 Data를 초기화할 때 이런 과정이 발생할 수 있다.  
또한 서버에서 에러 코드를 반환하거나 어플리케이션이 제공된 후에 업데이트가 있을 때 나타날 수 있다.  




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
