---
title: "[Programmers] N-Base Number Game (Python)"
date: 2025-03-25
categories: [Algorithm]
tags: [Programmers, level-2]
---

## Problem Description

> Players take turns saying digits of numbers.  
> Numbers are converted to **base N** before speaking.  
> All numbers start from 0 and increase by 1.  
> Digits are read **one by one**, left to right.  
> Players speak in a **fixed order**, looping back.

**Goal:** Return a continous string of `t` numbers spoken by `p` in order, using uppercase A-F for 10-15

Source: [Programmers - N-Base Number Game](https://school.programmers.co.kr/learn/courses/30/lessons/17687)


## Approach

- Convert each number to N-base number string.
- Build a combined string of digits.
- Collect every `m`-th digit starting from `p - 1`


## Code

### First Try
```python
import string

def solution(n, t, m, p):
    tmp = ''
    answer = ''

    for i in range(t * m):
        tmp += str(convert(i, n))

    for i in range(p - 1, len(tmp), m):
        answer += tmp[i]
        if len(answer) == t:
            break

    return answer

nums = string.digits + string.ascii_uppercase

def convert(num:int, base:int) -> str:
    q, r = divmod(num, base)
    if q == 0:
        return nums[r]
    else:
        return convert(q, base) + nums[r]
```

It works, but it's not sexy

## More sexy version
```python
import string

def solution(n, t, m, p):
    answer = []
    num = 0
    total_len = 0

    while len(answer) < t:
        for ch in convert(num, n):
            if total_len % m == (p - 1):
                answer.append(ch)
                if len(answer) == t:
                    break
            total_len += 1
        num += 1

    return ''.join(answer)

nums = string.digits + string.ascii_uppercase

... existing code ...

```
- No extra memory needed.
- Avoid unnecessary calculations.
- Only one loop is needed.

## Thoughts

- Another way to solve it, but with one loop, less memory, no waste.
