---
layout: post
published: true
title: "1431. Kids With the Greatest Number of Candies"
categories: interview
tags: string
---

> 사탕을 가진 n명의 아이들의 배열에서 i번째 아이에게 extraCandies를 모두 제공한 후 모든 아이 중에서 가장 많은 수의 사탕을 갖게 되면 true이고 그렇지 않으면 false

- [1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)

```java
class Solution {
    
    // T: O(n)
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        List<Boolean> result = new ArrayList<>();
        
        // Find out the greatest number of candies among all the kids.
        int maxCandies = 0;
        
        for (int candy : candies) {
            maxCandies = Math.max(candy, maxCandies);
        }
        
        // For each kid, check if they will have greatest number of candies among all the kids.
        for (int candy : candies) {
            result.add(candy + extraCandies >= maxCandies);
        }

        return result;
    }
}
```

