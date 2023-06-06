---
layout: post
published: false
title: "Two Pointer"
categories: interview
tags: topics two-pointers
---

## Two Pointer

배열이 정렬되어 있으면 고려한다.

reverse array
```java
public void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```

[Easy]
- [125. Valid Palindrome](/interview/2023/02/20/valid-palindrome/)
- [26. Remove Duplicates from Sorted Array](/interview/2023/05/21/remove-duplicates-from-sorted-array/)
- [28. Find the Index of the First Occurrence in a String](/interview/2023/05/01/find-the-index-of-the-first-occurrence-in-a-string/)
- [121. Best Time to Buy and Sell Stock](/interview/2023/02/22/best-time-to-buy-and-sell-stock/)
- [283. Move Zeroes](/interview/2023/05/21/move-zeroes/)
- [344. Reverse String](/interview/2023/05/21/reverse-string/)
- [392. Is Subsequence](/interview/2023/05/21/is-subsequence/)
- [1768. Merge Strings Alternately](/interview/2023/05/21/merge-strings-alternately/)
- [643. Maximum Average Subarray I](/interview/2023/05/21/maximum-average-subarray-i/)
- [345. Reverse Vowels of a String](/interview/2023/05/22/reverse-vowels-of-a-string/)

[Medium]
- [15. 3Sum](/interview/2023/04/05/3sum/)
- [16. 3Sum Closest](/interview/2023/05/08/3sum-closest/)
- [31. Next Permutation](/interview/2023/05/08/next-permutation/)
- [61. Rotate List](/interview/2023/04/10/rotate-list/)
- [75. Sort Colors](/interview/2023/04/16/sort-colors/)
- [287. Find the Duplicate Number](/interview/2023/05/01/find-the-duplicate-number/)
- [11. Container With Most Water](/interview/2023/05/21/container-with-most-water/)
- [5. Longest Palindromic Substring](/interview/2023/05/21/longest-palindromic-substring)
- [658. Find K Closest Elements](problems/2023-05-21-find-k-closest-elements.md)
- [28. Find the Index of the First Occurrence in a String](/interview/2023/05/21/find-the-index-of-the-first-occurrence-in-a-string/)
- [148. Sort List](/interview/2023/05/21/sort-list/)
- [1004. Max Consecutive Ones III](/interview/2023/05/21/max-consecutive-ones-iii/)
- [281. Zigzag Iterator](/interview/2023/05/21/zigzag-iterator/)
- [1229. Meeting Scheduler](/interview/2023/05/21/meeting-scheduler/)
- [131. Palindrome Partitioning](/interview/2023/05/21/palindrome-partitioning/)
- [253. Meeting Rooms II](/interview/2023/04/18/meeting-rooms-ii/)
- [209. Minimum Size Subarray Sum](/interview/2023/05/21/minimum-size-subarray-sum/)
- [1498. Number of Subsequences That Satisfy the Given Sum Condition](/interview/2023/05/21/number-of-subsequences-that-satisfy-the-given-sum-condition/)
- [723. Candy Crush](/interview/2023/05/21/candy-crush/)
- [443. String Compression](/interview/2023/05/21/string-compression/)
- [80. Remove Duplicates from Sorted Array II](/interview/2023/05/21/remove-duplicates-from-sorted-array-ii/)
- [167. Two Sum II - Input Array Is Sorted](/interview/2023/05/18/two-sum-ii-input-array-is-sorted/)
- [2095. Delete the Middle Node of a Linked List](/interview/2023/05/27/linked-list-cycle/)
- [1868. Product of Two Run-Length Encoded Arrays](/interview/2023/05/29/product-of-two-run-length-encoded-arrays/)

[Hard]
- [42. Trapping Rain Water](/interview/2023/05/21/trapping-rain-water)