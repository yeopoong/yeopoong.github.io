---
layout: post
published: true
title: "452. Minimum Number of Arrows to Burst Balloons"
categories: interview
tags: problems array greedy
---

> 배열 포인트가 주어지면 모든 풍선을 터뜨리기 위해 발사해야 하는 최소 화살 수를 반환

- [452. Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)

![](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/Figures/452/arrows.png)

```java
class Solution {
    
    // 풍선을 터뜨리기 위한 최소 화살표 수
    // T: O(nlogn)
    public int findMinArrowShots(int[][] points) {
        int arrows = 1;

        // sort by x_end
        Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));

        int start, end; 
        
        int firstEnd = points[0][1];
        
        for (int[] p: points) {
            start = p[0];
            end = p[1];
            
            // 현재 풍선이 다른 풍선이 끝난 후 시작되면 화살이 하나 더 필요하다.
            if (firstEnd < start) {
                arrows++;
                firstEnd = end;
            }
        }

        return arrows;
    }
}
```
