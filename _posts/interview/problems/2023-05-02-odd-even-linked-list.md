---
layout: post
published: true
title: "328. Odd Even Linked List"
categories: interview
tags: linked-list
---

> 단일 연결 리스트의 헤드가 주어지면 홀수 인덱스를 가진 모든 노드와 짝수 인덱스를 가진 노드를 함께 그룹화하고 재정렬된 리스트를 반환

- [328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)

![](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

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
    // O(1), O(n)
    public ListNode oddEvenList(ListNode head) {
        if (head == null) return null;
        
        ListNode odd = head; 
        ListNode even = head.next; 
        
        // 나중에 Odd -> Even 연결하기 위해서 저장
        ListNode evenHead = even;
        
        while (even != null && even.next != null) {
            // odd 포인터 변경시키고 위치 이동
            odd.next = even.next;
            odd = odd.next;
            
            // even 포인터 변경시키고 위치 이동
            even.next = odd.next;
            even = even.next;
        }
        
        // followd by the nodes with even indices
        odd.next = evenHead;
        
        return head;
    }
}
```
