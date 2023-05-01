---
layout: post
published: true
title: "232. Implement Queue using Stacks"
categories: interview
tags: problems design stack queue
---

> 스택을 이용해서 큐 구현하기 (입출력 스택으로 순서를 뒤집을 수 있다)

- [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)

```java
class MyQueue {
    Stack<Integer> input;
    Stack<Integer> output;

    public MyQueue() {
        input = new Stack<>(); 
        output = new Stack<>(); 
    }
    
    public void push(int x) {
        input.push(x);
    }
    
    public int pop() {
        // 먼저 들어온 데이터를 꺼내야 한다.
        peek();
        return output.pop();
    }
    
    public int peek() {
        // 출력스택이 비어 있으면 입력스택에서 가져온다.
        if (output.empty()) {
            // 입력스택에서 마지막 데이터를 꺼내서 출력스택에 넣으면 순서를 뒤집을 수 있다.
            while (!input.empty()) {
                output.push(input.pop());
            }
        }
        
        return output.peek();
    }
    
    public boolean empty() {
        return input.empty() && output.empty();
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```
