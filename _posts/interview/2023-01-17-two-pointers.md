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
- [26. Remove Duplicates from Sorted Array](/interview/2023/05/21/remove-duplicates-from-sorted-array/)
- [28. Find the Index of the First Occurrence in a String](/interview/2023/05/01/find-the-index-of-the-first-occurrence-in-a-string/)
- [121. Best Time to Buy and Sell Stock](/interview/2023/02/22/best-time-to-buy-and-sell-stock/)
- [125. Valid Palindrome](/interview/2023/02/20/valid-palindrome/)
- [141. Linked List Cycle](/interview/2023/06/16/linked-list-cycle/)
- [283. Move Zeroes](/interview/2023/05/21/move-zeroes/)
- [344. Reverse String](/interview/2023/05/01/reverse-string/)
- [345. Reverse Vowels of a String](/interview/2023/05/22/reverse-vowels-of-a-string/)
- [392. Is Subsequence](/interview/2023/05/21/is-subsequence/)
- [643. Maximum Average Subarray I](/interview/2023/05/21/maximum-average-subarray-i/)
- [1768. Merge Strings Alternately](/interview/2023/05/21/merge-strings-alternately/)

[Medium]
- [5. Longest Palindromic Substring](/interview/2023/04/06/longest-palindromic-substring)
- [11. Container With Most Water](/interview/2023/05/21/container-with-most-water/)
- [15. 3Sum](/interview/2023/04/05/3sum/)
- [16. 3Sum Closest](/interview/2023/05/08/3sum-closest/)
- [19. Remove Nth Node From End of List](/interview/2023/06/22/remove-nth-node-from-end-of-list/)
- [28. Find the Index of the First Occurrence in a String](/interview/2023/05/21/find-the-index-of-the-first-occurrence-in-a-string/)
- [31. Next Permutation](/interview/2023/05/08/next-permutation/)
- [61. Rotate List](/interview/2023/04/10/rotate-list/)
- [75. Sort Colors](/interview/2023/04/16/sort-colors/)
- [80. Remove Duplicates from Sorted Array II](/interview/2023/05/21/remove-duplicates-from-sorted-array-ii/)
- [86. Partition List](/interview/2023/06/23//partition-list/)
- [131. Palindrome Partitioning](/interview/2023/05/21/palindrome-partitioning/)
- [148. Sort List](/interview/2023/05/21/sort-list/)
- [167. Two Sum II - Input Array Is Sorted](/interview/2023/05/18/two-sum-ii-input-array-is-sorted/)
- [186. Reverse Words in a String II](/interview/2023/06/19/reverse-words-in-a-string-ii/)
- [209. Minimum Size Subarray Sum](/interview/2023/05/21/minimum-size-subarray-sum/)
- [253. Meeting Rooms II](/interview/2023/04/18/meeting-rooms-ii/)
- [281. Zigzag Iterator](/interview/2023/05/21/zigzag-iterator/)
- [287. Find the Duplicate Number](/interview/2023/05/01/find-the-duplicate-number/)
- [443. String Compression](/interview/2023/05/21/string-compression/)
- [532. K-diff Pairs in an Array](/interview/2023/05/11/k-diff-pairs-in-an-array/)
- [658. Find K Closest Elements](problems/2023-05-21-find-k-closest-elements.md)
- [723. Candy Crush](/interview/2023/05/21/candy-crush/)
- [1004. Max Consecutive Ones III](/interview/2023/05/21/max-consecutive-ones-iii/)
- [1229. Meeting Scheduler](/interview/2023/05/21/meeting-scheduler/)
- [1498. Number of Subsequences That Satisfy the Given Sum Condition](/interview/2023/05/21/number-of-subsequences-that-satisfy-the-given-sum-condition/)
- [1868. Product of Two Run-Length Encoded Arrays](/interview/2023/05/29/product-of-two-run-length-encoded-arrays/)
- [2095. Delete the Middle Node of a Linked List](/interview/2023/05/27/linked-list-cycle/)
- [2130. Maximum Twin Sum of a Linked List](/interview/2023/06/11/maximum-twin-sum-of-a-linked-list/)

[Hard]
- [42. Trapping Rain Water](/interview/2023/05/21/trapping-rain-water)