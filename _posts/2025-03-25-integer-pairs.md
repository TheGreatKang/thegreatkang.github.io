---
title: "[Programmers] Integer Pairs Between Two Circles (Python)"
date: 2025-03-25
categories: [Algorithm]
tags: [Programmers, level-2]
---

## Problem Description

> Two circles with different radii are drawn on a 2D Cartesian coordinate palne,
> both centered at the origin (0, 0)
>
> You are given two integers r1 and r2 representing the radii of the smaller and larger circles respectively.

**Goal:** Calculate the count of integer coordinate between two circles 

Source: [Programmers - Integer Pairs Between Two Circles](https://school.programmers.co.kr/learn/courses/30/lessons/181187)


## Approach

- Calculate the number of points in the first quadrant and multiply it by 4.
- From x = 0 to x = `r2`, find the range of valid values (`max y - min y`) for each `x`.


## Code

```python
def solution(r1: int, r2: int):
    answer = 0
    for x in range(r2):
        max_y, min_y = r2, r1
        while r2 ** 2 < x ** 2 + max_y ** 2:
            max_y -= 1
        while min_y - 1 and r1 ** 2 <= x ** 2 + (min_y-1) ** 2:
            min_y -= 1
        answer += max_y - min_y + 1

    return answer * 4
```
