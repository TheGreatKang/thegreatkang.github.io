---
title: "[Programmers] Perfect Crime (Python)"
date: 2025-03-28
categories: [Algorithm]
tags: [Programmers, level-2]
---

## Problem Description

> Thief A and Thief B are planning to steal together.  
> Each time they steal, both thieves leave evidence.  
> When Thief A steals, they leave `info[i][0]` pieces of evidence.  
> When Thief B steals, they leave `info[i][1]` pieces of evidence.  
> If Thief A leaves `n` or more pieces of evidence, they will be arrested.  
> If Thief B leaves `m` or more pieces of evidence, they will be arrested.  

**Goal:** Calculate the minimum number of times Thief A needs to steal.

Source: [Programmers - Perfect Crime](https://school.programmers.co.kr/learn/courses/30/lessons/389480)


## Approach

- Use **recursive function** with memoization (`@lru_cache`).
- For each stealing opportunity:
  - If Thief A steals: Add `info[i][0]` to evidence count and increment A's steal count.
  - If Thief B steals: Add `info[i][1]` to evidence count (A's steal count unchanged).
- Base cases:
  - If evidence exceeds limit (`n` or `m`): Return `infinity`.
  - If all opportunities used: Return current steal count.
- Return minimum count among all possible combinations.
- If no valid solution exists: Return `-1`.

***

## Code

```python
import math
from functools import lru_cache
from typing import List


def solution(info: List[List[int]], n: int, m: int) -> int:

    @lru_cache(maxsize=None)
    def recursive(idx:int, _n: int, _m: int, cnt: int):

        if _n <= 0 or _m <= 0:
            return math.inf
        elif len(info) == idx:
            return cnt

        a, b = info[idx]
        idx += 1

        return min(recursive(idx, _n - a, _m, cnt + a), recursive(idx, _n, _m - b, cnt))

    answer = recursive(0, n, m, 0)

    return answer if answer != math.inf else -1
```

## Thoughts

- Lists cannot be used as arguments in memoized functions due to their mutable nature.
- Using `@lru_cache` significantly improves performance in recursive solutions.