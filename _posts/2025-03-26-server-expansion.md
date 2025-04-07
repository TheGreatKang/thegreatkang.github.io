---
title: "[Programmers] Number of Server Expansions (Python)"
date: 2025-03-26
categories: [Algorithm]
tags: [Programmers, level-2]
---

## Problem Description

> One server can handle up to `m` players.  
> Each server runs for `k` hours and then shuts down.  
> `players[i]` represents the number of players at time `i`.

**Goal:** Calculate how many times do we need to add servers to handle traffic.

Source: [Programmers - Number of Server Expansions](https://school.programmers.co.kr/learn/courses/30/lessons/389479)


## Approach

- Loop through each time point and calculate how many servers are required.
- For required servers, add `k` to the deque.
- Decrease each value in the deque by 1 and remove expired servers.


## Code

```python
import math
from collections import deque


def solution(players: list[int], m: int, k: int) -> int:
    answer = 0
    q = deque()

    for player in players:
        q = deque([t - 1 for t in q if t > 1])

        while math.ceil((player + 1) / m) - 1 > len(q):
            q.append(k)
            answer += 1

    return answer
```

