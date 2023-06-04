---
layout: post
published: true
title: "88. Merge Sorted Array"
categories: interview
tags: two-pointers
---

> 정렬된 두 배열을 머지하면서 오름차순으로 정렬

- [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

```java
class Solution {
    // 정렬된 두 배열을 머지하면서 오름차순으로 정렬
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // * 뒤에서 부터 큰 숫자 순서로 넣는다(둘 중에 하나라도 처리할 값이 없으면 중지한다).
        while (m > 0 && n > 0) {
            nums1[m + n - 1] = Math.max(nums1[m - 1], nums2[n - 1]);
            // 큰값이 이동했으므로 인덱스를 감소 시킨다.
            if (nums1[m - 1] >= nums2[n - 1]) {
                m -= 1;
            } else {
                n -= 1;
            }
        }
        
        // 만약 num2가 남아있다면 num1보다 작은값 이므로 앞에서 부터 채우면 된다.
        if (n > 0) {
            for (int i = 0; i < n; i++) {
                nums1[i] = nums2[i];
            }
        }
    }
}
```