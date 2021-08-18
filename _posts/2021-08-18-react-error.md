---
title: "함께해서 더러웠고"
layout: posts
permalink: /categories/:categories/:title
categories:
  - React
tags:
  - React
  - JavaScript
  - JSX
  - Frontend
#date: 2021-08-18T22:00:00
toc: true
---
`last update: 2021.08.18.WED`

# 리액트 첫 프로젝트에서 만난 에러 모음  

### 함께해서 더러웠고 다신 보지 말자  

- 1) `Error: Objects are not valid as a React child (found: [object Promise]). If you meant to render a collection of children, use an array instead.`  
    - 참고 : [React-Objects-are-not-valid-as-a-React-child-에러-처리](https://velog.io/@bigbrothershin/React-Objects-are-not-valid-as-a-React-child-에러-처리)  
    - 참고 : [React 개발자가 실수하기 쉬운 몇 가지 (3)](https://cimfalab.github.io/deepscan/2017/07/react-3)
        - 요약 : 이벤트 핸들러를 문자열로 지정하거나, 이벤트 핸들러 함수가 바인딩이 잘못되었거나, 엘리먼트 스타일 속성을 잘못 지정했거나, 자식 엘리먼트의 key 속성을 지정하지 않았거나. 등등. 잘 정리된 좋은 글이었다.  
    - 참고 : [React 99% 에러잡기](https://helicopter55.tistory.com/21)  
        - 요약 : 내가 겪은 에러와 가장 비슷한 경험담.  
    - 원인 : api 데이터를 가져온 직후 console.log(res.data)로 출력하려고 했다. 객체를 그대로 프린트할 수 없는 것 같다. 
    - 해결책 : map 함수와 빨리 친해지자.  
        - 추가 참고 : [여러가지 예시를 들어 array map 함수를 익혀보자.](https://velog.io/@daybreak/Javascript-map%ED%95%A8%EC%88%98)  
        - 추가 참고 : [map과 set](https://ko.javascript.info/map-set) : map을 사용할 때 key 관련해서 참고할 내용이 담긴 글
    - 코드 예 : 
    ```javascript
    const newAns02 = data.map((q) => q.answer02);
    ```

<br />
<br />

- 2)`SyntaxError: Cannot use import statement outside a module`  
    - 참고 : [Cannot use import statement outside a module 에러 해결](https://takeknowledge.netlify.app/bugfix/cannot-use-import-statement-outside-a-module/)  
    - 원인 : 평소 맥에서 작업하다가 밖에서 코드를 수정할 일이 있어 윈도우 VSCODE로 코드를 실행했더니 저런 에러가 나왔다. package.json파일에 있는 변수 및 설정이 달라서 그런 것 같다.   
    - 해결책 : 위의 링크의 설명대로 아래 코드를 package.json에 추가하고 파일을 실행(예 : `node Title.js`)하면 된다.  
    ```
    "type": "module"
    ```
    - 새로운 문제 : 집으로 돌아와 맥에서 같은 방법을 쓰자 렌더링 에러가 난무해서 그냥 코드를 지웠다.   

<br />

- 3) `SyntaxError: Cannot use import statement outside a module`(2)  
    - 원인 : 윈도우 powershell에서 권한 문제로 패키지 설치가 되지 않았다.   
    - 해결 : `git bash` 쉘로 변경하니 설치가 잘 되었다.  
    - 안해본 해결책 : powershell 관리자모드로 실행하기  
    참고 : [Powershell 스크립트 실행 시 오류(UnauthorizedAccess)(PSSecurityException)](https://samsons.tistory.com/16)

<br />

- 4) `%22` 문제  
    - 참고 : [URL-encoding from %00 to %8f](https://www.eso.org/~ndelmott/url_encode.html)  
        - 요약 : URL에 인코딩 되는 것이 무엇인지 총 망라된 표이다.
    - 발생원인 : API URL과 KEY를 각각 변수로 따로 두고 합쳤더니, get 요청을 하는 url에 자꾸 %22가 붙어서 주소가 엉망이 되었다.  
    - 해결책 : 완전한 해결책은 아니지만 변수를 따로 두지 않고 그냥 하나의 문자열로 썼다.   
    ```javascript  
    const API_URL = "http://www.blahblah.com/12341234123412341234";
    ```
    - 망한 예 : 
    ```javascript
    const API_KEY = "12341234123412341234";
    const API_URL = "http://www.blahblah.com/{API_KEY}";
    //결과 : API_URL = http://www.blahblah.com/%22/12341234123412341234";
    //망할놈의 %22
    ```
    - 정확한 해결책을 더 찾아야 한다.  

<br />

- 5) `Error: connect ECONNREFUSED 127.0.0.1:80`  
    - 참고 : [Getting connect ECONNREFUSED 127.0.0.1:80 when attempting HTTP request](https://stackoverflow.com/questions/39910746/getting-connect-econnrefused-127-0-0-180-when-attempting-http-request)  
    ```  
    //from stackoverflow
    My mistake was not putting "/" as a prefix to some url.   
    So, double check if the url for the request you are making is proper.
    ```  
    - 원인 및 해결책 : axios url에 '/'을 빼먹거나, https://를 빼먹어서 생긴 문제    

<br />

- 6) `has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.`  
    - 참고 : [Axios에 헤더 추가하기](https://blog.jell.kr/dev/js/tip/2020/01/07/Axios%20%EC%84%A4%EC%A0%95%20%EC%8B%9C%20%ED%97%A4%EB%8D%94%EB%A5%BC%20%EB%84%A3%EB%8A%94%20%EB%B2%95/)  
    - 참고 : []()  
    - 참고 : []()  
    - 원인 : **CORS**!!!!!!!  
    - 해결책 : 이번 경우는 api get 요청 때 사용한 URL 주소에 오타가 있어서 해프닝으로 끝났다. 하지만 12시간을 날린 해프닝이었다. 이녀석은 언젠가는 다시 만나게 될 에러이니 참고 사이트만 우선 백업해두었다.  

<br />

- 7) `onSubmit`을 눌러도 페이지 이동이 안되는 현상 
    - 참고 : [[React] 라우터(Router), 스위치(Switch), 링크(Link), 리다이렉트(Redirect)를 이용한 페이지 이동](https://jiguin-hankun.tistory.com/39)  
    - 참고 : [React-Router-Dom 사용하기](https://yerinko.tistory.com/27) 
        - 요약 : BrowserRouter, HashRouter, Route, Switch 관련 개념이 잘 정리되어 있어 도움이 되었다. 
    - 참고 : [리액트 공식문서 - 폼(Form)](https://ko.reactjs.org/docs/forms.html)
        - 요약 : Form 태그에 대한 이해를 제대로 못한 것 같아서 읽었다. 공식문서부터 항상 먼저 보는 습관을 들이자.
    - 참고 : [React Router: router, link](https://velog.io/@bigbrothershin/React-Router)
        - 요약 : Router, Link 설명
    - 참고 : [input type="submit" vs button 비교](https://webdir.tistory.com/421)
        - 요약 : button 태그에 대한 좋은 요약 
    - 참고 : [reactrouter.com - Link 더 알아보기](https://reactrouter.com/web/api/Link)
        - 요약 : react-router 관련 기본 설명
    - 원인 : onSubmit과 관련된 DOM에 대한 이해 부족, react-router-dom에 대한 이해 부족  
    - 해결1 : `<BrowserRouter>`를 `<Link>`와 계속 같이 쓰고 있었다. 브라우저라우터를 삭제하니 잘 작동했다. 
    - 해결2 : 혹시 몰라 태그도 input으로 모두 바꾸고 type=button으로 두었다.   
    - 해결3 : onSubmitHandler도 상단의 form태그가 아니라 input button에 모두 두었다. 

<br />
  

- 8) `React Hook useEffect has a missing dependency: 'xxx'. Either include it or remove the dependency array. (react-hooks/exhaustive-deps)`  
    - 참고 : [exhaustive-deps-warning 해결법](https://kyounghwan01.github.io/blog/React/exhaustive-deps-warning/  #_1-useeffect%E1%84%82%E1%85%A2-state%E1%84%85%E1%85%B3%E1%86%AF-%E1%84%82%E1%85%A5%E1%87%82%E1%84%8B%E1%85%A5%E1%84%8C%E1%85%AE%E1%86%B7)  
        - 요약 : useEffect 관련 문제에 대해 잘 설명하는 좋은 글  
    - 원인 및 해결책 : useEffect 내의 함수가 사용하는 변수를 배열(dependency array)에 넣어줘야 한다. 그 밖의 원인 및 해결책은 위의 링크 참고  

<br />

- 9) `Unexpected lexical declaration in case block`  
    - 참고 : [case / default 절에서 어휘 선언을 허용하지 않습니다 (대소 문자 구분 안함)](https://runebook.dev/ko/docs/eslint/rules/no-case-declarations)  
    - 원인 : ESLint 설치 후 생긴 현상이었다.  
    - 해결 : 중괄호를 잘 치자.  