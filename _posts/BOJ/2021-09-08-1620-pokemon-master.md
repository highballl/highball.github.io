---
title: "나는야 포켓몬 마스터 이다솜"
layout: posts
permalink: categories/:categories/:title
categories:
  - Algorithm
tags:
  - Algorithm
  - Python
#date: 2021-09-08T00:30:00
toc: true
---

`last update: 2021.09.08.WED` 

### 1620 나는야 포켓몬 마스터 이다솜, Silver 4
Memory 147968KB, Time 6972ms

<br>

* 시간 초과가 나서 PyPy3으로 제출하여 통과했다.
* 메모리 및 시간 측면에서 개선이 필요하다.
* 해시를 사용해서 개선을 해봐야겠다.


```python
import sys

N, M = map(int, input().split())
input_list = [sys.stdin.readline().strip() for _ in range(N+M)]

quiz = []
pokemon = []


for i in range(N+M):
    if i < N:
        pokemon.append(input_list[i])
    else:
        quiz.append(input_list[i])

for i in range(M):
    q = quiz[i]
    if q.isalpha():
        print(pokemon.index(quiz[i])+1)
    elif q.isdigit():
        print(pokemon[int(quiz[i])-1])
```