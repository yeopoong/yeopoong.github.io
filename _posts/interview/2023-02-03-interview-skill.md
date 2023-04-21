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

List to Array
```java
List<int[]> list;
list.toArray(new int[list.size()][]);
```

```java
int[] num = new int[list.size()];

for (int i = 0 ; i < list.size(); i ++) {
    num[i] = list.get(i);
}       
```

```java
// ArrayList to Array Conversion
int[] arr = list.stream().mapToInt(i -> i).toArray();
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

Palindrome
```java
boolean isPalindrome(String s, int low, int high) {
    while (low < high) {
        if (s.charAt(low++) != s.charAt(high--)) return false;
    }
    return true;
}
```

Graph DFS
```java
// 연결된 모든 네크워크를 방문처리 한다.
int dfs(int c, List<Integer>[] graph, boolean[] visited) {
    if (visited[c]) return 0;
    
    visited[c] = true;
    
    for (int v : graph[c]) {
        dfs(v, graph, visited);
    }
    
    return 1;
}
```

Merge List
```java
 private ListNode merge(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {
            curr.next = l1;
            l1 = l1.next;
        } else {
            curr.next = l2;
            l2 = l2.next;
        }

        curr = curr.next;
    }

    if (l1 != null) {
        curr.next = l1;
    } else {
        curr.next = l2;
    }

    return dummy.next;
}
```

Merge Array
```java
 private int[] merge(int[] nums1, int[] nums2) {
    int[] merge = new int[nums1.length + nums2.length];
    
    int n1 = 0, n2 = 0;
    int p = 0;

    // 작은 노드를 P 노드에 연결 시킨다.
    while (n1 < nums1.length  && n2 < nums2.length) {
        if (nums1[n1] < nums2[n2]) {
            merge[p] = nums1[n1];
            n1++;
        } else {
            merge[p] = nums2[n2];
            n2++;
        }
        p++;
    }
    
    for (; n1 < nums1.length; n1++) merge[p++] = nums1[n1];
    for (; n2 < nums2.length; n2++) merge[p++] = nums2[n2];

    return merge; 
}
```