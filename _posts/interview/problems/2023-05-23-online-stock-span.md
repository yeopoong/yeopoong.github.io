---
layout: post
published: true
title: "901. Online Stock Span"
categories: interview
tags: problems monotonic-stack design
---

> 일부 주식에 대한 일일 가격 시세를 수집하고 현재 날짜의 해당 주식 가격 범위를 반환하는 알고리즘을 설계합니다.  
> - 하루 동안의 주가 범위는 주가가 그날의 가격보다 작거나 같은 최대 연속 일수(당일부터 시작하여 뒤로)입니다.
> - Example: [100,80,60,70,60,75,86] -> [1,1,1,2,1,4,6]

- [901. Online Stock Span](https://leetcode.com/problems/online-stock-span/)

```java
class StockSpanner {

    Stack<int[]> stack; 
    
    public StockSpanner() {
        this.stack = new Stack<>();
    }
    
    public int next(int price) {
        int ans = 1;
        
        while (!stack.isEmpty() && stack.peek()[0] <= price) {
            ans += stack.pop()[1];
        }
        
        stack.push(new int[] {price, ans});
        
        return ans;
    }
}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner obj = new StockSpanner();
 * int param_1 = obj.next(price);
 */
```