---
layout: post
published: true
title: "740. Delete and Earn"
categories: interview
tags: problems dynamic-programming
---

> 정수 배열에서 다음 연산을 몇 번 적용하여 얻을 수 있는 최대 포인트 수를 반환
> - nums[i]를 선택하고 삭제하여 nums[i] 포인트를 얻습니다.  
> - nums[i] - 1과 같은 모든 요소와 nums[i] + 1과 같은 모든 요소를 ​​삭제

- [740. Delete and Earn](https://leetcode.com/problems/delete-and-earn/)

```java
class Solution {
    public int deleteAndEarn(int[] nums) {
        int n = 10001;
        
        int[] values = new int[n];
        
        for (int num : nums) {
            values[num] += num;
        }

        int take = 0, skip = 0;
        
        for (int i = 0; i < n; i++) {
            int takei = skip + values[i];
            int skipi = Math.max(skip, take);
            take = takei;
            skip = skipi;
        }
        
        return Math.max(take, skip);
    }
}
```
