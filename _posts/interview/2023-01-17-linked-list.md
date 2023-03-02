---
layout: post
published: false
title: "Linked List"
categories: interview
tags: interview linked-list
---

## Linked List

Merge List
```java
private ListNode merge(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {
            curr.next = l1;
            l1 = l1.next;
        } else {
            curr.next = l2;
            l2 = l2.next;
        }

        curr = curr.next;
    }

    if (l1 != null) {
        curr.next = l1;
    } else {
        curr.next = l2;
    }

    return dummy.next;
}
```


[Easy]
- [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
- [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

[Medium]
- [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
- [61. Rotate List](https://leetcode.com/problems/rotate-list/)
- [148. Sort List](https://leetcode.com/problems/sort-list/)
- [430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)

[Hard]
- [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)