---
layout: post
published: true
title: "278. First Bad Version"
categories: interview
tags: easy binary-search
---

> 버전이 잘못된지 여부를 반환하는 API bool isBadVersion(version) 이 제공됩니다. 첫 번째 불량 버전을 찾는 기능을 구현하십시오. 

[278. First Bad Version](https://leetcode.com/problems/first-bad-version/)

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int pivot = 0, left = 1, right = n;
        
        while (left < right) {
            pivot = left + (right - left) / 2;
            //all the versions after a bad version are also bad
            if (isBadVersion(pivot)) {
                // 배드버전은 현재 버전일 수도 있다.
                right = pivot;
            } else { 
                // 배드버전은 더 뒤에 있다.
                left = pivot + 1;
            }
        }
        
        return left;
    }
}
```
