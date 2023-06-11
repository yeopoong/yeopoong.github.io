---
layout: post
published: true
title: "2130. Maximum Twin Sum of a Linked List"
categories: interview
tags: medium linked-list two-pointers 
---

> 길이가 짝수인 연결된 목록의 헤드가 주어지면 연결된 목록의 최대 쌍 합계를 반환

[2130. Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/)

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
    
    // 연결된 목록의 최대 트윈 합계
    // T: O(n)
    public int pairSum(ListNode head) {
        int maximumSum = 0;
        
        List<Integer> values = new ArrayList<>();
        ListNode current = head;
        
        while (current != null) {
            values.add(current.val);
            current = current.next;
        }

        int i = 0, j = values.size() - 1;
        while (i < j) {
            maximumSum = Math.max(maximumSum, values.get(i) + values.get(j));
            i++;
            j--;
        }

        return maximumSum;
    }
}
```
