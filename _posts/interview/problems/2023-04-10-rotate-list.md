---
layout: post
published: true
title: "61. Rotate List"
categories: interview
tags: interview linked-list
---

- [61. Rotate List](https://leetcode.com/problems/rotate-list/)

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
    
    // 연결된 목록의 헤드가 주어지면 목록을 오른쪽으로 k만큼 회전
    // O(n)
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }
        
        int length = getLength(head);
        
        k = k % length;
        
        // Move to the pivot and rotate(피봇노드가 마지막 노드가 된다)
        ListNode curr = head;
        for (int i = 1; i < length - k; i++) {
            curr = curr.next;
        } 
        
        // 피봇노드의 다음노드가 시작노드가 된다.
        head = curr.next;
        
        // 피봇노드를 마지막 노드로 만든다.
        curr.next = null;
        
        return head;
    }
    
    // Get length
    public int getLength(ListNode head) {
        int length = 1;
        
        ListNode tail = head;
        while (tail.next != null) {
            tail = tail.next;
            length += 1;
        }
        
        // Tail to the front
        tail.next = head;
        
        return length;
    }
}
```