---
layout: post
published: true
title: "83. Remove Duplicates from Sorted List"
categories: interview
tags: easy linked-list
---

> 정렬된 연결 목록의 헤드가 주어지면 각 요소가 한 번만 나타나도록 모든 중복 항목을 삭제

[83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

![](https://assets.leetcode.com/uploads/2021/01/04/list1.jpg)

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
    // 정렬되어 있으므로 연속된 두 노드만 비교하면서 처리하면 된다.
    public ListNode deleteDuplicates(ListNode head) {
        ListNode cur = head;
        
        // 중복 체크를 해야 하므로 다음노드가 존재할때 까지 반복한다.
        while (cur != null && cur.next != null) {
            if (cur.val == cur.next.val) {
                // 다음노드만 건너뛴다(다음 다음노드도 중복일 수 있으므로 현재 포인터는 아직 변경하지 않는다)
                cur.next = cur.next.next;
            } else {
                // 현재 포인터를 다음으로 변경한다.
                cur = cur.next;
            }
        }
        
        return head;
    }
}
```