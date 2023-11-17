---
layout: post
published: true
title: "1474. Delete N Nodes After M Nodes of a Linked List"
categories: interview
tags: easy linked-list
---

> 연결된 목록을 순회하고 다음과 같은 방법으로 일부 노드를 제거한 후 수정된 목록의 헤드를 반환  
> - 헤드를 현재 노드로 시작  
> - 현재 노드부터 시작하는 첫 번째 m 노드를 유지  
> - 다음 n 노드 제거  
> - 목록 끝에 도달할 때까지 2단계와 3단계를 계속 반복

[1474. Delete N Nodes After M Nodes of a Linked List](https://leetcode.com/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/)

![](https://assets.leetcode.com/uploads/2020/06/06/sample_1_1848.png)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    
    public ListNode deleteNodes(ListNode head, int m, int n) {
        ListNode currentNode = head;
        ListNode lastMNode = head;
        
        while (currentNode != null) {
            // initialize mCount to m and nCount to n
            int mCount = m, nCount = n;
            // traverse m nodes
            while (currentNode != null && mCount != 0) {
                lastMNode = currentNode;
                currentNode = currentNode.next;
                mCount--;
            }
            // traverse n nodes
            while (currentNode != null && nCount != 0) {
                currentNode = currentNode.next;
                nCount--;
            }
            // delete n nodes
            lastMNode.next = currentNode;
        }
        
        return head;
    }
}
```