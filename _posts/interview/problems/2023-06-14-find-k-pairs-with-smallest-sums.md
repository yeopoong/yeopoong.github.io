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
        // 1. Create a min heap
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> (a[0] + a[1]) - (b[0] + b[1]));
        
        // 2. Add all the pairs to the min heap
        for (int i = 0; i < nums1.length && i < k; i++) {
            minHeap.offer(new int[]{nums1[i], nums2[0], 0});
        }
        
        // 3. Create a result list
        List<List<Integer>> result = new ArrayList<>();
        
        // 4. Iterate until k
        while (k-- > 0 && !minHeap.isEmpty()) {
            // 5. Get the top element from the min heap
            int[] current = minHeap.poll();
            
            // 6. Add the pair to the result list
            result.add(Arrays.asList(current[0], current[1]));
            
            // 7. If the index of the second element is less than the length of the second array
            if (current[2] < nums2.length - 1) {
                // 8. Add the next pair to the min heap
                minHeap.offer(new int[]{current[0], nums2[current[2] + 1], current[2] + 1});
            }
        }
        
        return result;
    }
}
}
```
