---
layout: post
published: true
title: "118. Pascal's Triangle"
categories: interview
tags: array dynamic-programming
---

> 정수 numRows가 주어지면 파스칼 삼각형의 첫 번째 numRows를 반환

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

- [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)

```java
class Solution {
    // Pascal's Triangle: 바로 위에 있는 두 숫자의 합으로 구성된 삼각형
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> triangle = new ArrayList<>();
        
        for (int i = 0; i < numRows; i++) {
            // 각 행의 리스트
            List<Integer> row =  new ArrayList<>();
            
            for (int j = 0; j < i + 1; j++) {
                // 처음값과 마지막 값은 1
                if (j == 0 || j == i) {
                    row.add(1);
                } else {
                    // 이전 열(i-1)의 두 컬럼(j-1, j) 값을 더한 값이 현재 값이 된다.
                    row.add(triangle.get(i-1).get(j-1) + triangle.get(i-1).get(j));
                }
            }
            
            triangle.add(row);
        }
        
        return triangle;
    }
}
```