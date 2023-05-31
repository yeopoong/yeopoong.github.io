---
layout: post
published: true
title: "31. Next Permutation"
categories: interview
tags: problems array two-pointers
---

> 정수 nums의 배열이 주어지면 nums의 다음 순열을 찾습니다.

[31. Next Permutation](https://leetcode.com/problems/next-permutation/)


```java
class Solution {
    
    // 정수 nums의 배열이 주어지면 nums의 다음 순열을 찾습니다.
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        
        // 1 3(A) 5 4 4(B)
        // ->
        // 1 4 3 4 5
        // 뒤에서 탐색하면서 오름차순이 깨지는 인덱스를 확인 (A)
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        
        if (i >= 0) {
            int j = nums.length - 1;
            // 다시 뒤에서부터 탐색하면서 A 보다 큰 첫번째 인덱스를 확인 (B)
            while (nums[j] <= nums[i]) {
                j--;
            }
            // A와 B를 스왑
            swap(nums, i, j);
        }
        
        // A+1에서부터 끝까지 오름차순 정렬
        reverse(nums, i + 1);
    }

    private void reverse(int[] nums, int start) {
        int i = start, j = nums.length - 1;
        while (i < j) {
            swap(nums, i, j);
            i++;
            j--;
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
