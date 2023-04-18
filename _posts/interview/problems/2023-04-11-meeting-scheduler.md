---
layout: post
published: true
title: "1229. Meeting Scheduler"
categories: interview
tags: problems two-pointers
---

> duration 동안 지속 가능한 가장 빠른 시간 슬롯을 반환

- [1229. Meeting Scheduler](https://leetcode.com/problems/meeting-scheduler/)

```java
class Solution {
    
    // duration 동안 지속 가능한 가장 빠른 시간 슬롯을 반환
    // T: O(mlogm + nlogn)
    public List<Integer> minAvailableDuration(int[][] slots1, int[][] slots2, int duration) {
        List<Integer> result = new ArrayList<>();
        
        // 시작시간으로 정렬
        Arrays.sort(slots1, (a, b) -> a[0] - b[0]);
        Arrays.sort(slots2, (a, b) -> a[0] - b[0]);
        
        int s1 = 0, s2 = 0;
        while (s1 < slots1.length && s2 < slots2.length) {
            // 시작은 큰값을 선택한다.
            int maxStart = Math.max(slots1[s1][0], slots2[s2][0]);
            // 종료는 작은값을 선택한다.
            int minEnd = Math.min(slots1[s1][1], slots2[s2][1]);
            
            if (minEnd - maxStart >= duration) {
                result.add(maxStart);
                result.add(maxStart + duration);
                break;
            }
            
            // increment indexes of whatever interval is ending first, sometimes it could be both
            if (slots1[s1][1] == minEnd) s1++;
            if (slots2[s2][1] == minEnd) s2++;
        }
        
        return result;
    }
}
```