---
title: "대칭 차집합"
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

### 1269 대칭 차집합, Silver 3
Memory 85532KB, Time 360ms

<br>

* 코드는 짧지만 메모리나 실행 시간을 보니 리팩토링을 꼭 다시 해봐야겠다.
* 집합을 집합 자료형이 아닌 형태로 푸는 게 더 나을까?
* 백준의 알고리즘 분류를 보면 트리나 해시를 이용하는 문제인 것 같으니 추후 다시 풀어봐야겠다.


```python
import sys
a, b = map(int, input().split())
A = set(map(int, sys.stdin.readline().split()))
B = set(map(int, sys.stdin.readline().split()))

print(len(A | B) - len(A & B))
```