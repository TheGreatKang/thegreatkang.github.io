---
title: "[LeetCode] Longest Palindromic Substring"
date: 2025-04-11
categories: [Algorithm]
tags: [LeetCode, medium]
---

## Problem Description

> Given a string s, return the longest palindromic substring in s.

Source: [LeetCode - Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

## Approach

- Use two pointers to expand outward from the center and check if the substring is palindromic.
- For even-length cases, perform the loop twice, starting with the right pointer at `i + 1`.

## Code

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        answer = ''

        for i in range(len(s)):
            l, r = i, i
            while 0 <= l <= r < len(s):
                if s[l] != s[r]:
                    break
                tmp = s[l:r + 1]
                if len(tmp) > len(answer):
                    answer = tmp
                l -= 1
                r += 1

            l, r = i, i + 1
            while 0 <= l <= r < len(s):
                if s[l] != s[r]:
                    break
                tmp = s[l:r + 1]
                if len(tmp) > len(answer):
                    answer = tmp
                l -= 1
                r += 1

        return answer
```