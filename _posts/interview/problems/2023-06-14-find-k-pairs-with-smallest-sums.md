---
layout: post
published: true
title: "373. Find K Pairs with Smallest Sums"
categories: interview
tags: medium heap
---

> 오름차순으로 정렬된 두 개의 정수 배열에서 첫 번째 배열의 한 요소와 두 번째 배열의 한 요소로 구성된 쌍(u, v)을 정의하고 합계가 가장 작은 k 쌍을 반환

[373. Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/)

```java
class Solution {
    
    // 합계가 가장 작은 K 쌍 찾기
    // T: O(klogk)
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        List<List<Integer>> res = new ArrayList<>();
        
        PriorityQueue<int[]> q = new PriorityQueue<>(Comparator.comparingInt(a -> (a[0] + a[1])));
        
        int len1 = nums1.length, len2 = nums2.length;
        
        for (int i = 0; i < Math.min(len1, k); i++) q.offer(new int[]{nums1[i], nums2[0], 0});
        
        for (int i = 0; i < Math.min(len1 * len2, k); i++) {
            int[] cur = q.poll();
            
            List<Integer> pair = new ArrayList<>();
            pair.add(cur[0]);
            pair.add(cur[1]);
            
            res.add(pair);
            
            if (cur[2] < len2 - 1) { 
                int idx = cur[2] + 1;
                q.offer(new int[]{cur[0], nums2[idx], idx});
            }
        }
        
        return res;
    }
}
```
