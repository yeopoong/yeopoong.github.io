---
layout: post
published: true
title: "2095. Delete the Middle Node of a Linked List"
categories: interview
tags: problems linked-list two-pointers
---

> 연결된 목록의 헤드가 주어집니다. 중간 노드를 삭제하고 수정된 연결 목록의 헤드를 반환

- [2095. Delete the Middle Node of a Linked List](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/)

![](https://assets.leetcode.com/uploads/2021/11/16/eg1drawio.png)

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
    
    // 연결된 목록의 중간 노드 삭제
    // T: O(n)
    public ListNode deleteMiddle(ListNode head) {
        // Edge case: return nullptr if there is only one node.
        if (head.next == null) return null;
        
        // Initialize two pointers, 'slow' and 'fast'.
        ListNode slow = head, fast = head.next.next;
        
        // Let 'fast' move forward by 2 nodes, 'slow' move forward by 1 node each step.
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // When 'fast' reaches the end, remove the next node of 'slow' and return 'head'.
        slow.next = slow.next.next;
        
        return head;
    }
}
```