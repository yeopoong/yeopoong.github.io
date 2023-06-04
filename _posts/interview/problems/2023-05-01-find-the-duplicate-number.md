---
layout: post
published: true
title: "287. Find the Duplicate Number"
categories: interview
tags: array two-pointers sort
---

> 정수 배열에서 반복되는 숫자를 반환

- [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

Two Pointer
```java
class Solution {
    // 중복 번호 찾기
    // T: O(n), S: O(1)
    public int findDuplicate(int[] nums) {
        if (nums.length > 1) {
            int slow = nums[0];
            int fast = nums[nums[0]];
            
            while (slow != fast) {
                slow = nums[slow];
                fast = nums[nums[fast]];
            }

            fast = 0;
            while (fast != slow) {
                fast = nums[fast];
                slow = nums[slow];
            }
            
            return slow;
        }
        
        return -1;
    }
}
```

Sort
```java
class Solution {
    // T: O(nlogn), S: O(logn)
    public int findDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i-1] == nums[i])
                return nums[i];
        }

        return -1;
    }
}
```

Set
```java
class Solution {
    // T: O(n), S: O(n)
    public int findDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<Integer>();
        
        for (int num : nums) {
            if (seen.contains(num)) {
                return num;
            } else {
                seen.add(num);
            }
        }

        return -1;
    }
}
```
