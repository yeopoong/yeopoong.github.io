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

두개의 노드를 선언하고 하나의 노드를 N 노드 만큼 앞서가게 만들어서 해당 노드가 마지막 노드에 도달하면 정상 노드의 포인터를 한칸 건너뛰게 만든다.

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

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        slow = fast = dummy
        
        # let the fast pointer move n steps ahead of the slow pointer
        for _ in range(n + 1): 
            fast = fast.next
        
        while fast:
            fast = fast.next
            slow = slow.next
            
        slow.next = slow.next.next
        
        return dummy.next
```
