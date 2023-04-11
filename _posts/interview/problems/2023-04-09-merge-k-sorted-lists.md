---
layout: post
published: true
title: "23. Merge k Sorted Lists"
categories: interview
tags: problems linked-list
---

[Easy]

- [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

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
    
    // 모든 연결 리스트를 하나의 정렬된 리스트로 병합
    // Merge Sort
    // T: O(nlogn), S: O(1)
    public ListNode mergeKLists(ListNode[] lists) {
        int size = lists.length;
        int interval = 1;

        while (interval < size) {
            for (int i = 0; i < size - interval; i += 2 * interval) {
                // 머지해서 앞에 리스트에 저장한다.
                lists[i] = merge(lists[i], lists[i + interval]);
            }

            // 2의 배수로 리스트가 줄어든다.
            interval *= 2;
        }

        return size > 0 ? lists[0] : null;
    }

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
}
'''

'''java
class Solution {

    // 모든 연결 리스트를 하나의 정렬된 리스트로 병합
    // Brute Force
    // T: O(nlogn), S: O(n)
    public ListNode mergeKLists(ListNode[] lists) {
        List<Integer> nodes = new ArrayList<>(); 
            
        // 모든 노드의 값을 리스트에 저장한다.
        for (ListNode l : lists) {
            while (l != null) {
                nodes.add(l.val);
                l = l.next;
            }
        }
        
        // 값을 정렬한다.
        Collections.sort(nodes);   
        
        ListNode head = new ListNode();
        // 시작값을 모르는 경우에는 더미 노드를 만들고 작업 노드를 헤드로 선언해서 작업한다.
        ListNode node = head;
        
        // 정렬된 값을 연결 리스트로 만든다.
        for (int x : nodes) {
            node.next = new ListNode(x);
            node = node.next;
        }
                
        return head.next;
    }
}
```