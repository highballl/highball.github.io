---
title: "팩토리얼 0의 개수"
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

### 1676 팩토리얼 0의 개수, Silver 4
Memory 31312KB, Time 76ms

<br>


```python
import math

n = int(input())
num = str(math.factorial(n))
i = len(num)-1
count = 0

if n == 0 or n < 5:
    print(0)
else:
    while i > 0:
        if num[i] != '0':
            print(count)
            break
        elif num[i] == '0':
            i -= 1
            count += 1
```