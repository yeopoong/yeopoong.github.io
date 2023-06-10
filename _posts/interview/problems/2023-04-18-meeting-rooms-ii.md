---
layout: post
published: true
title: "253. Meeting Rooms II"
categories: interview
tags: medium array two-pointers
---

> 미팅 시간이 겹치지 않도록 필요한 최소 회의실 수

[253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)

```java
class Solution {
    
    // 미팅 시간이 겹치지 않도록 필요한 최소 회의실 수
    // T: O(nlogn)
    public int minMeetingRooms(int[][] intervals) {
        int maxRoom = 0;
        
        int[] startTime = new int[intervals.length];
        int[] endTime = new int[intervals.length];

        // 시작/종료 시간을 저장하고 정렬
        for (int i = 0; i < intervals.length; i++) {
            startTime[i] = intervals[i][0];
            endTime[i] = intervals[i][1];
        }

        Arrays.sort(startTime);
        Arrays.sort(endTime);

        int room = 0;
        
        // Two Pointer
        int s = 0, e = 0;
        while (s < intervals.length) {
            // 미팅 시간이 중첩되면 미팅룸이 필요하다.
            if (startTime[s] < endTime[e]) {
                s++;
                room++;
                maxRoom = Math.max(maxRoom, room);
            // 미팅이 종료되었으므로 미팅룸을 감소한다.
            } else {
                e++;
                room--;
            }
        }

        return maxRoom;
    }
}
```