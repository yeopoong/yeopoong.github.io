---
layout: post
published: true
title: "141. Linked List Cycle"
categories: interview
tags: easy linked-list two-pointers
---

> 연결된 목록의 헤드가 주어지면 연결된 목록에 순환이 있는지 확인

[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow, fast;
        slow = fast = head;
        
        // 사이클이 존재하지 않으면 마지막 노드까지 진행하게 된다.
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            // 두 포인터가 만나면 사이클이 존재한다.
            if (slow == fast) {
                return true;
            }
        }
        
        return false;
    }
}
```
