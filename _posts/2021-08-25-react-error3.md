---
title: "[여기에 에러를 입력] - 리액트 첫 프로젝트에서 만난 에러모음(3)"
layout: posts
permalink: /categories/:categories/:title
categories:
  - React
tags:
  - React
  - JavaScript
  - JSX
  - Frontend
#date: 2021-08-25T12:00:00
toc: true
---
`last update: 2021.08.25.WED`

# 리액트 첫 프로젝트에서 만난 에러 모음(3)    

## [여기에 에러를 입력]  

- 수정 : 지난번 [에러모음(2)](https://highballl.github.io/categories/react/react-error2)에서 반려CORS 에러 운운했는데 이번 프로젝트에 사용하는 API가 아무렇게나 뱉는 에러 메시지여서 그렇다고 한다. 원래는 헤더 수정을 하는 등 인터넷에 많이 나오는 방법대로 하면 해결이 되는 게 맞고, 이렇게 쉽게(?) 무시할 수 있는 에러도 아닌 거 같다.  
- 프로젝트 후반으로 오니 오히려 에러 메시지가 반가워졌다. 이렇다할 에러가 안 나오는데 결과 데이터가 이상하게 꼬여버리기 시작하니 뇌와 미간의 주름이 깊어지기 시작했다.  


### 1) key prop  
 
- `Warning: Each child in a list should have a unique "key" prop.`  
    - key 추가하는 걸 깜빡했다. Date.now()로 키를 바꿔봤더니, 다음 에러가 발생했다.    
- `Warning: Encountered two children with the same key, 1629775901666. Keys should be unique so that components maintain their identity across updates. Non-unique keys may cause children to be duplicated and/or omitted — the behavior is unsupported and could change in a future version.`  
    - **1629775901666**는 Date.now()로 얻은 값이다.   
    - 5개 컴포넌트에 데이터만 각기 순차적으로 다르게 하여 화면에 렌더링 하는 구조였다.   
    - 컴포넌트마다 입력 데이터도 출력 결과물도 다를테지만 키는 Date.now()로 같아져 결국 고유성을 부여하는 데에 실패했다.  
    - 순차적으로 렌더링되면서 유의미한 시차가 생길 것이라 생각했는데 그 정도가 아니었나보다. key는 다른 방식을 사용해야겠다.      
    - 참고 : [React key prop 이해하기](https://awesomezero.com/development/react-key/)   
        - 이 블로그 글을 보고 도움을 많이 받았다.   
        - 보통 key값에는 데이터의 id값을 많이 쓴다고 한다. `{data.id}`와 같은 형식으로. 이번 데이터는 그러기가 조금 애매해서 그냥 인덱스를 썼다.  
    - 참고 : [리액트 공식 문서](https://ko.reactjs.org/docs/lists-and-keys.html#keys-must-only-be-unique-among-siblings)
        - 가급적 공식 문서부터 찾자.  

<br/>

### 2) type error  

- `.map is not a function`  
    - map은 배열에만 쓸 수 있다. 객체에는 쓸 수 없다.   
    - 반환되는 자료형도 배열이다.  
    - 참고 : [javascript 공식 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)  
    - "`map()` 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다."  
- `Unhandled Rejection (TypeError): Cannot read property '1' of undefined`    
    - 말 그대로 `undefined` 상태인 데이터가 입력되어서 나는 에러메시지.   
    - 이 에러는 api 서버에서 데이터를 받아와서 가공한 뒤 상태관리 로직에 넣었다가 다시 꺼내오는 과정에서 자주 볼 수 있었다.  
    - 상태가 변하는 타이밍, 즉 함수가 호출될 타이밍을 잘못 계산한 것 같다. 어젯밤부터 다시 해결하려고 하는데 잘 안되어서 상태관리 로직 대신 일반 함수로 다시 구현하긴 했는데, 방법을 더 찾아야겠다. 
    - 상태가 변할 필요, 즉 렌더링이 더 필요한지 아닌지 더 깊게 생각해봐야겠다.          
- `typeof(blahblah) 또는 typeof blahblah` 사용하기  
    - 에러가 뜬다 싶으면 우선 지금 내가 보내고 받는 자료형이 뭔지 확인하기 시작했다.  
    - (이제서야!)   

<br/>

### 3) `no-unused-expressions`

- `Expected an assignment or function call and instead saw an expression no-unused-expressions`   
    - 참고 : [ESLint 공식 문서](https://eslint.org/docs/2.0.0/rules/no-unused-expressions)  
        - 분명히 사용을 하는 함수였는데 사용되지 않는 표현식에 대한 경고가 나왔다. 
        - 문제는 함수와 화살표 함수를 섞어쓰다가 리턴값을 제대로 살펴보지 않았다는 데에 있었다.
    - 참고 : [화살표 함수 사용 시 주의사항](https://velog.io/@bigbrothershin/JavaScript-화살표-함수-사용-시-와-사용상-주의할-점)  
    - 참고 : [MDN 공식 문서 - 화살표 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
        ```
        // 화살표 함수의 유일한 문장이 'return'일 때 'return'과
        // 중괄호({})를 생략할 수 있다.
        elements.map(element => element.length); // [8, 6, 7, 9]
        ```
        - MDN의 예제를 보면 화살표 함수도 일반 함수와 마찬가지로 중괄호{}를 사용하나, return과 중괄호를 생략할 때만 소괄호()로 나타낼 수 있다. 이걸 제대로 숙지하지 않고 무턱대고 썼다가 경고장이 떴다. 

<br/>

  



