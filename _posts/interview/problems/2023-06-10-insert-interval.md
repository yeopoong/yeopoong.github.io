---
layout: post
published: true
title: "57. Insert Interval"
categories: interview
tags: medium array 
---

> 새로운 간격을 삽입하고 필요하면 머지

[57. Insert Interval](https://leetcode.com/problems/insert-interval/)

```java
class Solution {
    // 새로운 간격을 삽입하고 필요하면 머지
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> result = new ArrayList<>();
        
        for (int[] interval : intervals) {
            // 신규정보를 추가했거나 신규시작이 기존종료보다 클 경우: 기존 정보 추가한다.
            if (newInterval == null || interval[1] < newInterval[0]) {
                result.add(interval);
            }
            // 신규종료가 기존시작보다 작을 경우: 신규 정보 추가하고 기존 정보도 추가한다.
            else if (newInterval[1] < interval[0]) {
                result.add(newInterval);
                result.add(interval);
                newInterval = null;
            // 현재 노드와 신규노드의 머지노드를 만든다.
            } else {
                // 시작은 작은값
                newInterval[0] = Math.min(newInterval[0], interval[0]);
                // 종료는 큰값
                newInterval[1] = Math.max(newInterval[1], interval[1]);
            }
        }
        
        // 아직 추가되지 않은 신규 노드가 있으면 추가한다.
        if (newInterval != null) result.add(newInterval);
        
        return result.toArray(new int[result.size()][]);
    }
}
```
