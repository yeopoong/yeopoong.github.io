---
layout: post
published: true
title: "369. Plus One Linked List"
categories: interview
tags: medium linked-list
---

> 연결된 숫자 목록으로 표시되는 음이 아닌 정수에 1을 더하기

[369. Plus One Linked List](https://leetcode.com/problems/plus-one-linked-list/)

![](https://leetcode.com/problems/plus-one-linked-list/Figures/369/diff.png)

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
    
    // 리스트로 표현된 숫자에 1 더하기
    // 숫자가 9이면 앞자리가 하나 증가하고 9는 0으로 바뀐다.
    // [1,2,9]
    // T: O(n)
    public ListNode plusOne(ListNode head) {
        
        ListNode sentinel = new ListNode();
        ListNode notNine = sentinel;
        
        sentinel.next = head;

        // find the rightmost not-nine digit
        while (head != null) {
            if (head.val != 9) {
                notNine = head;
            }
            head = head.next;
        }

        // increase this rightmost not-nine digit by 1
        notNine.val++;
        notNine = notNine.next;

        // set all the following nines to zeros
        while (notNine != null) {
            notNine.val = 0;
            notNine = notNine.next;
        }
        

        // 가장 앞자리가 증가했는지 체크해서 리턴한다: [9,9,9] -> [1,0,0,0]
        return sentinel.val != 0 ? sentinel : sentinel.next;
    }
}
```
