# Refactoring 해가며 완성하는 NodeJS 블로그 포스팅 서비스

## Version

node v14.18.1   
npm v6.14.15   
<br>

----------
<br>

## commit 내용
<br>

### 1. [environment settings (about formatting and linting)](https://github.com/b00db/BLOG-POSTING-SERVICE/commit/3f54f2def408f7d8b156984c28a1da6adbc21ce5)

프로젝트를 만들고 환경을 설정하는 단계입니다.   
Formatting을 위해 Prettier를, Linting을 위해 eslint를, Type Checking을 위해 typescript를 devDependencies로 설치하고 각각을 사용하기 위해 추가 파일을 만들어 설정을 완료하였습니다.
<br>

```
Formatting?
   
: 사용자가 지정한 옵션에 따라 코드스타일을 자동으로 정렬해줍니다.
```

```
Linting?
   
: 자바스크립트 문법에서 에러를 표시해줍니다. 에러의 기준을 직접 설정할 수 있습니다.
문법적인 오류만을 잡아낼 수도 있지만, 세미콜론(;) 사용과 같은 전반적인 코딩 스타일을 정해둘 수도 있습니다.  
```

```
왜?

: 개발자마다 코드 스타일이 다른 것을 극복하여 협업을 편리하게 하기 위해 사용합니다.
하나의 공통화된 코드 스타일을 사용하여 유지보수 및 협업을 편리하게 만들어줍니다.
```

<br>

### 2. [Create RESTful API using NO FRAMEWORK and NO DATABASE](https://github.com/b00db/BLOG-POSTING-SERVICE/commit/a3bce88386ddaf20313f5fa33970805dcdf7d2b8)

어떠한 프레임워크의 도움없이 아래의 3가지 SERVER RESTful API를 만들었습니다. 프레임워크를 사용하지 않고 조건문으로 분기를 처리하였습니다. URL 인자는 정규식을 활용해 추출하여 사용하였습니다. 또한, 개발 과정에서 JSDoc을 이용하여 타입 세이프티를 하였습니다. 서버 포트는 localhost 4000번 포트를 사용하였습니다.

```
GET /posts  
: 모든 게시글 조회 API
```     
``` 
GET /posts/:id   
: 하나의 게시글 조회 API
```   
``` 
POST /posts   
: 게시글 작성 API   
```

추가적인 툴로 HTTPie를 사용하여 테스팅 완료하였습니다.   
<br>

```
정규표현식(Regular Expression: Regex)? 

: 특정 패턴의 문자열을 찾거나 대체 또는 발췌하기 위한 표현 방식입니다. 
(발췌는 ```(): 캡처``` 패턴을 사용하여 괄호 안에 있는 표현식을 캡처하여 사용합니다.)
```

``` 
JSDoc?   

: 자바스크립트 API 문서 생성기입니다. 
자바스크립트 코드에 JSDoc 형식의 주석을 추가하면 API를 설명하는 HTML 문서를 생성할 수 있습니다. 
(JSDoc 주석은 '/** ... */' 사이에 기술합니다. 일반적인 자바스크립트 주석 '/* ... */' 은 무시됩니다.)
```

<br>

### 3. [Separate main.js with api.js for Separating API Server.](https://github.com/b00db/BLOG-POSTING-SERVICE/commit/f0bf2a88fa2961167b8e7ede27a2218dc5e13c49)

중복된 코드를 하나의 로직으로 추상화하는 단계입니다.   
기존의 if 분기문에서의 공통된 로직은 다음과 같습니다.

```
- statusCode 값을 할당받습니다.
- http body (response body) 값을 전달합니다.
```

또한, 기존 코드는 위의 공통된 로직이 없어도 런타임 전에 에러를 나타내지 않습니다.
추상화 단계에서 함수로 인자를 설정해두거나 타입 정의를 하여 타입 체크 진행하는 방식으로 로직을 묶어서, 런타임에 가지 않더라도 오류를 알 수 있도록 코드를 리팩토링(Refactoring) 하는 것이 가독성과 유지보수성에 유리합니다.