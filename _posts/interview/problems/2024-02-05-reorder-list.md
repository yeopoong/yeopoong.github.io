---
layout: post
published: true
title: "143. Reorder List"
categories: interview
tags: medium linkedlist
---

> 다음 형식이 되도록 목록을 재정렬합니다.
> L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …

[143. Reorder List](https://leetcode.com/problems/reorder-list/)

![](https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg)

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
//This question is a combination of Reverse a linked list I & II. It should be pretty straight forward to do it in 3 steps :)
class Solution {

    // 리스트 재정렬
    public void reorderList(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;
        
        // 1. find middle(= slow)
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // 2. reverse second half: 1->2->3->4->5->6 to 1->2->3 -> 6->5->4
        ListNode second = slow.next;
        ListNode prev = null;
        
        while (second != null) {
            ListNode next = second.next;
            second.next = prev;
            prev = second;
            second = next;
        }
        
        // 3. merge two halfts: 1->2->3->6->5->4 to 1->6->2->5->3->4
        ListNode first = head;
        second = prev;

        slow.next = null; // 머지후에 순환하지 않도록 널 처리 

        while (second != null) {
            ListNode tmp1 = first.next;
            ListNode tmp2 = second.next;
            
            first.next = second;
            second.next = tmp1;
            
            first = tmp1;
            second = tmp2;
        }
    }
}
```