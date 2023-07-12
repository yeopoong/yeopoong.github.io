---
layout: post
published: false
title: "Linked List"
categories: interview
tags: topics linked-list
---

## Approach

The entry point into a linked list is called the head of the list.

연결 리스트의 통합은 세가지 조건을 체크해서 처리한다(>, <, ==)


## Sentinel Head
To handle the last use case, one needs so called Sentinel Node. Sentinel nodes are widely used for trees and linked lists as pseudo-heads, pseudo-tails, etc. They are purely functional, and usually don't hold any data. Their main purpose is to standardize the situation to avoid edge case handling.

```java
// 처음에 어떤 노드가 될지 모르므로 더미 노드를 생성한다.
ListNode dumy = new ListNode();

// 헤드 포인터를 리턴해야 하므로 작업 포인트 노드 변수를 선언한다.
ListNode p = dumy;

//...

// 헤드 리턴
return dumy.next;
```

## 리스트 주요 연산

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

Swap List
```java
ListNode reverse(ListNode prev, ListNode node) {
    // 더 이상 다음노드가 없으면 종료(헤드노드가 된다.)
    if (node == null) return prev;

    ListNode next = node.next;
    node.next = prev;

    return reverse(node, next);
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

## Questions

[Easy]
- [21. Merge Two Sorted Lists](/interview/2023/04/12/merge-two-sorted-lists/)
- [83. Remove Duplicates from Sorted List](/interview/2023/07/04/remove-duplicates-from-sorted-list/)
- [141. Linked List Cycle](/interview/2023/06/16/linked-list-cycle/)
- [160. Intersection of Two Linked Lists](/interview/2023/04/26/intersection-of-two-linked-lists/)
- [203. Remove Linked List Elements](/interview/2023/07/04/remove-linked-list-elements/)
- [206. Reverse Linked List](/interview/2023/04/26/reverse-linked-list/)
- [876. Middle of the Linked List](/interview/2023/06/26/middle-of-the-linked-list/)
- [1474. Delete N Nodes After M Nodes of a Linked List](/interview/2023/06/30/delete-n-nodes-after-m-nodes-of-a-linked-list/)

[Medium]
- [2. Add Two Numbers](/interview/2023/04/09/add-two-numbers/)
- [19. Remove Nth Node From End of List](/interview/2023/06/22/remove-nth-node-from-end-of-list/)
- [24. Swap Nodes in Pairs](/interview/2023/05/06/swap-nodes-in-pairs/)
- [61. Rotate List](/interview/2023/04/10/rotate-list/)
- [82. Remove Duplicates from Sorted List II](/interview/2023/06/22/remove-duplicates-from-sorted-list-ii/)
- [86. Partition List](/interview/2023/06/23//partition-list/)
- [92. Reverse Linked List II](/interview/2023/05/20/reverse-linked-list-ii.md)
- [138. Copy List with Random Pointer](/interview/2023/04/13/copy-list-with-random-pointer/)
- [146. LRU Cache](/interview/2023/04/26/lru-cache/)
- [148. Sort List](/interview/2023/04/26/sort-list/)
- [328. Odd Even Linked List](/interview/2023/04/26/odd-even-linked-list/)
- [369. Plus One Linked List](/interview/2023/05/08/plus-one-linked-list/)
- [430. Flatten a Multilevel Doubly Linked List](/interview/2023/04/26/flatten-a-multilevel-doubly-linked-list/)
- [445. Add Two Numbers II](/interview/2023/04/26/add-two-numbers-ii/)
- [2095. Delete the Middle Node of a Linked List](/interview/2023/05/27/linked-list-cycle/)
- [2130. Maximum Twin Sum of a Linked List](/interview/2023/06/11/maximum-twin-sum-of-a-linked-list/)

[Hard]
- [23. Merge k Sorted Lists](/interview/2023/04/26/merge-k-sorted-lists/)