---
layout: post
published: true
title: "19. Remove Nth Node From End of List"
categories: interview
tags: medium linked-list two-pointers
---

> 연결된 목록의 헤드가 주어지면 목록 끝에서 n번째 노드를 제거하고 헤드를 반환

[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

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
    // 끝에서 N번째 노드 제거
    public ListNode removeNthFromEnd(ListNode head, int n) {
        
        // 더미노드(헤드를 리턴해야 하기 때문에 필요하고 헤드노드가 어떤 노드가 될지 모르기 때문에 더미노드로 선언)
        ListNode start = new ListNode();
        
        // 시작노드는 헤드노드를 가리킨다.
        start.next = head;
        
        ListNode slow = start, fast = start;

        // Move fast in front so that the gap between slow and fast becomes n
        for (int i = 1; i <= n + 1; i++)   {
            fast = fast.next;
        }
        
        // Move fast to the end, maintaining the gap
        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
        }
        
        // Skip the desired node
        slow.next = slow.next.next;
        
        return start.next;
    }
}
```
