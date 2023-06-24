---
layout: post
published: true
title: "977. Squares of a Sorted Array"
categories: interview
tags: easy two-pointers
---

> 오름차순으로 정렬된 정수 배열 nums가 주어지면 오른차순으로 정렬된 각 숫자의 제곱 배열을 반환

[977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

```java
class Solution {
    // 오름차순으로 정렬된 배열의 제곱
    // T: O(n)
    public int[] sortedSquares(int[] nums) {
        int[] answer = new int[nums.length];
        
        int left = 0, right = nums.length - 1;
        int leftAbs = 0, rightAbs = 0;
        
        // 반대 방향으로 부정적인 부분을 반복하고 정방향으로 긍정적인 부분을 반복
        // 결국, 두개의 감소하는 배열을 머지하는 것이다.
        while (left <= right) {
            leftAbs = Math.abs(nums[left]);
            rightAbs = Math.abs(nums[right]);
            
            // 절대값을 비교해서 큰값을 뒤에서 부터 저장한다.
            if (leftAbs > rightAbs) {
                answer[right - left] = leftAbs * leftAbs;
                left += 1;
            } else {
                answer[right - left] = rightAbs * rightAbs;
                right -= 1;
            }
        }
        
        return answer;
    }
}
```
