---
layout: post
published: true
title: "1272. Remove Interval"
categories: interview
tags: medium interval
---

> 정렬된 간격의 목록에서 toBeRemoved 간격을 제거한 실수 집합을 반환

[1272. Remove Interval](https://leetcode.com/problems/remove-interval/)

![](https://assets.leetcode.com/uploads/2020/12/24/removeintervalex1.png)

```java
class Solution {
    
    // T: O(n)
    public List<List<Integer>> removeInterval(int[][] intervals, int[] toBeRemoved) {
        List<List<Integer>> ans = new ArrayList<>();
        
        for (int[] i : intervals) {
            if (i[1] <= toBeRemoved[0] || i[0] >= toBeRemoved[1]) { // no overlap.
                ans.add(Arrays.asList(i[0], i[1]));
            } else { // i[1] > toBeRemoved[0] && i[0] < toBeRemoved[1].
                if (i[0] < toBeRemoved[0]) { // left end no overlap.
                    ans.add(Arrays.asList(i[0], toBeRemoved[0]));
                }
                if (i[1] > toBeRemoved[1]) { // right end no overlap.
                    ans.add(Arrays.asList(toBeRemoved[1], i[1]));
                }
            }
        }
        
        return ans;
    }
}
```