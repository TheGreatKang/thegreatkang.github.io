---
title: "[Programmers] Counter After Quad Compression (Python)"
date: 2025-03-27
categories: [Algorithm]
tags: [Programmers, level-2]
---

## Problem Description

> Given a 2D integer list.  
> Compress the given array using [quad tree](https://en.wikipedia.org/wiki/Quadtree) compression.

**Goal:** Count the number of zeros and ones.

Source: [Programmers - Counter After Quad Compression](https://school.programmers.co.kr/learn/courses/30/lessons/68936)


## Approach

- Check if all values are the same as the first value in the array.
- If all values are the same as the first value, return a list containing only the first value.
- If not, divide the array into 4 parts and process recursively.


## Code

```python
def solution(arr:list[list[int]]):
    compressed = recursive(arr)
    zero = 0
    one = 0

    for n in compressed:
        if n == 0:
            zero += 1
        else:
            one += 1

    return [zero, one]


def recursive(arr: list[list[int]]) -> list[int]:
    if len(arr) == 1 and len(arr[0]) == 1:
        return [arr[0][0]]

    first_val = arr[0][0]
    if all(all(cell == first_val for cell in row) for row in arr):
        return [first_val]

    n = len(arr)
    half = n // 2

    top_left     = [row[:half] for row in arr[:half]]
    top_right    = [row[half:] for row in arr[:half]]
    bottom_left  = [row[:half] for row in arr[half:]]
    bottom_right = [row[half:] for row in arr[half:]]

    return (
        recursive(top_left) +
        recursive(top_right) +
        recursive(bottom_left) +
        recursive(bottom_right)
    )
```

## Thoughts

- Python's list comprehension proved to be incredibly powerful for handling 2D array slicing, making the code both elegant and readable. I should definitely get more comfortable with this pythonic way of writing code as it can significantly reduce the complexity of array manipulations.
