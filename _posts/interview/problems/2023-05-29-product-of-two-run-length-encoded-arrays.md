---
layout: post
published: true
title: "1868. Product of Two Run-Length Encoded Arrays"
categories: interview
tags: array two-pointers
---

> 인코딩된 두 배열 encoding1과 encoding2의 곱을 반환

- [1868. Product of Two Run-Length Encoded Arrays](https://leetcode.com/problems/product-of-two-run-length-encoded-arrays/)

```java
class Solution {
    
    // Two Pointer
    // encoding1.length == encoding2.length
    // O(n)
    public List<List<Integer>> findRLEArray(int[][] encoded1, int[][] encoded2) {
        List<List<Integer>> res = new ArrayList<>();
        
        int p1 = 0, p2 = 0;
        while (p1 < encoded1.length) {
            int len = Math.min(encoded1[p1][1], encoded2[p2][1]);
            int prd = encoded1[p1][0] * encoded2[p2][0];
            
            // 이전값(리스트의 마지막 세크먼트)이 현재값과 같으면 길이를 더해준다.
            if (res.size() > 0 && res.get(res.size()-1).get(0) == prd) { 
                res.get(res.size()-1).set(1, res.get(res.size()-1).get(1) + len); //update previous prd in res instead of adding a new one
            } else {
                // 처음에는 그냥 결과 리스트에 추가한다.
                res.add(Arrays.asList(prd, len));
            }
            
			encoded1[p1][1] -= len;
            encoded2[p2][1] -= len;
            
            if (encoded1[p1][1] == 0) p1++;
            if (encoded2[p2][1] == 0) p2++;
        }
        
        return res;
    }
}
```