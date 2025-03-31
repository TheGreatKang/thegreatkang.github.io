---
title: "[Programmers] Flexible Work System (Python)"
date: 2025-03-24
categories: [Algorithm]
tags: [Programmers, level-1]
---

## Problem Description

> Each employee has a **preferred check-in time**.  
> They must check in within **10 minutes** of that time on **weekdays (Mon–Fri)**.  
> Check-ins on **weekends** are ignored.  
> If an employee is **late even once on a weekday**, they are disqualified.  
> Count how many employees successfully checked in on time for **all 5 weekdays**.

**Goal:** Calculate how many employees can receive awards

Source: [Programmers - Flexible Work System](https://school.programmers.co.kr/learn/courses/30/lessons/388351)


## Approach

- Simply loop through each employee’s time logs and check if they meet the conditions.
- When adding 10 minutes to the preferred time, convert it properly if the minutes go over 60.


## Code

```python
def solution(schedules, timelogs, startday):
    answer = len(schedules)

    for i, timelog in enumerate(timelogs):
        for j, time in enumerate(timelog):
            day = (startday + j - 1) % 7
            time_hope = schedules[i] + 10
            hour = time_hope // 100
            minute = time_hope % 100
            time_hope = (hour + (minute // 60)) * 100 + minute % 60
            if time > time_hope and day < 5:
                answer -= 1
                break

    return answer
```

## Thoughts

- Easy problem, but tricky edge cases.
- Be careful with the edge cases.
