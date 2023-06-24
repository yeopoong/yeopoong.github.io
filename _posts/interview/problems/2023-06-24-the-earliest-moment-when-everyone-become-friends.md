---
layout: post
published: true
title: "1101. The Earliest Moment When Everyone Become Friends"
categories: interview
tags: easy two-pointers
---

> 다음 배열에서 모든 사람이 다른 모든 사람을 알게 되는 가장 빠른 시간을 반환
> - logs[i] = [timestampi, xi, yi]는 xi와 yi가 시간 timestampi에서 친구가 될 것임을 나타낸다.

[1101. The Earliest Moment When Everyone Become Friends](https://leetcode.com/problems/the-earliest-moment-when-everyone-become-friends/)

```java
class Solution {
    
    // 모두가 친구가 되는 가장 빠른 순간
    // 우정은 대칭입니다. 즉, a가 b와 친구이면 b는 a와 친구입니다. 
    // 또한 a가 b와 친구이거나 a가 b와 아는 사람의 친구라면 a는 b와 아는 사이입니다.
    public int earliestAcq(int[][] logs, int n) {
        // 시간순으로 오름차순 정렬
        Arrays.sort(logs, (a, b) -> a[0] - b[0]);
        
        int[] parent = new int[n];
        Arrays.fill(parent, -1);
        
        int count = n;
        for (int[] log : logs) {
            if (find(parent, log[1]) != find(parent, log[2])) {
                parent[find(parent, log[1])] = log[2];
                count--;
            }
            
            if (count == 1) {
                return log[0];
            }
        }
        
        return -1;
    }
    
    private int find(int[] p, int f) {
        if (p[f] == -1) return f;
        
        return find(p, p[f]);
    }
}
```
