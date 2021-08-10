---
title: "English for Developers"
layout: posts
permalink: /categories/english/
categories:
  - english
tags:
  - programming
  - general
  - english
  - translation
#date: 2021-08-01T00:00:00
toc: true
---

# English for Developers / 개발자 영어
* 필요한 용어를 검색하는 용도로 생성한 문서입니다.
* 번역 문의 : jyp0293@gmail.com 




## drive / driven

* drive는 무언가를 '촉발하다, 일으키다'라는 뜻으로 자주 사용됩니다. 
* 예문 :
    * event-driven : 이벤트에 의해 생성되거나 작동하는 무언가를 설명할 때 사용합니다.

## trigger
* 
* 예문 : 



## resolve 
* 문제를 해결한다는 의미입니다. 
* 현재형으로 쓰지만 실제 코드에서는 '(문제나 상황이) 해결되었을 때'를 의미하기도 합니다.
* javascript의 경우 promise-then 구문에서 요청을 처리할 수 있는 상황이 되었을 때 할 작업을 resolve 부분에 둡니다.

## parse
* 분석하다
* 구문을 분석할 때 보통 파싱(parsing)이라는 용어를 사용합니다. 
* 예문 : 
    - C에서 컴파일 단계를 거치면서 C언어를 기계어로 파싱한다. 
    - HTML코드를 파싱하여 DOM tree로 만든다.


## lexical analysis vs parser
* lexical analysis : 어휘 분석, 낱말 분석
* parser : 구문 분석
* 더 알아보기 : 
    - lexical analysis : https://coding-groot.tistory.com/17
    - parser : 
    - Main difference between lexical analyzer and parser?
    https://na27.tistory.com/230
        - 답변 번역+요약
        - Lexical analyzer는 입력값을 해당 언어에 유효한 토큰으로 나눕니다.
            - 예 : beautiful은 영어에서 유효한 단어이자 토큰입니다.
            - 예 : dsefuewfiu는 영어에서 유효한 단어 및 토큰이 아닙니다.
        - Parser는 문장이 문법에 맞는지 검사합니다.
            - 예 : My name is Rahul은 유효한 문장입니다.
            - 예 : name my is Rahul은 그렇지 않습니다.


## fetch, retrieve, get
* fetch : '명령에 따라서 가져오다'
* retrieve : '가져오다' + '회수하다'
* get : '가져오다' 또는 '얻다'
* 더 알아보기 : 생활코딩 토론 스레드
    https://www.facebook.com/groups/engfordev/permalink/575140472537782/


## Error vs Warning
* Error는 해결하지 않으면 실행에 지장이 생기는 오류
* Warning은 말 그대로 경고이며 해결하지 않아도 프로그램을 당장 실행할 수는 있음