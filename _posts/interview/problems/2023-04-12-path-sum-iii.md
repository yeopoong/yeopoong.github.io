---
layout: post
published: true
title: "437. Path Sum III"
categories: interview
tags: problems dfs tree
---

> 이진 트리의 루트와 정수 targetSum이 주어지면 경로를 따라 값의 합이 targetSum과 같은 경로의 수를 반환합니다.

- [437. Path Sum III](https://leetcode.com/problems/path-sum-iii/)

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
    int count;
    
    Map<Long, Integer> map = new HashMap<>();
    
    // 노드의 합이 targetSum 이 되는 경로의 수
    public int pathSum(TreeNode root, int targetSum) {
        map.put(0L, 1);
        dfs(root, 0, targetSum);
        
        return count;
    }
    
    public void dfs(TreeNode root, long currSum, int targetSum) {
        if (root == null) {
            return;
        }
        
        currSum += root.val;

        // 현재합에서 타켓에 대한 보수값이 존재하면 합이 타켓이 되는 경로가 존재한다.
        if (map.containsKey(currSum - targetSum)) {
            count += map.get(currSum - targetSum);
        }
        
        // 보수값 체크를 위해서 현재까지 합을 카운트 한다.
        map.put(currSum, map.getOrDefault(currSum, 0) + 1);
        dfs(root.left, currSum, targetSum);
        dfs(root.right, currSum, targetSum);
        map.put(currSum, map.get(currSum) - 1);
    }
}
```