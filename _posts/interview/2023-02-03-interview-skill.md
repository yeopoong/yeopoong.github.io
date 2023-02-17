---
layout: post
published: false
title: "[Interview Skill] Coding Interview Skill"
categories: interview
tags: interview 
---

## Coding Interview Skill
> 코딩 인터뷰는 문제를 푸는 것이 목적이 아니다.

## Read the question
## Repeat the question out loud
## Understand given examples
## Ask about input & output data (array sized, value ranges, possible invalid inputs)
## Ask about initial time / space constraints
## Write your own simple example and edge cases
## Propose brute force solution
## Use extra space to find more optimal solution
## Try to find even more solutions
## Explain tradeoffs and time / space complexity
## Choose one approach
## Pseudo code
## Code solution
## Debug skill

## Pattern

If input array is sorted then
- Binary search
- Two pointers

If asked for all permutations/subsets then
- Backtracking

If given a tree then
- DFS
- BFS

If given a graph then
- DFS
- BFS

If given a linked list then
- Two pointers

If recursion is banned then
- Stack

If must solve in-place then
- Swap corresponding values
- Store one or more different values in the same pointer

If asked for maximum/minimum subarray/subset/options then
- Dynamic programming

If asked for top/least K items then
- Heap
- QuickSelect

If asked for common strings then
- Map
- Trie

Else
- Map/Set for O(1) time & O(n) space
- Sort input for O(nlogn) time and O(1) space

https://seanprashad.com/leetcode-patterns/


## Code Spat

Length
```
left = 3, right = 1 (0,1,2,3)
len = right - left + 1;
```


SWAP

- Array
```java
t = a, a = b, b = t;
```

- List
```java
p -> c -> n (이전: p, 현재: c, 다음: n)
n = c.next, c.next = p;
p = c, c = n;
```

- Tree
```
```


Binary Search
```java
// 이진검색
int left = 0, right = arr.length - 1;

while (left <= right) {
    int pivot = left + (right - left) / 2;
    if (arr[pivot] > target) {
        right = pivot - 1;
    } else if (arr[pivot] < target) {
        left = pivot + 1;
    } else {
        return true;
    }
}
```

Tree Travesal