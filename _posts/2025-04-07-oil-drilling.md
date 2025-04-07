---
title: "[Programmers] Oil Drilling (Python)"
date: 2025-04-07
categories: [Algorithm]
tags: [Programmers, level-2]
---

## Problem Description

> Given 2D grid representing a map of land and underground oil. (`0` is empty land, `1` is land that can be drilled)  
> Only a single vertical oil pipe can be used.

**Goal:** Return the maximum volume of oil that can be extracted.

Source: [Programmers - Oil Drilling](https://school.programmers.co.kr/learn/courses/30/lessons/250136)

## Approach

- Calculate each amount of oil using BFS.
- Loop through each column to find the maximum volume.

## Code

### First Try
```python
from collections import deque


def solution(land):
    answer = 0
    q = deque()
    group = []
    visited = [[False for _ in row] for row in land]
    ey = [0, -1, 0, 1]
    ex = [1, 0, -1, 0]

    for i, row in enumerate(land):
        for j, cell in enumerate(row):
            if not visited[i][j] and cell == 1:
                size = 1
                maxx = j
                minx = j
                q.append([i, j])
                visited[i][j] = True
                while q:
                    y, x = q.popleft()
                    for k in range(4):
                        ny = y + ey[k]
                        nx = x + ex[k]
                        if 0 <= ny < len(land) and 0 <= nx < len(land[0]) and not visited[ny][nx] and land[ny][nx] == 1:
                            visited[ny][nx] = True
                            q.append([ny, nx])
                            size += 1
                            maxx = max(maxx, nx)
                            minx = min(minx, nx)
                group.append([minx, maxx, size])

    for i in range(len(land[0])):
        n = 0
        for g in group:
            minx, maxx, size = g
            if minx <= i <= maxx:
                n += size
        answer = max(n, answer)

    return answer
```

It fails because of timeout.

```python
from collections import deque


def solution(land):
    answer = 0
    q = deque()
    col_info=[]
    visited = [[False for _ in row] for row in land]
    ey = [0, -1, 0, 1]
    ex = [1, 0, -1, 0]
    col_id = 0
    col_groups = [set() for _ in range(len(land[0]))]

    for i, row in enumerate(land):
        for j, cell in enumerate(row):
            if not visited[i][j] and cell == 1:
                q.append([i, j])
                visited[i][j] = True
                col_groups[j].add(col_id)
                size = 1
                while q:
                    y, x = q.popleft()
                    for k in range(4):
                        ny = y + ey[k]
                        nx = x + ex[k]
                        if 0 <= ny < len(land) and 0 <= nx < len(land[0]) and not visited[ny][nx] and land[ny][nx] == 1:
                            visited[ny][nx] = True
                            q.append([ny, nx])
                            size += 1
                            col_groups[nx].add(col_id)
                col_info.append([col_id, size])
                col_id += 1
    for i in range(len(land[0])):
        n = 0
        for g in col_groups[i]:
            n += col_info[g][1]
        answer = max(n, answer)

    return answer
```

By using oil group IDs and sets, unnecessary column checks were removed.

## Thoughts

- It's impressive how indexing can help in solving algorithm problems.