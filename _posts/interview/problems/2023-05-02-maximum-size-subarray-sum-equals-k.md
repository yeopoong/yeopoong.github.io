---
layout: post
published: true
title: "325. Maximum Size Subarray Sum Equals k"
categories: interview
tags: array hashmap prefix-sum
---

> 정수 배열 nums와 정수 k가 주어지면 합계가 k인 하위 배열의 최대 길이를 반환

- [325. Maximum Size Subarray Sum Equals k](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/)

```java
class Solution {
    // 합계가 k인 하위 배열의 최대 길이
    // T: O(n)
    public int maxSubArrayLen(int[] nums, int k) {
        int max = 0;
        
        // 보수값의 인덱스를 맵에 저장한다.
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        
        int sum = 0;
        // 배열의 앞에서부터 시작해서 배열크기를 증가해가면서 체크
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];

            // 보수값을 맵에서 찾아보고 존재하면
            if (map.containsKey(sum - k)) {
                // 그 위치부터 현재까지의 배열의 크기를 최대 길이와 비교한다.
                max = Math.max(max, i - map.get(sum - k));
            }
            
            map.putIfAbsent(sum, i);
        }
        
        return max;
    }
}
```
