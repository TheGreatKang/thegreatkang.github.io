---
title: "[Programmers] Fork Lift and Crane (Python)"
date: 2025-03-31
categories: [Algorithm]
tags: [Programmers, level-2]
---

## Problem Description

> In a warehouse with containers arranged in an n * m gird, each container is labeled with an uppercase letter.
> If a request like "A" is received, all **accessible** containers of type A are removed using forklift.
> If a request like "AA" is received, **all** containers of type A are removed using crane.

**Goal:** Calculate how many containers are left

Source: [Programmers - Fork Lift and Crane](https://school.programmers.co.kr/learn/courses/30/lessons/388353)


## Approach

- Use BFS to check if it's accessible.


## Code

```python
from collections import deque
from typing import List


def solution(storage: List[str], requests: List[str]):
    store = [[char for char in row] for row in storage]

    for req in requests:
        to_remove = []
        for i, row in enumerate(store):
            for j, char in enumerate(row):
                if char == req:
                    if i == 0 or j == 0 or i == len(store) - 1 or j == len(store[0]) - 1:
                        to_remove.append((i, j))
                    elif bfs(store, (i, j)):
                        to_remove.append((i, j))
                if len(req) == 2 and char == req[0]:
                    to_remove.append((i, j))

        for i, j in to_remove:
            store[i][j] = '0'

    print(store)

    return sum(1 for row in store for val in row if val != '0')


def bfs(arr: List[List[str]], start) -> bool:
    q = deque()
    ey = [0, -1, 0, 1]
    ex = [1, 0, -1, 0]
    visited = [[False for _ in row] for row in arr]

    q.append(start)
    visited[start[0]][start[1]] = True

    while q:
        y, x = q.popleft()
        for i in range(4):
            ny = y + ey[i]
            nx = x + ex[i]

            if arr[ny][nx] == '0' and (ny == 0 or nx == 0 or ny == len(arr) - 1 or nx == len(arr[0]) - 1):
                return True
            elif not visited[ny][nx] and arr[ny][nx] == '0':
                q.append((ny, nx))
                visited[ny][nx] = True

    return False
```
