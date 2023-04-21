---
layout: post
published: false
title: "Linked List"
categories: interview
tags: interview linked-list
---

## Linked List

The entry point into a linked list is called the head of the list.

연결 리스트의 통합은 세가지 조건을 체크해서 처리한다(>, <, ==)

Sentinel Head

To handle the last use case, one needs so called Sentinel Node. Sentinel nodes are widely used for trees and linked lists as pseudo-heads, pseudo-tails, etc. They are purely functional, and usually don't hold any data. Their main purpose is to standardize the situation to avoid edge case handling.

Merge List
```java
private ListNode merge(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode();
    ListNode curr = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
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

```java
// remove node from list
private void remove(Node node) {
    Node prev = node.prev;
    Node next = node.next;

    prev.next = next;
    next.prev = prev;
}

// insert node at right
private void insert(Node node) {
    Node prev = this.right.prev;
    Node next = this.right;

    prev.next = node;
    next.prev = node;

    node.next = next;
    node.prev = prev;
}

private class Node {

    private int key;
    private int val;

    Node next;
    Node prev;

    public Node(int key, int val) {
        this.key = key;
        this.val = val;
    }
}
```

Get length
```java
public int getLength(ListNode head) {
    int length = 1;
    
    ListNode tail = head;
    while (tail.next != null) {
        tail = tail.next;
        length += 1;
    }
    
    return length;
}
```

[Easy]
- [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
- [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)
- [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
- [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

[Medium]
- [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
- [24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)
- [61. Rotate List](https://leetcode.com/problems/rotate-list/)
- [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)
- [146. LRU Cache](https://leetcode.com/problems/lru-cache/)
- [148. Sort List](https://leetcode.com/problems/sort-list/)
- [430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)

[Hard]
- [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)