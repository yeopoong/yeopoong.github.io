---
layout: post
published: true
title: "624. Maximum Distance in Arrays"
categories: interview
tags: problems array greedy
---

> 각 배열이 오름차순으로 정렬된 m개의 배열에서 두 요소의 최대 절대값 구하기

- [624. Maximum Distance in Arrays](https://leetcode.com/problems/maximum-distance-in-arrays/)

```java
class Solution {
    
    // 각 배열이 오름차순으로 정렬된 m개의 배열이 제공
    // T: O(n)
    public int maxDistance(List<List<Integer>> arrays) {
        int min = arrays.get(0).get(0);
        int max = arrays.get(0).get(arrays.get(0).size()-1);

        int result = Integer.MIN_VALUE;

        for (int i=1; i<arrays.size(); i++) {
            int curmax = arrays.get(i).get(arrays.get(i).size()-1);
            int curmin = arrays.get(i).get(0);
            result = Math.max(result, Math.abs(max - curmin));
            result = Math.max(result, Math.abs(min - curmax));

            max = Math.max(max, curmax);
            min = Math.min(min, curmin);
        }

        return result;
    }
}
```