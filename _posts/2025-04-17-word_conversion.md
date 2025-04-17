---
title: "[Programmers] Word Conversion"
date: 2025-04-17
categories: [Algorithm]
tags: [Programmers, level-3]
---

## Problem Description

> Convert the word `begin` to `target` using words from the list `words`.

**Goal:** Return the shortest convertion time.

Source: [Programmers - Word Conversion](https://school.programmers.co.kr/learn/courses/30/lessons/43163)

## Approach

- Use BFS

## Code

```python
from collections import deque


def solution(begin, target, words):
    if target not in words:
        return 0

    hs=set()
    dq = deque()
    dq.append((begin,0))

    while dq:
        tmp,cnt = dq.popleft()
        if tmp == target:
            return cnt

        for word in words:
            if sum(c1 != c2 for c1, c2 in zip(tmp, word)) == 1 and word not in hs:
                dq.append((word,cnt+1))
                hs.add(word)

    return 0
```
