---
layout: post
published: true
title: "967. Numbers With Same Consecutive Differences"
categories: interview
tags: backtracking
---

> 두 개의 정수 n과 k가 주어지면 연속되는 두 자릿수 사이의 차이가 k이고 길이가 n인 모든 정수의 배열을 반환

- [967. Numbers With Same Consecutive Differences](https://leetcode.com/problems/numbers-with-same-consecutive-differences/)

```java
class Solution {
    
    ArrayList<Integer> al = new ArrayList<Integer>();
    
    // 두 개의 정수 n과 k가 주어지면 연속되는 두 자릿수 사이의 차이가 k이고 길이가 n인 모든 정수의 배열을 반환
    public int[] numsSameConsecDiff(int n, int k) {
        for(int i = 1 ; i < 10 ; i ++){
            permute(0,i,0,n,k);
        }
        int num[] = new int[al.size()];
        for(int i = 0 ; i < al.size(); i ++){
            num[i] = al.get(i);
        }
        return num;
    }
    
    public void permute(int num,int digit,int size,int n,int k){
        if(n == size){
            if(!al.contains(num)){
                al.add(num);
            }
            return;
        }
        if(digit < 10 && digit >= 0){
            num = (num*10) + digit;
            permute(num,digit+k,size+1,n,k);
            permute(num,digit-k,size+1,n,k);
        }
    }
}
```
