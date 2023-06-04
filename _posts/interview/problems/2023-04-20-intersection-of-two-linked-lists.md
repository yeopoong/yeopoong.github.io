---
layout: post
published: true
title: "160. Intersection of Two Linked Lists"
categories: interview
tags: linked-list two-pointers
---

> 두 단일 연결 리스트 headA와 headB의 헤드가 주어지면 두 리스트가 교차하는 노드를 반환  
> 두 개의 연결된 목록에 교차가 전혀 없으면 null을 반환

- [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    // https://leetcode.com/problems/intersection-of-two-linked-lists/discuss/49785/Java-solution-without-knowing-the-difference-in-len!/165648
    // 두 연결 리스트의 교집합
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode a = headA;
        ListNode b = headB;

        //if a & b have different len, then we will stop the loop after second iteration
        while (a != b) {
            //for the end of first iteration, we just reset the pointer to the head of another linkedlist
            a = (a == null) ? headB : a.next;
            b = (b == null) ? headA : b.next;    
        }

        return b;
    }
}
```