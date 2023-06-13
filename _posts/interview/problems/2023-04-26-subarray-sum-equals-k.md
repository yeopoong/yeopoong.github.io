---
layout: post
published: true
title: "560. Subarray Sum Equals K"
categories: interview
tags: medium array hashmap prefix-sum
---

> 정수 nums 배열과 정수 k가 주어지면 합계가 k인 하위 배열의 총 개수를 반환

[560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

```java
class Solution {
    // return the total number of subarrays whose sum equals to k
    // 값이 존재하는지 검색하기 위해서 해시맵자료 구조를 사용(중복해서 발생할 수 있기 때문에 발생 회수를 값으로 저장)
    // O(n)
    public int subarraySum(int[] nums, int k) {
        int count = 0; 
        
        Map<Integer, Integer> map = new HashMap<>();
        // 합이 K가 되는 경우
        map.put(0, 1);
        
        int sum = 0;
        for (int num: nums) {
            sum += num;
            // 보수값이 존재하면 그 경우의 수 만큼 더한다.
            if (map.containsKey(sum -k)) {
                count += map.get(sum - k); 
            }
            // 현재합을 맵에 추가한다.
            map.put(sum, map.getOrDefault(sum, 0) + 1); 
        }
        
        return count;
    }
}
```