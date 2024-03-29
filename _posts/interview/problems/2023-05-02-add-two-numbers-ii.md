---
layout: post
published: true
title: "445. Add Two Numbers II"
categories: interview
tags: linked-list
---

> 두 개의 음수가 아닌 정수를 나타내는 두 개의 비어 있지 않은 연결 목록이 제공됩니다. 가장 중요한 숫자가 먼저 나오고 각 노드에는 단일 숫자가 포함됩니다.  
> 두 숫자를 더하고 합계를 연결 리스트로 반환

- [445. Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/)

![](https://assets.leetcode.com/uploads/2021/04/09/sumii-linked-list.jpg)

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
    
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // find the length of both lists
        int n1 = 0, n2 = 0;
        
        ListNode curr1 = l1, curr2 = l2;
        
        while (curr1 != null) {
            curr1 = curr1.next; 
            ++n1;    
        }
        
        while (curr2 != null) {
            curr2 = curr2.next; 
            ++n2;    
        }
            
        // parse both lists
        // and sum the corresponding positions 
        // without taking carry into account
        // 3->3->3 + 7->7 --> 3->10->10--> 10->10->3
        curr1 = l1; 
        curr2 = l2;
        ListNode head = null;
        
        while (n1 > 0 && n2 > 0) {
            int val = 0;
            if (n1 >= n2) {
                val += curr1.val; 
                curr1 = curr1.next; 
                --n1;    
            }
            if (n1 < n2) {
                val += curr2.val; 
                curr2 = curr2.next;
                --n2;    
            }
                
            // update the result: add to front
            ListNode curr = new ListNode(val);
            curr.next = head;
            head = curr;    
        }

        // take the carry into account
        // to have all elements to be less than 10
        // 10->10->3 --> 0->1->4 --> 4->1->0
        curr1 = head;
        head = null;
        int carry = 0;
        while (curr1 != null) {
            // current sum and carry
            int val = (curr1.val + carry) % 10;
            carry = (curr1.val + carry) / 10;
            
            // update the result: add to front
            ListNode curr = new ListNode(val);
            curr.next = head;
            head = curr;

            // move to the next elements in the list
            curr1 = curr1.next;    
        }
        
        // add the last carry
        if (carry != 0) {
            ListNode curr = new ListNode(carry);
            curr.next = head;
            head = curr;    
        }

        return head;
    }
}
```
