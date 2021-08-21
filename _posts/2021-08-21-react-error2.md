---
title: "자 이제 시작이야 - 리액트 첫 프로젝트에서 만난 에러모음(2)"
layout: posts
permalink: /categories/:categories/:title
categories:
  - React
tags:
  - React
  - JavaScript
  - JSX
  - Frontend
#date: 2021-08-21T23:55:00
toc: true
---
`last update: 2021.08.21.SAT`

# 리액트 첫 프로젝트에서 만난 에러 모음(2)    

## 자 이제 시작이야  

- 평생 에러와 함께할 것 같은 느낌이다. 받아들여야겠지?  
- 지난번에 함께해서 더러웠고 다신 만나지 말자고 했지만 얼굴 아니 메시지에 점만 찍고 나타나서는 쟤랑 나는 다른 에러라 우기는 친구들을 오늘도 참 많이 봤다.  
- 에러의 이유는 다 다른데 에러 자체는 은근히 공통점이 있었다.   


### 1) data type을 다신 무시하지 마라  

- 초식동물이 육식을 할 수 없듯 리턴값에 함수와 객체를 함부로 멕이면 안된다.   
**[Object Object]는 차라리 양반이다.** 자료형 때문에 별별 에러메시지를 다 영접했다.  
- error message 모음  
    - `Uncaught TypeError: data.split is not a function`  
        - 제가 감히 객체를 자르려고 했사옵니다 통촉하여 주시옵소서... 장미칼이 아닌 이상 자를 수 있는 건 문자열까지다. (response.data를 자르려고 했다는 말)   
    - `Cannot read property '0' of undefined`  
        - 이 글 쓰기 직전까지도 계속 봤던 에러다. 내가 널 좀 아는데... 답은 왜 계속 틀릴까  
    - `ReferenceError: Cannot access 'newAnswer' before initialization`  
        - 자료형 에러는 아니지만 어차피 초보가 하는 에러니까 아무데나 써본다.  
        - 초기화/선언 하기 전에 제발 값을 할당하지 말자. 김칫국 그만 마시기  



- 불변 자료형을 가변 자료형 취급하면 콘솔창에서 자꾸 네 이노옴 한다.   

<br/>

### 2) 라이브러리를 믿었는데 - ESLint error  

