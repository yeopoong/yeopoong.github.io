---
layout: post
published: true
title: "203. Remove Linked List Elements"
categories: interview
tags: easy linked-list
---

> 연결된 목록의 헤드와 정수 값이 주어지면 Node.val == val인 연결된 목록의 모든 노드를 제거하고 새 헤드를 반환

[203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)

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
    // 연결리스트에서 노드 삭제
    // O(n)
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode();
        dummy.next = head;
        
        // 동일한 노드를 가리키고 있다.
        ListNode curr = dummy;
        
        // 마지막 노드까지 반복하면서 연결노드와 현재노드의 포인터를 변경한다.
        while (curr.next != null) {
            // 다음 노드의 값이 찾는값이면
            if (curr.next.val == val) {
                // 다음노드를 건너뛴다(단, 현재노드는 변경하지 않는다. 현재노드를 변경하면 해당 노드가 지워야 되는 노드일 경우 삭제할 방법이 없다).
                curr.next = curr.next.next;
            // 다음 노드의 값이 찾는값이 아니면
            } else {
                // 현재 노드를 다음 노드로 진행한다.
                curr = curr.next;
            }
        }
                
        return dummy.next;
    }
}
```