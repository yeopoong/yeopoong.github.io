---
layout: post
published: true
title: "2. Add Two Numbers"
categories: interview
tags: interview linked-list
---

[Easy]

- [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

```java
class Solution {
    
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // 처음에 어떤 노드가 될지 모르므로 더미 노드를 생성한다.
        ListNode head = new ListNode();
        
        // 헤드 포인터를 리턴해야 하므로 작업 포인트 노드 변수를 선언한다.
        ListNode p = head;

        int sum = 0;
        // 오버플로우값도 다음노드에 추가해야 한다.
        while (l1 != null || l2 != null || sum != 0) {
            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }

            p.next = new ListNode(sum % 10);
            p = p.next;
            
            // 오버플로우
            sum = sum / 10;
        }
        
        return head.next;
    }
}
```