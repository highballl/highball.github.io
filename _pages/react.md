---
title: "React"
categories:
  - Frontend
tags:
  - React
  - JavaScript
  - JSX
  - Frontend
---

- 각종 에러 메시지와 해결방법
    - DevTools failed to load source map: Could not load content for chrome-extension://pgjjikdiikihdfpoppgaidccahalehjh/webspeed.js.map: HTTP error: status code 404, net::ERR_UNKNOWN_URL_SCHEME (콘솔창에서 에러, 실행도 안 됨)
        - index.js 가 비어있을 때 발생
    - Each child in a list should have a unique "key" prop
        - 목록을 for문으로 생성할 때(map등을 이용할 때) key라는 prop값을 부여해야 한다
        - 키를 세팅하지 않으면 위의 에러가 난다
        - key는 다른 것과 중복되지 않는 식별자를 써야 한다
            - 다른 엘리먼트들과 다른 UNIQUE한 string값을 부여 (.toString()이용)
            - 대부분 데이터의 id값을 key값으로 부여함
            - index를 사용하는 경우도 있음
                - 그러나 배열 내 아이템의 순서가 바뀔 수 있어서 좋지 않음
                - 성능이 저하되거나 컴포넌트의 state와 관련한 문제가 발생할 수 있으므로
                - id값을 쓰는 편이 나음
    - 'userState' is not defined no-undef
        - `import {useState} from 'react';` 추가해서 해결
    - Module not found: Can't resolve '파일경로'
        -  파일이 누락되었거나 파일 경로에 오타가 있을 경우 발생(점, 슬래시 등 체크)
    - 컴포넌트의 입력인자에 숫자를 할당하려면?
        ```jsx
        **<Profile name="AnSan" age="20" /> (o)
        <Profile name="AnSan" age={20} /> (o)
        <Profile name="AnSan" age=25 /> (x)**
        ```

# 리액트란?
- 페이스북에서 개발, 자바스크립트 라이브러리
- 동적 유저 인터페이스(UI)를 구축할 때 용이
- 현재 가장 사용자 점유율이 높음(2021년 기준)
- `**Virtual DOM**`
- `**JSX`(JavaScript eXtension, 자바스크립트 확장 문법)**를 이용
- `**컴포넌트(Component)**`를 이용하여 코드를 모듈화
- `**Hooks**`를 이용하여 컴포넌트를 쉽게 관리
- 오픈소스
- 데이터는 부모→자식 단방향으로만 전달(props 이용)

## 리액트 초기 세팅
(정리중)

## 리액트 설치 직후 초기 파일 살펴보기
### index.html
- 리액트로 만든 앱은 아무리 커도 이 root 태그 안에 들어가기로 약속한다.
- 따라서 아래 코드는 index.html에 기본적으로 포함되어야 하고, 리액트를 시작하면 파일에 기본적으로 들어가 있는 코드이기도 하다.

```html
<div id="root"></div>
```

### index.js
- 실질적인 입구역할을 하는 파일.
- src 폴더 내에 위치
- `ReactDOM.render();`
    : 해당 아이디(여기서는 root)를 가진 html태그 아래에 리액트를 렌더링 할 것이라는 의미
    : `DOM(Document Object Model)`(문서 객체 모델) - HTML 요소를 노드로 포함하는 트리 구조
- `<React.StrictMode> </React.StrictMode>`
    : 리액트 앱이 로딩되는 부분
    ```jsx
    import React from 'react';
    import ReactDOM from 'react-dom';
    import App from './App';

    ReactDOM.render(
        <React.StrictMode>
            <App />
        <React.StrictMode>
        **document.getElementById('root')**
    );
    ```

### App.js
- index.js와 마찬가지로 src 폴더 내에 위치
- App.js → index.js → index.html 흐름 정리
    → App.js의 내용 작성
    → index.js에서 임포트 
    → 위 코드에서는 App.js 내에서 정의된 function App() 부분을 임포트 하여 
    → index.js 내의 ReactDOM.render() 내부에 있는 `<App />` 
    → 'root' 태그를 가진 html에 전달되어 
    → index.html의 <div id='root'>에서 코드가 실행됨

### 기타 파일 구조
(정리중)

