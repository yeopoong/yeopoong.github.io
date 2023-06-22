---
layout: post
published: true
title: "82. Remove Duplicates from Sorted List II"
categories: interview
tags: medium linked-list two-pointers
---

> 정렬된 연결 목록의 헤드가 주어지면 원래 목록에서 고유한 번호만 남기고 중복 번호가 있는 모든 노드를 삭제

[82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

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
    // 정렬 리스트에서 중복 제거
    public ListNode deleteDuplicates(ListNode head) {
        
        // 노드가 변경될 수 있으므로 더미노드로 시작한다.
        ListNode dummy = new ListNode();
        
        // slow - track the node before the dup nodes, 
        ListNode slow = dummy;
        
        // fast - to find the last node of dups.
        ListNode fast = head;
        
        slow.next = fast;
        
        while (fast != null) {
            // find the last node of the dups.
            while (fast.next != null && fast.val == fast.next.val) {
                fast = fast.next;
            }
            
            // duplicates detected.
            if (slow.next != fast) {
                fast = fast.next;      // reposition the fast pointer 
                slow.next = fast;      // remove the dups
            // no dup, move down both pointer.
            } else { 
                slow = slow.next;
                fast = fast.next;
            }
        }
        
        return dummy.next;
    }
}
```