- 현재 create-react-app으로 프로젝트를 시작한 뒤 yarn으로 패키지 관리를 하는 중이다.  
- 작업 도중에 ESLint와 prettier를 추가로 설치했다. 하지만 그때부터 지옥도가 펼쳐졌다.  
- npm 에러까지 나고 난리도 아니었다. 폴더를 다 밀고 환경을 새로 세팅했는데도 같은 에러가 나왔다.  
- error message 모음  
    - `Uncaught [Error: could not find react-redux context value; please ensure the component is wrapped in a <Provider>`  
        - Provider 안에 컴포넌트가 있어야 한다고 했는데 이미 그런 상태다.  
    - `Failed to load config "react-app" to extend from.`  
        - 제일 황당했다. 왜 갑자기 리액트 앱이 안된다는 거지?  
    - `Failed to load parser 'babel-eslint' declared in 'package.json » eslint-config-react-app » (대충 파일 경로)/node_modules/eslint-config-react-app/base.js': Cannot find module 'babel-eslint' Require stack:`  
        - 바벨, 파서가 문제가 생겼다는데 파서를 직접 건드릴 레벨이면 지금 내가 부트캠프가 아니라 네카라쿠배당토나 FAMANG에 있었겠지?  
        - 공식 문서를 믿자. [공식 문서](https://eslint.org/docs/user-guide/getting-started)를 열어봤다 
        - ESLint는 npm으로 설치하래서 그렇게 했다. 나는 시키는대로 했을 뿐인데...
    - `React version not specified in eslint-plugin-react settings. See https://github.com/yannickcr/eslint-plugin-react#configuration`  
        - eslint 설정 파일을 보니 뭔가 휑하긴 했다. 다른 블로그를 찾아서 이것저것 수정했으나 어차피 이게 문제의 핵심은 아니었다.  
        - 참고 : [1](https://blog.kwonmory.com/tip/react-version-not-specified-in-eslint-plugin-react-settings/)
        - 참고 : [2](https://www.python2.net/questions-1298078.htm)
        ```
        참고1의 해결법
        //.eslintrc.js
        {
            ...
            settings: {
                react: {
                version: 'detect',
                },
            },
        }
        ```
        ```
        참고2의 해결법
        module.exports = {
            "env": {
                "browser": true,
                "es2021": true
            },
            "extends": "plugin:react/recommended",
            "parserOptions": {
                "ecmaFeatures": {
                    "jsx": true
                },
                "ecmaVersion": 12,
                "sourceType": "module"
            },
            "plugins": [
                "react"
            ],
            "rules": {
                "semi": ["error", "always"],
                "quotes": ["error", "double"]
            },
            "settings": {
                "react": {
                "version": 'detect',
                },
            },
            {
                "extends": "eslint:recommended"
            }
        };
        ```
    - `Cannot find module 'babel-eslint'`  
        - 내가 물건을 못 찾을 때 답답했을 엄마의 심정이 이랬을까...  
        - 참고 : [https://github.com/standard/standard/issues/85](https://github.com/standard/standard/issues/85)
        - `npm install babel-eslint --save-dev` : 이걸 하고 잠깐 괜찮았는데 다시 에러.  
    - `is missing in props validation`  
        - [stackoverflow](https://stackoverflow.com/questions/38684925/react-eslint-error-missing-in-props-validation)   
        - 찾으면 답이 하나씩 다 나오는 건 정말 신기했지만 그때 뿐이었다. 나올 에러는 어차피 계속 나왔다.  
        - 링크에서는 이런 방법을 추천해줬다. 고맙지만 효과가 없었다.  
        ```
        "rules": {
            "react/prop-types": "off"
        }
        ```
    
    - **`TypeError: Cannot read property 'join' of undefined`**
        - 제일 황당했다. 이제 자바스크립트 기본 함수까지도 먹통이네?  
        - 이 에러를 보고 안되겠어서 그냥 다 밀어버리려고 했다. node를 다시 깔고(전역, 로컬 모두) 다른 패키지도 처음부터 다시 설치했다.  
        - 그러나 에러는 여기서 끝이 아니었다.  


### 끝은 곧 시작이고 시작은 곧 끝이다. 

- 처음에 공유받은 문서에 답이 다 있었는데 글을 끝까지 읽지 않은 내 잘못이었다. 한국어는 특히 끝까지 들어야 한다. 
- [ESLint-Prettier-적용하기](https://velog.io/@recordboy/ESLint-Prettier-적용하기)
- create-react-app으로 리액트 프로젝트를 만든 경우에는 eslint가 이미 적용되어 있으므로 추가 설치시 충돌이 일어난다는 것 같다. 분명 이 문서를 처음에 읽고 그냥 넘어갔었는데 다른 충돌을 해결하고자 폴더를 한 번 밀어버린 뒤 ESLint를 설치했더니 계속 여러 오류가 발생했던 거였다. ESLint를 설치하지 않으니 문제가 모두 해결되었다. 하루 반나절이 날아갔다.   


<br/>


### 3) Cannot read property 'join' of undefined

- 너 왜 집에 아직도 안갔니?  
- create-react-app을 설치하고 별다른 일을 하지 않았더니 오히려 ESLint 에러가 해결되었는데 위의 에러는 계속 나왔다. 이번엔 컴퓨터를 싹 밀어야 하나?  

<br />

### 4) 반려 CORS error 

- 에러가 나면 모두 해결하려고만 했다. 
  주로 크롬을 사용하는데, CORS error가 콘솔창에 뜨면 어떻게든 해결하려고 며칠째 용을 썼다. 
  하지만 죄다 실패했다.
- 별짓을 다해봤는데 이것 자체는 해결하지 못했다. 그러나,
- 이 에러는 무시가 되는 에러였다. 뭐지? 그래서 그냥 에러와 그럭저럭 함께 잘 지내고 있다. 콘솔창만 켜면 계속 보이니까 반갑다야.(아님)

<br />

### 5) 기타 에러 
- 에러 메시지 
    - `Warning: You provided a checked prop to a form field without an onChange handler. This will render a read-only field. If the field should be mutable use defaultChecked. Otherwise, set either onChange or readOnly.`  
        - radio 버튼에 onClick을 썼는데 친절히 onChange를 쓰라고 해서 바꿨더니 잘 해결되었다. 끝이 좋으면 다 좋은 거니까 엔딩은 이걸로   



실제 에러는 이 2-3배쯤 더 겪었는데 기록으로 남긴 게 이것 '뿐'이다.  
다음주엔 우리 제발 좀 헤어지자...    