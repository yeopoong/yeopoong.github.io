---
layout: post
published: true
title: "252. Meeting Rooms"
categories: interview
tags: sort array
---

> intervals[i] = [starti, endi]인 일련의 회의 시간 간격이 주어지면 한 사람이 모든 회의에 참석할 수 있는지 확인

- [252. Meeting Rooms](https://leetcode.com/problems/meeting-rooms/)

```java
class Solution {
        
    // Brute Force    
    // T: O(n^2)
    public boolean canAttendMeetings(int[][] intervals) {
        for (int i = 0; i < intervals.length; i++) {
            for (int j = i + 1; j < intervals.length; j++) {
                if (overlap(intervals[i], intervals[j])) {
                    return false;
                }
            }
        }
        return true;
    }

    // 종료가 시작보다 크고, 시작이 종료보다 작으면 오버랩
    private boolean overlap(int[] interval1, int[] interval2) {
        return (interval1[1] > interval2[0] && interval2[1] > interval1[0]);
    }
}
```

```java
class Solution {
        
    // 시작순으로 정렬하고 이전 종료가 이후 시작보다 크면 중복 미팅이 존재함
    // T: O(nlogn)
    public boolean canAttendMeetings(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        for (int i = 0; i < intervals.length - 1; i++) {
            if (intervals[i][1] > intervals[i+1][0]) {
                return false;
            }
        }
        return true;
    }
}
```