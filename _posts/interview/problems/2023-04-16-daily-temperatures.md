---
layout: post
published: true
title: "739. Daily Temperatures"
categories: interview
tags: problems stack array monotonic-stack
---

> 더 따뜻한 온도를 얻기 위해 기다려야 하는 일수  
> A monotonic stack is simply a stack where the elements are always in sorted order. 

- [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

```java
class Solution {
    
    // 더 따뜻한 온도를 얻기 위해 기다려야 하는 일수
    // Monotonic Stack:  A monotonic stack is simply a stack where the elements are always in sorted order. 
    // O(n)
    public int[] dailyTemperatures(int[] temperatures) {
        int[] ans = new int[temperatures.length];

        // * 반복을 한번만 하기위해서 날짜값을 저장해 둔다(가장 최근일자 저장)
        Stack<Integer> stack = new Stack<>();

        for (int currDay = 0, prevDay = 0; currDay < temperatures.length; currDay++) {
            // 현재온도가 스택의 값보다 크면 
            while (!stack.isEmpty() && temperatures[currDay] > temperatures[stack.peek()]) {
                // 스택에서 제거하고
                prevDay = stack.pop();
                // 날짜값의 차이를 결과에 저장한다. 
                ans[prevDay] = currDay - prevDay;
            }
            stack.add(currDay);
        }

        return ans;
    }
}
```