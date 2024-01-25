---
layout: post
published: true
title: "21. Merge Two Sorted Lists"
categories: interview
tags: easy linked-list
---

> 두 개의 정렬된 연결 목록을 하나의 정렬된 목록으로 병합

[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

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
    //The entry point into a linked list is called the head of the list.
    //연결리스트의 진입점을 리스트의 헤드라고 부른다.
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        //the head of the merged linked list(첫번째 노드가 어떤노드가 될지 모르기 때문에 더미 노드로 시작해야 한다)
        ListNode result = new ListNode();
        
        //현재 노드에 대한 포인터
        ListNode curr = result;
        
        //각 리스트를 순서에 따라서 진행하면서 현재 노드 포인터가 가리키도록 한다.
        while (list1 != null && list2 != null) {
            // 작은값을 현재노드로 지정하고 다음으로 연결한다.
            if (list1.val < list2.val) {
                curr.next = list1;
                list1 = list1.next;
            } else {
                curr.next = list2;
                list2 = list2.next;
            }
            curr = curr.next;
        }
        
        if (list1 != null) curr.next = list1;
        if (list2 != null) curr.next = list2;
                
        return result.next;
    }
}
```