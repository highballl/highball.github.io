---
title: "효율적인 해킹"
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

### 1325 효율적인 해킹, Silver 2
Memory 206584KB, Time 13400ms

<br>

* 시간 문제로 이번에는 PyPy3을 이용했다.
* 하지만 그럼에도 불구하고 메모리나 시간을 너무 잡아먹는다. 더 나은 방법을 찾아야겠다.
* 백준의 알고리즘 분류를 보면 트리나 해시를 이용하는 문제인 것 같으니 추후 다시 풀어봐야겠다.


```python
import sys
from collections import deque

n, m = map(int, input().split())

graph = [[] for _ in range(n+1)]
for i in range(m):
    a, b = map(int, sys.stdin.readline().split())
    graph[b].append(a)

result = []
max_count = -1

for i in range(1, n+1):
    visited = [False]*(n+1)
    q = deque([i])
    visited[i] = True
    count = 1
    while q:
        curr = q.popleft()
        for num in graph[curr]: 
            if visited[num] == False:
                q.append(num)
                visited[num] = True
                count += 1
    if count > max_count:
        max_count = count
        result = []
        result.append(i)
    elif max_count == count:
        result.append(i)

for i in range(len(result)):
    print(result[i], end=" ")
```


<br>

* 출력 초과가 났던 코드

```python
import sys
from collections import deque

n, m = map(int, input().split())

graph = [[] for _ in range(n+1)]
for i in range(m):
    a, b = map(int, sys.stdin.readline().split())
    graph[b].append(a)

result = []
max_count = -1

for i in range(1, n+1):
    visited = [False]*(n+1)
    q = deque([i])
    count = 1
    while q:
        curr = q.popleft()
        for num in graph[curr]: 
            if visited[num] == False:
                q.append(num)
                visited[num] = True
                count += 1
    if count > max_count:
        max_count = count
        result = []
        result.append(i)
    elif max_count == count:
        result.append(i)

result.sort()
for i in range(len(result)):
    print(result[i], end=" ")

```
