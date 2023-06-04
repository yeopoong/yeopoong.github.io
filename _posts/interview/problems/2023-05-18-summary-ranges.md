---
layout: post
published: true
title: "228. Summary Ranges"
categories: interview
tags: array
---

> 정렬된 배열의 모든 숫자를 정확히 포함하는 범위의 가장 작은 정렬 목록을 반환

- [228. Summary Ranges](https://leetcode.com/problems/summary-ranges/)

```java
class Solution {
    
    // 정렬된 배열의 모든 숫자를 정확히 포함하는 범위의 가장 작은 정렬 목록을 반환
    // T: O(n)
    public List<String> summaryRanges(int[] nums) {
        List<String> ranges = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
            int start = nums[i];
            
            // Keep iterating until the next element is one more than the current element.
            while (i + 1 < nums.length && nums[i] + 1 == nums[i + 1]) {
                i++;
            }

            // 연속된 값이 존재하면 구간 표현식으로 저장
            if (start != nums[i]) {
                ranges.add(start + "->" + nums[i]);
            // 아니면 숫자만 저장
            } else {
                ranges.add(String.valueOf(start));
            }
        }

        return ranges;
    }
}
```