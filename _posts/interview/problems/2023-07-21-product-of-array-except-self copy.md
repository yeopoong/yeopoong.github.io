---
layout: post
published: true
title: "108. Convert Sorted Array to Binary Search Tree"
categories: interview
tags: medium binary-search-tree
---

> 오름차순으로 정렬된 정수 배열이 주어지면 높이 균형 이진 검색 트리로 변환

[108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

![](https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    // 정렬된 배열을 이진 검색 트리로 변환
    // O(n), O(lon n): height of tree
    public TreeNode sortedArrayToBST(int[] num) {
        return helper(num, 0, num.length - 1);
    }

    // 이진탐색트리 중위순회하면 오름차순 정렬: 중앙값은 노드값, 작은값은 왼쪽 큰값은 오른쪽 노드로 만든다.
    public TreeNode helper(int[] num, int low, int high) {
        // 종료조건
        if (low > high) { 
            return null;
        }
        
        int mid = (low + high) / 2;
        
        // 중앙값은 루트 노드
        TreeNode node = new TreeNode(num[mid]);
        // 왼쪽노드는 작은값
        node.left = helper(num, low, mid - 1);
        // 오른쪽노드는 큰값
        node.right = helper(num, mid + 1, high);
        
        return node;
    }
}
```