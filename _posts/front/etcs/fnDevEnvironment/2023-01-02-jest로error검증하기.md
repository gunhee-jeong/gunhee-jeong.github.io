---
layout: single
title: "Jest로 error 검증하기"
# categories: Git
categories:
  - feDevEnvironment # HTML CSS JavaScript Server Algorithm Wecodes Programmers CS Github Blog
tag: [Jest, 테스트 코드, TDD] #tag는 여러개 가능함
toc: true #table of content 기능!
toc_sticky: true
author_profile: true #blog 글안에서는 author_profile이 따라다니지 않도록 설정함
date: 2023-01-02
last_modified_at: 2023-01-12
# sidebar:
# nav: "docs" #네비게이션에 있는 docs를 의미함
---

✏️ 글의 목적: 아이디와 비밀번호를 POST 요청 보내고, 정보가 맞지 않을 경우 error를 throw 하는 테스트 코드를 만들어 보았다. 처음 만들다 보니 고생을 며칠 했다. 다음에도 이러한 postLogin() 함수의 테스트 코드를 만들 나를 위해, 그리고 다른 개발자를 위하여 정보를 제공하고자 한다.

```jsx
// api.test.js
import {
  postLogin,
} from './api';

import LOGINTOKENS from '../../fixtures/loginTokens';
import LOGINFAILDATA from '../../fixtures/loginFailData';

describe('api', () => {
  const mockFetch = (data) => {
    global.fetch = jest.fn().mockResolvedValue({
      async json() { return data; },
    });
  };

  describe('postLogin', () => {
    beforeEach(() => {
      mockFetch(LOGINTOKENS);
    });

    it('returns loginTokens', async () => {
      const data = await postLogin({
        email: '',
        password: '',
      });

      expect(data).toEqual(LOGINTOKENS);
    });

    context('when login fails', () => {
      beforeEach(() => {
        mockFetch(LOGINFAILDATA);
      });

      it('throw an error', async () => {
        try {
          await postLogin({
            email: 'tester@example.com',
            password: '',
          });
        } catch (e) {
          expect(e.message).toBe('INVALID_PASSWORD');
        }
      });
    });
  });
});
```

*위의 코드와 같이 it을 작성하면* `api.js에서 try …catch 구조를 사용하지 않아도` 위의 테스트에서는 정상적으로 통과했다고 테스트를 완료한다. **나는 아직 api.js의 postLogin() 함수에서 try …catch 구조를 사용하지도 않았는데 테스트가 정상적으로 수행만 돼버려도 해당 테스트를 통과**하게 되는 것이다.(거짓으로 테스트를 통과한 것이다🥹) 이를 바로잡기 위해서 아래의 코드가 필요했다.

```jsx
// api.test.js
import {
  postLogin,
} from './api';

import LOGINTOKENS from '../../fixtures/loginTokens';
import LOGINFAILDATA from '../../fixtures/loginFailData';

describe('api', () => {
  const mockFetch = (data) => {
    global.fetch = jest.fn().mockResolvedValue({
      async json() { return data; },
    });
  };

  describe('postLogin', () => {
    beforeEach(() => {
      mockFetch(LOGINTOKENS);
    });

    it('returns loginTokens', async () => {
      const data = await postLogin({
        email: '',
        password: '',
      });

      expect(data).toEqual(LOGINTOKENS);
    });

    context('when login fails', () => {
      beforeEach(() => {
        mockFetch(LOGINFAILDATA);
      });

      it('throw an error', async () => {
        let errorExcept = null;
        try {
          await postLogin({
            email: 'tester@example.com',
            password: '',
          });
        } catch (e) {
          expect(e.message).toBe('INVALID_PASSWORD');
          errorExcept = e;
        }

        expect(errorExcept).not.toBeNull();
      });
    });
  });
});
```

위의 코드에서는 *it 문 안에 errorExpect 변수를* 만들고, **catch가 실행되면** `errorExcept에 값을 재할당`하여 catch가 실행되었는지 테스트할 수 있게 된다. 

이렇게 errorExcept 변수를 선언하고 catch가 실행될 경우 값을 재할당하는 방식은 *let을 최대한 지양해서 프로젝트를 만들고 싶었던* 나의 방향과는 맞지 않았다. 그리고 postLogin() 함수를 테스트하기 위해 *기존의 코드와 관계없는 부가적인 변수를 선언하는 것도* 조금은 아쉬움이 생겼다.

그러다가 이동욱 님이 작성하신 블로그 글을 발견하게 되었고, 여기서 더 나은 방법을 찾을 수 있었다. 그것은 바로 `expect.rejects.toThrowError`를 사용하는 것이다.

💡 *이동욱님 블로그: [Jest로 Error 검증시 catch 보다는 expect](https://jojoldu.tistory.com/656)*

```jsx
// api.test.js
import {
  postLogin,
} from './api';

import LOGINTOKENS from '../../fixtures/loginTokens';
import LOGINFAILDATA from '../../fixtures/loginFailData';

describe('api', () => {
  const mockFetch = (data) => {
    global.fetch = jest.fn().mockResolvedValue({
      async json() { return data; },
    });
  };

  describe('postLogin', () => {
    beforeEach(() => {
      mockFetch(LOGINTOKENS);
    });

    it('returns loginTokens', async () => {
      const data = await postLogin({
        email: '',
        password: '',
      });

      expect(data).toEqual(LOGINTOKENS);
    });

    context('when login fails', () => {
      beforeEach(() => {
        mockFetch(LOGINFAILDATA);
      });

      it('throw an error', async () => {
        await expect(async () => {
          await postLogin({
            email: 'tester@example.com',
            password: '',
          });
        }).rejects.toThrowError(new Error('INVALID_PASSWORD'));
      });
    });
  });
});
```

expect.rejects.toThrowError() matcher를 사용하면, **비동기 함수에서 예상한 오류를 발생하는지 확인**할 수 있다. 테스트되는 함수가 *프로미스를 반환하고*, 해당 `프로미스가 reject되면 matcher가 통과`된다. 위의 실제 코드보다 조금 더 간단한 코드를 살펴보자.

```jsx
async function asyncFunction() {
  throw new Error('This is an error');
}

test('async function throws an error', async () => {
  await expect(asyncFunction()).rejects.toThrowError('This is an error');
});
```

위 예제에서 *asyncFunction()은 Error 객체를 throw* 한다. 그렇기 때문에 rejects.toThrowError() matcher를 사용하면, **예상한 메시지와 일치하는지 테스트**하게 된다.

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
 -->
