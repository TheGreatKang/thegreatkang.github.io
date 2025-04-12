---
title: "[LeetCode] Longest Substring Without Repeating Characters"
date: 2025-04-08
categories: [Algorithm]
tags: [LeetCode, medium]
---

## Problem Description

> Given a string s, find the length of the longest substring without duplicate characters.

Source: [LeetCode - Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

## Approach

- Typical sliding window problem.

## Code

```python
from collections import deque


class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        dq= deque()
        st = set()
        answer = 0

        for ch in s:
            while ch in st:
                rs = dq.popleft()
                st.remove(rs)

            st.add(ch)
            dq.append(ch)
            answer = max(answer, len(st))
        return answer
```
