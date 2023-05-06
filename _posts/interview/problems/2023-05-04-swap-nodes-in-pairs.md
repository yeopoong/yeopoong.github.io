---
layout: post
published: true
title: "1029. Two City Scheduling"
categories: interview
tags: problems linked-list
---

> 연결 목록이 주어지면 인접한 두 노드마다 교환하고 헤드를 반환

- [24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

~[](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)


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
    
    // 연결 목록이 주어지면 인접한 두 노드마다 교환하고 헤드를 반환합니다.
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode();
        
        // 처음에는 헤드를 가리킨다.
        dummy.next = head;
        
        // 작업노드
        ListNode node = dummy;

        // 두개의 노드가 존재하면 스왑한다.
        while (node.next != null && node.next.next != null) { 
            ListNode swap1 = node.next;
            ListNode swap2 = node.next.next;

            // 두 노드를 스왑한다.
            swap1.next = swap2.next;
            swap2.next = swap1;
            
            // 앞의 노드 포인터를 스왑된 노드로 변경하고
            node.next = swap2;
            // 작업노드를 변경한다.
            node = swap1;
        }

        return dummy.next;
    }
}
```
