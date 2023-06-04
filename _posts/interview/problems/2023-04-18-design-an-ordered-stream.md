---
layout: post
published: true
title: "430. Flatten a Multilevel Doubly Linked List"
categories: interview
tags: design
---

> 정렬된 스트림 설계

- [1656. Design an Ordered Stream](https://leetcode.com/problems/design-an-ordered-stream/)

```java
class OrderedStream {

    int ptr;
    String[] res;
    
    public OrderedStream(int n) {
        ptr = 0;
        res = new String[n];
    }
    
    // 삽입할 때마다 값의 청크(목록)를 반환하여 ID의 오름차순으로 값을 반환
    // 모든 청크를 연결하면 정렬된 값 목록이 생성됩니다.
    public List<String> insert(int id, String value) {
        List<String> list = new ArrayList<>();
        
        res[id - 1] = value;
        while (ptr < res.length && res[ptr] != null) {
            list.add(res[ptr]);
            ptr++;
        }
        
        return list;
    }
}

/**
 * Your OrderedStream object will be instantiated and called as such:
 * OrderedStream obj = new OrderedStream(n);
 * List<String> param_1 = obj.insert(idKey,value);
 */
```