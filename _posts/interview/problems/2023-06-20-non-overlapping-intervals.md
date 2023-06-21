---
layout: post
published: true
title: "435. Non-overlapping Intervals"
categories: interview
tags: medium intervals greedy
---

> intervals[i] = [starti, endi]인 간격의 배열이 주어지면 나머지 간격이 겹치지 않도록 제거해야 하는 최소 간격 수를 반환

[435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

```java
class Solution {
    
    // 나머지 간격이 겹치지 않도록 제거해야 하는 최소 간격 수: 겹치는 건수를 찾는다.
    // T: O(nlogn)
    public int eraseOverlapIntervals(int[][] intervals) {
        
        int count = 0; 
        
        // 종료지점(end)을 기준으로 정렬한다.
        Arrays.sort(intervals, (a, b) -> a[1] - b[1]);
        
        // 시작지점의 종료값
        int prevEnd = intervals[0][1]; 
        
        for (int i = 1; i < intervals.length; i++) {
            // 이전 종료값이 현재 시작값보다 크면 겹친다.
            if (prevEnd > intervals[i][0]) {
                // 작은값으로 갱신 
                prevEnd = Math.min(prevEnd, intervals[i][1]);
                count++;
            } else {
                // 다음 종료값으로 넘어간다.
                prevEnd = intervals[i][1];
            }
        }
        
        return count;
    }
}
```
