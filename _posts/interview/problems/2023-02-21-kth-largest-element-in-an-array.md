---
layout: post
published: true
title: "215. Kth Largest Element in an Array"
categories: interview
tags: heaps
---

> 정수 배열 nums와 정수 k가 주어지면 배열에서 k번째로 큰 요소를 반환

- [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```java
class Solution {

    int[] nums;
    int k;
    
    // 배열에서 K번째로 큰 요소
    // T: O(n)
    public int findKthLargest(int[] nums, int k) {
        this.nums = nums;
        this.k = nums.length - k;

        return quickSelect(0, nums.length - 1);
    }
    
    private int quickSelect(int left, int right) {
        int pivot = nums[right], p = left;

        for (int i = left; i < right; i++) {
            if (nums[i] <= pivot) {
                swap(p, i);
                p++;
            }
        }

        swap(p, right);

        if (p > k) return quickSelect(left, p - 1);
        else if (p < k) return quickSelect(p + 1, right);
        else return nums[p];
    }

    private void swap(int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```