## 핫 리로딩
출처 : [https://reactnative.dev/blog/2016/03/24/introducing-hot-reloading](https://reactnative.dev/blog/2016/03/24/introducing-hot-reloading)
참고 : [http://daplus.net/javascript-react-native의-핫-리로딩과-라이브-리로딩의-차이점은-무/](http://daplus.net/javascript-react-native%EC%9D%98-%ED%95%AB-%EB%A6%AC%EB%A1%9C%EB%94%A9%EA%B3%BC-%EB%9D%BC%EC%9D%B4%EB%B8%8C-%EB%A6%AC%EB%A1%9C%EB%94%A9%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80-%EB%AC%B4/)
React-Native 앱을 개발하는 동안 코드 변경 사항을보고 코드 변경 사항을 보려면 React-Native에 두 가지 옵션이 있습니다.
1. 핫 리로드
    핫 리로드는 앱을 처음부터 다시 시작하지 않고 새로운 코드 변경에 따른 코드 변경 사항 만 표시하며 변경된 코드에만 적용됩니다.
2. 라이브 리로드
    때로는 탐색과 같은 코드를 테스트하기 위해 Live Reload가 필요할 수 있으므로 Live reload는 이 경우 유용하므로 코드 변경시 전체 응용 프로그램을 다시로드합니다.

# JSX
[변수](https://www.notion.so/388bcb2fe1e44d78920127ef22cc5272)
- **`React.createElement()`**
    - 코드틀
        ```jsx
        const element = React.createElement(
        		'div', // Tag name
        		{className: show}, // Class name
        		'hi!' // Content
        );
        // 위 아래는 같은 코드
        const element = <div className="show">hi!</div>
        ```
    - JSX 문법을 이용하지 않고 element를 객체로 표현할 수 있음
    - HTML element를 생성하여 객체로 반환
    - 엘리먼트는 한번 생성하고 나면 수정이 불가능한 객체(const element...)
        ⇒ 값 변경을 위해서는 계속 새 엘리먼트를 만들어서 업데이트 해야 함
        ⇒ setInterval()을 이용해서 tick을 지속적으로 하여 해결할 수 있음
        - 코드 작동 순서 : 버튼 클릭 시 클릭 횟수 증가하여 반환하는 예제
            ⇒ setInterval(tick, 1000), function tick 호출
            ⇒ button onClick={click}, function click 호출
            ⇒ value = value + 1하여 반환
            ⇒ function tick의 element 내부에서 {value}값 업데이트
            ⇒ ReactDOM.render(element, document.getElementById('root');에서 element를 렌더링
        ```jsx
        import React from 'react';
        import ReactDOM from 'react-dom';
        import './index.css';
        import App from './App';
        import * as serviceWorker from './serviceWorker';

        //클릭 횟수 저장 변수
        let value = 0

        //클릭 횟수 증가 함수
        function click() {
          value=value+1;
        }

        //엘리먼트 업데이트 & 렌더링 함수
        function tick(){
          const element = (
            <div>
              <h1>버튼을 클릭해보세요</h1>
              <button onClick={click}>Click Me!</button>
              <h2>총 {value}번 클릭했습니다.</h2>
            </div>
          );
          
          ReactDOM.render(element,document.getElementById('root'));
        }

        //1초마다 tick()함수 호출
        setInterval(tick, 1000);

        serviceWorker.unregister();
        ```

- JSX 표현식
    - 코드 틀
        ```jsx
        // variable
        const name = "AnSan";
        const element = <h1> Hi, {name}</h1>;

        // function
        function article(){
        	return "Hello World!"
        }
        const element = <h2>{article()}</h2>;

        // function with argument
        function bookInfo(book)
        	return book.title + ' ' + book.author;

        const book = {
        	title = 'One Piece'
        	author = 'Oda Aiichiro'
        }

        function printInfo(book){
        	return <p>This is {bookInfo(book)}.</p>;
        }

        const element = article(book);
        ReactDOM.render(element, document.getElementById('root')); 
        ```

## 주의사항
- HTML을 JSX로 변환할 때, 변수 내에 HTML코드를 저장하기
- 최상단 element는 반드시 하나
    - 여러 자식 태그로 구성된 HTML 코드는 반드시 부모 태그 내에 구성하기
    - 부모 태그처럼 <>, </>를 쓸 수도 있음
- 문장의 끝은 세미콜론(**`;`**)을 사용하기
- 닫는 태그를 필수로 작성해야 함
- class대신 className 사용
- 인라인 스타일 정의
    참고 : https://www.w3schools.com/react/react_css.asp
    : CSS 속성명은 camel case로 작성
    : "color: red;" (x) - 문자열 안됨!
    : 세미콜론 대신 콤마를 사용할 것
    : { { } } (o) 
    → 바깥쪽 중괄호는 HTML태그 내에서 자바스크립트를 사용하겠다는 선언에 해당
    → 안쪽 중괄호가 내용을 담은 **객체**에 해당
    ```jsx
    import React from 'react';
    import './App.css';

    function App() {
      return (
        <div className="App">
            **<div style={{
                padding: 48, 
                color:"red",
                backgroundColor:"blue", 
            }}>**안녕하세요.</div>
        </div>
      );
    }

    export default App;
    ```

### 객체(Object)
- 데이터를 모아 묶은 것
    { id: 1, title: 'html', description: 'html is ...'}
- 파이썬의 딕셔너리와 비슷하다고 이해
- 배열에는 데이터가 순서대로 담기지만, 객체는 데이터가 이름을 갖고 저장됨



# 컴포넌트
- 일종의 사용자 정의 태그
- 코드의 재사용성 증대, 복잡한 코드를 부품으로 만들 수 있음
- 첫글자는 대문자로 시작
- 모든 태그는 닫는 태그가 있어야 하며, 축약표현도 사용 가능 (<></>, <NavTag />)

### 컴포넌트가 사용된 기본 코드
```jsx
import logo from './logo.svg';
import './App.css';

function HeaderTag(){
  return (
    <header>
      <h1>
        <a href="index.html">WEB</a>
      </h1>
    </header>
  )
}

function NavTag(){
  return (
  <nav>
    <ul>
      <li><a href="1.html">html</a></li>
      <li><a href="2.html">css</a></li>
    </ul>
  </nav>
  )
}

function ArticleTag(){
  return (  
  <article>
    <h2>Welcome</h2>
        Hello, WEB
    </article>
  )
}

function App() {
  return (
    <div className="App">
      <HeaderTag />
      <NavTag />
      <ArticleTag />
    </div>
  );
}

export default App;
```

### 속성(props)을 통해 컴포넌트에서 컴포넌트로 입력값 전달하기(1)
- Props : 컴포넌트로 값을 전달하는 매개변수
- 함수컴포넌트에서:
    `function 함수이름(props){ 함수내용 }` 와 같이 쓴다. 입력인자 자리에 props가 들어감
- 클래스 컴포넌트에서:
    입력인자 자리가 없는 대신 코드에서  `this.props` 또는 `this.props.name`과 같은 매개변수를 쓴다. (`this.props.속성`)
```jsx
function ArticleTag(props){
  console.log('props', props); //props가 담고 있는 내용을 콘솔에서 확인해보자
  return (  
  <article>
    <h2>Welcome</h2>
        Hello, WEB
    </article>
  )
}

function App() {
  return (
    <div className="App">
      <HeaderTag />
      <NavTag />
      <ArticleTag title="Welcome" description="Hello, WEB"/>
    </div>
  );
}
```

- {props}, {props.title}, {props.description} 과 같은 컴포넌트가 만들어짐
- 사용자 정의 태그로 사용하고 있음
```jsx
import logo from './logo.svg';
import './App.css';

function HeaderTag(){
  return (
    <header>
      <h1>
        <a href="index.html">WEB</a>
      </h1>
    </header>
  )
}

function NavTag(){
  return (
  <nav>
    <ul>
      <li><a href="1.html">html</a></li>
      <li><a href="2.html">css</a></li>
    </ul>
  </nav>
  )
}

f**unction ArticleTag(props){
  console.log('props', props.title);
  return (  
  <article>
    <h2>{props.title}</h2>
        {props.description}
    </article>
  )
}**

function App() {
  return (
    <div className="App">
      <HeaderTag />
      <NavTag />
      **<ArticleTag title="Welcome" description="Hello, WEB"/>
      <ArticleTag title="Hi" description="Hello, React"/>**
    </div>
  );
}

export default App;
```

### 속성(props)을 통해 컴포넌트에서 컴포넌트로 입력값 전달하기(2)
- props는 JSX attribute를 단일 object의 형태로 컴포넌트에 전달
- props는 구조분해할당destructing해서도 사용
```jsx
// props에 속성 1개 전달
function App(){
	return (
		<Welcome name="Elice" />
	);
}

function Welcome(props){
	return <div>Hello my name is {props.name}</div>
}
```

```jsx
// props에 속성 2개 전달
function App(){
	return (
		<Welcome name="Elice" age="12" />
	);
}

function Welcome(props){
	return <div>Hello my name is {props.name}, I'm {props.age} years old!</div>;
}
```

```jsx
// props에 속성 여러개 전달
function App(){
	return (
		<Welcome name="Elice" age="12" />
	);
}

function Welcome({name,age}){ // object destructuring assignment
	return <div>Hello my name is {name}, I'm {age} years old!</div>;
}
```

## 함수 컴포넌트(Function Component)
- JSX를 return
- Hooks 사용 가능, state 사용 불가능
- 코드 기본 틀
    ```jsx
    import React from 'react';
    // 함수는 클래스가 아니므로 상속 개념은 아니지만 
    // 여기서 임포트가 필요한 이유는
    // return 내부가 JSX 반환하는 것이라고 코드가 이해해야 해서 필요

    function Header(){
    	**return (
    		<div> Hello </div>; // JSX 반환 부분
    	)**
    }
    ```

- 함수 컴포넌트 정의 방법

    1) 컴포넌트 정의(대문자로 시작할 것)

    2) 컴포넌트 호출

    3) ReactDOM에 렌더링

    ```jsx
    /* ver 1 */
    import React from 'react';
    // JSX를 쓰기 위한 세팅

    //함수 컴포넌트 작성
    function Hello() {
      return <h1>Hello, React!</h1>;
    }

    //컴포넌트 호출
    const element = <Hello/>;

    //렌더링
    ReactDOM.render(element, document.getElementById('root'));
    Copy

    /* ver 2 - Welcome.js */
    import React from 'react';

    function Welcome(){
        const name = "Sara";
        return (
            // JSX 반환 부분
            <h2>Welcome, {name}</h2>
        
        )
    };

    export default Welcome;
    // App.js에서 쓸 수 있도록 해주는 부분
    // 정확히는 Welcome이라는 함수를 다른 파일에서 쓸 수 있게 해주겠다고 설명하는 거 같음

    /* ver2 - Welcome.js를 임포트 할 App.js */
    import React from 'react';
    import './App.css';
    **import welcome from './components/Welcome';
    // Welcome을 임포트해서 사용하기**

    function App() {
      return (
        <div className="App">
            **<Welcome />
    				/**/Welcome 컴포넌트 사용하기
        </div>
      );
    }

    export default App;
    // App도 어디선가 다른데에서 사용할 수 있게 해줬다
    // index.js를 보면 거기서 쓰고 있다(렌더링하고 있음)
    ```

## 클래스 컴포넌트(Class Component)
공식문서 : [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)
- state 관련 기능 사용 가능
- 코드 기본 틀
    ```jsx
    **import React from 'react';**
    // 여기서는 Header 클래스가 React.Component를 상속하니까 임포트를 해야 함

    class Header **extends React.Component**{
    	**render()**{ //render() 메서드를 클래스 메서드로 포함해야 함
    		return (
    			//JSX 반환부분
    			<div> Hello </div>
    		)
    	}
    }
    ```

- 코드 예제
    - Welcome.js
        ```jsx
        import React from 'react';

        **const name = 'Sara';
        class Welcome extends React.Component{**
        	
        	**render(){
        		return(**
        			<div>Welcome, {name}</div>
        		**)
        	}
        }**

        export default Welcome;
        ```
    - App.js

        ```jsx
        import Rreact from 'react';
        import './App.css';
        import Welcome from './components/Welcome';

        function App(){
        	return (
        		<Welcome />
         )
        }

        export default App;
        ```


# 문법
### 몇가지 유용한 내장 메서드
- `parseInt(문자열, 진법)` : 문자열을 해당 진법에 맞는 숫자로 변환
- `###.length`
- `###.value`
- `###.textContent`


### 리액트에서 함수를 호출하기
- 컴포넌트에서 함수를 바로 호출하지 않는다. 직접 다른 함수를 호출하지 않는다.
```jsx
function HeaderTag(props){

  debugger;
  **console.log('Header', props);**

  **function onClickHandler(){
    props.onChangeMode();** 
    // props의 onChangeMode 호출(불러오기)
    // function App()에서 onChangeMode는 onChangeModeHandler 함수를 호출하고 있다
    // function App()의 코드 : onChangeMode={onChangeModeHandler}
  }

  return (
    <header>
      <h1>
        <a href="index.html" onClick={onClickHandler}>{props.title}</a>
      </h1>
    </header>
  )
}
```

### this
- 자기 자신의 상위 객체를 의미
- 화살표 함수(Arrow Function)에서는 this를 사용할 수 없음

### 화살표 함수(Arrow Function)
```jsx
const 함수내용을 담을 변수명 = (함수이름생략)(입력인자) => 인자.메서드;
const 변수명 = (입력인자) => 다른함수(입력인자);
//map 응용
const poweredArray = arrayA.map(el => pow(el));
```
- 익명함수
- 재사용하지 않을 때 사용 - 1회용
    ⇒ 하지만 변수에 대입을 하면 일반 함수처럼 재사용 가능
- map, forEach 문 등에서 사용
- 화살표 함수 내용에 리턴문만 한 줄이 존재한다면 return, 중괄호 모두 생략 가능
    ```jsx
    const element = (array) => array.length;

    /*
    동일한 코드
    const element = (array) {
    	return array.length;
    }
    */
    ```
- 함수의 입력인자가 하나이면 주변 괄호도 생략 가능
    ```jsx
    const element = **array** => array.length;
    ```
참고 : [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)


### map(내장함수)
```jsx
function NavTag(props){
  var d = props.data;
  return(
    <nav>
      <ul>
				{d.map((e)=><li><a href={e.id}>{e.title}</a></li>)}
      </ul>
    </nav>
  )
}
```

### forEach
- 배열의 메서드
- 각 요소를 한번씩 순서대로 호출
- forEach내에 들어가는 함수로는 보통 화살표 함수를 사용
```jsx
// 예제1
const arrayA = [1,2,3];
/* arrayA의 요소들이 각각 element에 한 번씩 대입됩니다.
   그 후 각 요소들이 console.log를 통해 콘솔에 찍힙니다. */
arrayA.foreEach(element => console.log(element));

// 예제2
const pow = a*a;
arrayA.forEach(el=>console.log(pow(el));
//el = elements, e도 되고 el도 되고 element도 되고...
```

### 구조분해할당(Destructuring)
(정리중)


### 세 점 표기법(Three dots Expression)
- 나머지 표기법(Rest Expression)
    - 구조 분해 할당 후 남은 값을 가져올 때 사용
    - 해당 대상이 없으면 빈 배열 또는 빈 객체가 할당됨
    ```jsx
    const [a, b, ...rest] = [10, 20, 30, 40, 50];
    // three dots expression

    console.log(rest);
    // expected output: Array [30,40,50]

    const obj = {
    	d: '1',
    	e: '2',
    	f: '3',
    	g: '4',
    };

    const {d,e,...restObj} = obj;

    console.log(restObj);
    // expected output : Object { f: '3', g: '4' }

    // const [a, b, c, ...restList] = [10, 20, 30, 40, 50]
    // 어차피 안 쓸 변수에 메모리 할당을 하면 메모리 낭비니까 아래처럼 쓰자
    const [, , , ...restList] = [10, 20, 30, 40, 50]**
    console.log(restList)
    // output : [40, 50]
    ```

- 전개 표기법(Spread Expression)
    - 원소 나열할 때 사용
    - 객체에서도 사용가능
    - 단, 객체에서는 같은 키가 존재한다면 나중에 쓴 내용으로 덮어쓰기 됨
    ```jsx
    let res = [1, 2, 3];

    const arrayA = [...res, ...res]

    console.log(arrayA);
    // expected output : Array [1, 2, 3, 1, 2, 3]

    res = [...res, 4]

    console.log(res)
    // expected output : Array [1, 2, 3, 4]

    let obj = {
    	a: '1',
    	b: '2',
    	c: '3',
    }

    const copiedObj = { ...obj, d:'4' }

    console.log(copiedObj);
    // expected output : Object { a: '1', b: '2', c: '3', d: '4'}

    const newObj = {...obj, c:'4'}

    console.log(newObj);
    // expected output : Object { a: '1', b: '2', c: '4'}

    let res = [1, 2, 3];
    **res = [...res, 4];
    // expected output : [1, 2, 3, 4]**

    let obj = {
    	a: '1',
    	b: '2',
    	c: '3',
    }

    const newObj = {...obj, a:'4', test:'test'}
    console.log(newObj)
    // expected output : {a: "4", b: "2", c: "3", test: "test"}
    ```

### Prevent Default Behavior
- 리액트는 SPA(Single Page Application?), 따라서 a태그의 기본 동작인 페이지 이동을 막는 편
- 그 때 사용하는 코드 : `functionparameter.preventDefault();`
```jsx
function onClickHandler(e){
    e.preventDefault();
    props.onChangeMode();
}
```

### State

- input의 데이터를 state를 이용해서 관리 → Controlled component
- 데이터를 필요할 때마다 element에서 가져오는 경우(리액트로 관리하지 않는 경우) → Uncontrolled component
- 함수 컴포넌트에서 사용하기 - useState
    ```jsx
    function Car(){
    	**const [favorite,setFavorite] = useState("ice cream");**

    	return(
    		<div>
    			<h1>I like {favorite}</h1>
    		</div>
    	);
    }
    ```

- 클래스 컴포넌트에서 사용하기 - constructor(props)
    ```jsx
    class Car extends React.Component{
    	**constructor(props){
    		super(props);
    		this.state = {
    			favorite: "ice cream";
    		}**
    	}

    	render(){
    		return(
    			<div>
    				<h1>I like {this.state.favorite}</h1>
    			</div>
    		);
    	}
    }
    ```

- 예제
    ⇒ HeaderTag 부분의 I love WEB 을 누르면 
    ⇒ setState가 'WELCOME'이 되고
    ⇒ if 문에 따라 mode === 'WELCOME'이면
    ⇒  title, desc가 바뀌게 되고
    ⇒  <ArticleTag title={title} description={desc}/> 부분에 자동 적용되어
    ⇒ 화면에 보이는 내용이 바뀐다
```jsx
function App() {

  **var [mode, setMode] = useState('WELCOME');
  // useState 함수에 전달한 'WELCOME'이라는 인자값은 mode의 디폴트값이 됨
  console.log('mode', mode);**

  var topics = [
    {id:1, title:'html', description:'html is . . .'},
    {id:2, title:'css', description:'css is . . .'}
  ]

  function onChangeHeaderHandler(){
      console.log('Header!!!');
      **setMode('WELCOME');**
      // mode에 맞는 기능이 실행되도록 하고 싶다.
  }

  function onChangeNavHandler(){
      console.log('onChangeMode!!!');
      **setMode('READ');**
      // mode에 맞는 기능이 실행되도록 하고 싶다.
  }

  var title; 
  var desc;
  if(mode === 'WELCOME'){
    title = 'Welcome';
    desc = 'Hello, React';
  } else if(mode === 'READ') {
    title = 'Read Mode';
    desc = 'Hello, Read';
  }

  return (
    <div className="App">
      <HeaderTag title="I love WEB" onChangeMode={onChangeHeaderHandler} />
      <NavTag data={topics} onChangeMode={onChangeNavHandler} />
      <ArticleTag title={title} description={desc} />
      <ArticleTag title={title} description={desc}/>
    </div>
  );
}

export default App;
```


### setState()
- 특정 이벤트(클릭, 마우스오버 등)로 상태가 변하는 비동기적 변경
- 클래스 컴포넌트에서 constructor 부분에서 State가 초기화 됨
- 코드 틀
    ```jsx
    class Example extends React.Component {
    	constructor(props){
    		super(props);
    		this.state  = {isToggleOn: "On"};
    	}
    	
    	isToggleOn(){
    		setTimeout( () => {this.setState( {isToggleOn: "Off"} ) }, 1000)
      }
    	
    	render() {
    		return (
    			<div>The switch is {this.state.isToggleOn}</div>
    		);
    	}
    }

    ReactDOM.render(<Example />, document.getElementById('root'));
    ```



# 이벤트
## 바인딩
- 이벤트 함수 선언시 바인딩은 필수 `.bind()`
- 단, 화살표 함수로 선언시 함수 선언과 이벤트 바인딩이 자동으로 됨
- 지역변수(this 와 같은)를 참조하기 위해서는 명시적으로 바인딩 해야 함
    - 화살표 함수에는 바인딩 불필요, 애초에 화살표 함수에는 this를 사용하지 않음
```jsx
// 예제1
class EventClass extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      message: 'Hello'
    }
    // 이벤트 바인딩
    this.handleClick = this.handleClick.bind(this);
  }
	
	handleClick() {
    this.setState({
      message: 'Goodbye!'
    })
  }

  render() {
    return (
      <div>
        <div>{this.state.message}</div>
        <button
          //{/* 이벤트와 함수를 연결하세요. */}
          onClick={this.handleClick}>
          Click
          </button>
      </div>
    )
  }
}

//예제2
class EventClass extends React.Component {
  constructor(props) {
    super(props);
    
  }

  //handleClick 이벤트 정의, 인자값을 받아 alert()을 출력
  handleClick = (data) => {
    alert(`전달받은 인자값: ${data}`)
  };

  render() {
    var data = "ABCDEFG"
    return (
      //data값을 인자값으로 제공하는 이벤트 핸들러를 작성
      <button onClick={(e) => this.handleClick(data, e)}>
        버튼을 눌러주세요!
      </button>
    );
  }
}

```


## 조건부 렌더링
- `조건 ? expr1 : expr 2`
    조건이 true인 경우 → expr 1 실행
    조건이 false인 경우 → expr 2 실행
- 



# 기타 예제 코드
- 이 함수를 통해, items state에 데이터를 추가하면 별도의 DOM 조작없이 화면에 추가 된 요소가 렌더링 됩니다.
```jsx
function GroceryList(props) {
		const [items, setItems] = useState(["Milk", "Bread", "Eggs"]);
		const [itemName, setItemName] = useState('');

    function addItem() {
       setItems([...items, itemName]);
    }
 
    return (
        <div>
            <h1>Grocery List</h1>
            <ul>
                {items.map(item => (
					        <li key={item}>{item}</li>
						    ))}
            </ul>
						<input type="text" onChange="{e => setItemName(e.target.value)}" />
						<button onClick={addItem}>Add React</button>
        </div>
    )
};
```

- React는 사용자의 입력을 기반으로 자신의 상태를 관리하고 업데이트 하는 제어 컴포넌트를 이용해 사용자 입력 시 자바스크립트 객체의 텍스트 값을 설정
- 이를 위해 먼저 상태를 정의해야 함
- 입력이 변경될 때마다 설정이 되어야 하여 HTML코드는 다소 복잡

```jsx
const [itemInput, setItemInput] = useState("");

<input type="text" placeholder="Enter an item" value={itemInput} onChange={e => setItemInput(e.target.value)}

```

- React로 업데이트하기 - 새로운 목록 추가하기
    - React 앱은 자바스크립트 변수의 전체 상태를 유지
    - 변수의 각 항목을 매핑한 후 그에 대한 목록 요소를 반환하여 JSX에 표시
    - 버튼을 누르는 기능을 정의
    - **`setItems`** 함수를 사용하여 기존 항목에 새 항목을 추가

    ⇒ 목록이 변경되었음을 자동으로 등록하고 UI를 자동으로 업데이트!

```jsx
const [items, setItems] = useState(["Milk", "Bread", "Eggs"]);

<ul>
    {items.map(item => (
        <li key={item}>{item}</li>
    ))}
</ul>

<button onClick={addItem}>Add React</button>

function addItem() { 
	console.log(itemInput); 
	setItems([...items, itemInput]); 
}

```