---
title: "[LeetCode] Ransom Note (Python)"
date: 2025-04-06
categories: [Algorithm]
tags: [LeetCode, easy]
---

## Problem Description

> Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.

Source: [LeetCode - Ransom Note](https://leetcode.com/problems/ransom-note/description/?envType=problem-list-v2&envId=rab78cw1)

## Approach

- Count letters in magazine.
- Subtract the letters from the magazine letter counts.
- If any count goes below zero, return false.

## Code

```python
from collections import defaultdict

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        tmp = defaultdict(int)

        for a in magazine:
            tmp[a] += 1

        for a in ransomNote:
            if tmp[a] <= 0:
                return False
            tmp[a] -= 1

        return True
```
