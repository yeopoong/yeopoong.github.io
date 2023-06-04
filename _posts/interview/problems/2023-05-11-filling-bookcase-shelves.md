---
layout: post
published: true
title: "1105. Filling Bookcase Shelves"
categories: interview
tags: array
---

> 선반을 배치한 후 전체 책장이 될 수 있는 최소 높이를 반환

- [1105. Filling Bookcase Shelves](https://leetcode.com/problems/filling-bookcase-shelves/)

![](https://assets.leetcode.com/uploads/2019/06/24/shelves.png)

```java
class Solution {
    public int minHeightShelves(int[][] books, int shelfWidth) {
        int[] dp = new int[books.length + 1];
        
        dp[0] = 0;
        
        for (int i = 1; i <= books.length; ++i) {
            int width = books[i-1][0];
            int height = books[i-1][1];
            dp[i] = dp[i-1] + height;
            for (int j = i - 1; j > 0 && width + books[j-1][0] <= shelfWidth; --j) {
                height = Math.max(height, books[j-1][1]);
                width += books[j-1][0];
                dp[i] = Math.min(dp[i], dp[j-1] + height);
            }
        }
        
        return dp[books.length];
    }
}
```