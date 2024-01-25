---
layout: post
published: true
title: "2422. Merge Operations to Turn Array Into a Palindrome"
categories: interview
tags: medium two-pointers
---

> 인접한 두 요소를 선택하고 합계로 변경하여 배열을 회문으로 바꾸는 데 필요한 최소 작업 수를 반환

[2422. Merge Operations to Turn Array Into a Palindrome](https://leetcode.com/problems/merge-operations-to-turn-array-into-a-palindrome/)

```java
class Solution {
    public int minimumOperations(int[] nums) {
        int cnt = 0;
        int n = nums.length;
        int left = nums[0], right = nums[n - 1];
        
        for (int i = 0, j = n - 1; i < j;) {
            // 양쪽끝의 두값이 동일할 경우
            if (left == right) {
                i++;
                j--;
                left = nums[i];
                right = nums[j];
            // 값이 다를경우 작은쪽을 머지한다.
            } else if (left < right) {
                i++;
                left += nums[i];
                cnt++;
            } else if (left > right) {
                j--;
                right += nums[j];
                cnt++;
            }
        }
        
        return cnt;
    }
}
```