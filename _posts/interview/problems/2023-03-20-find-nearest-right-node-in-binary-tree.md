---
layout: post
published: false
title: "1602. Find Nearest Right Node in Binary Tree"
categories: interview
tags: medium tree bfs
---

> 이진 트리의 루트와 트리의 노드 u가 주어지면 u의 오른쪽에 있는 동일한 수준에서 가장 가까운 노드를 반환  
> - 큐를 이용한 트리노드의 BFS 탐색

[1602. Find Nearest Right Node in Binary Tree](https://leetcode.com/problems/find-nearest-right-node-in-binary-tree/)

![](https://assets.leetcode.com/uploads/2020/09/24/p3.png)

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
    
    // 동일한 레벨에서 가장 가까운 오른쪽 노드를 반환
    // T: O(n), S: O(diameter)
    public TreeNode findNearestRightNode(TreeNode root, TreeNode u) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        // BFS
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            for (int i = 0; i < levelSize; i++) {
                TreeNode curr = queue.poll();
                // 노드를 찾으면 다음노드가 가장 가까운 노드이다. 
                if (curr == u) {
                    // 현재 노드가 마지막 노드이면 레벨에서 가장 오른쪽에 있는 노드이다.
                    if (i == levelSize - 1) {
                        return null;
                    } else {
                        return queue.poll();
                    }
                }

                // 왼쪽에서 오른쪽 순으로 큐에 넣는다. 
                if (curr.left != null) queue.offer(curr.left);
                if (curr.right != null) queue.offer(curr.right);
            }
        }
        
        return null;
    }
}
```