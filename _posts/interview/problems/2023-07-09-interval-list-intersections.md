---
layout: post
published: true
title: "986. Interval List Intersections"
categories: interview
tags: medium two-pointers
---

> 쌍으로 서로소이고 정렬되어 있는 두 간격 목록의 교집합을 반환

[986. Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/)

![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

```java
class Solution {
    
    // 교차되는 부분 찾기 
    // Two Pointer: O(m+n)
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        List<int[]> list = new ArrayList();
        
        int i = 0, j = 0;
        while (i < firstList.length && j < secondList.length) {
            // 시작점은 큰값, 종료점은 작은값이 된다.
            int lo = Math.max(firstList[i][0], secondList[j][0]); // lo - the startpoint of the intersection
            int hi = Math.min(firstList[i][1], secondList[j][1]); // hi - the endpoint of the intersection

            // 종료지점이 시작지점보다 크면 겹친다.
            if (lo <= hi) {
                list.add(new int[]{lo, hi});
            }

            // 종료지점이 작은 구간을 다음 처리한다.
            if (firstList[i][1] < secondList[j][1]) {
                i++;
            } else {
                j++;
            }
        }

        return list.toArray(new int[list.size()][]);
    }
}
```