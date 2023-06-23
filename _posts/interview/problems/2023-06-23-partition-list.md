---
layout: post
published: true
title: "86. Partition List"
categories: interview
tags: medium linked-list two-pointers
---

> 연결된 목록의 헤드와 값 x가 주어지면 x보다 작은 모든 노드가 x보다 크거나 같은 노드 앞에 오도록 분할

[86. Partition List](https://leetcode.com/problems/partition-list/)

![](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)

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
    
    // 리스트 분한
    // T: O(n)
    public ListNode partition(ListNode head, int x) {
        ListNode smallerHead = new ListNode(0);
        ListNode biggerHead = new ListNode(0);
        
        ListNode smaller = smallerHead; 
        ListNode bigger = biggerHead;
        
        while (head != null) {
            if (head.val < x) {
                smaller = smaller.next = head;
            } else {
                bigger = bigger.next = head;
            }
            head = head.next;
        }
        
        // no need for extra check because of fake heads
        smaller.next = biggerHead.next; // join bigger after smaller
        bigger.next = null; // cut off anything after bigger
        
        return smallerHead.next;
    }
}
```
