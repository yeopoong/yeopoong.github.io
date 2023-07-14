---
layout: post
published: true
title: "56. Merge Intervals"
categories: interview
tags: medium interval
---

> intervals[i] = [starti, endi]인 간격 배열이 주어지면, 모든 겹치는 간격을 병합하고 입력의 모든 간격을 포함하는 겹치지 않는 간격의 배열을 반환

[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

시작값을 기준으로 정렬 후 

```java
class Solution {
    // Time : O(nlogn)
    // Space: O(n)
    public int[][] merge(int[][] intervals) {
        List<int[]> merged = new ArrayList<>();
        
        // 시작값을 기준으로 오름차순으로 정렬
        // Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        
        int[] last = null;
        for (int[] interval : intervals) {
            // 종료값이 시작값보다 크면 오버랩
            if (last != null && last[1] >= interval[0]) {  
                // 종료지점을 큰 값으로 갱신한다.
                last[1] = Math.max(last[1], interval[1]);
            // 오버랩되지 않으면 마지막 셀을 갱신하고 현재 셀을 병합리스트에 추가한다.
            } else { 
                last = interval;
                merged.add(interval);
            }
        }
        
        return merged.toArray(new int[merged.size()][]);
    }
}
```