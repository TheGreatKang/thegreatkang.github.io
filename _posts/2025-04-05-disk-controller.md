---
title: "[Programmers] Disk Controller (Python)"
date: 2025-04-05
categories: [Algorithm]
tags: [Programmers, level-3]
---

## Problem Description

> A hard disk can handle only one task at a time. Each task is given as a pair `[request_time, duration]`. The goal is to schedule the tasks in a way that minimizes the **average turnaround time**, where turnaround time is the time from request to completion for each task.

**Goal:**  
Minimize the average time each task spends from request to completion.

Source: [Programmers - Disk Controller](https://school.programmers.co.kr/learn/courses/30/lessons/42627)

---

## Approach

- The key idea is to implement **Shortest Job First (SJF)** scheduling.
- Tasks that have arrived by the current time are pushed into a **min-heap**, prioritized by their duration.
- At each time unit, we:
  - Check for newly available tasks and add them to the heap.
  - If the heap is not empty, pop the shortest job and process it.
  - If no jobs are available, simply advance the current time.
- This strategy ensures that shorter jobs are processed first, reducing the overall average waiting time.

---

## Code

```python
import heapq

def solution(jobs):
    answer = 0
    now = 0
    done = 0
    start = -1
    njobs = []
    hq = []
    
    for i, job in enumerate(jobs):
        a, b = job
        njobs.append((b, a, i))  # (duration, request_time, job_id)
        
    while done < len(jobs):
        for job in njobs:
            if start < job[1] <= now:
                heapq.heappush(hq, job)
        if hq:
            duration, req, jid = heapq.heappop(hq)
            start = now
            now += duration
            answer += now - req
            done += 1
        else:
            now += 1
    
    return answer // len(jobs)
```