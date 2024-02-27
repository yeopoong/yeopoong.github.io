---
layout: post
published: true
title: "299. Bulls and Cows"
categories: interview
tags: medium hashmap
---

> 비밀번호와 추측이 주어지면 추측에 대한 힌트를 반환
> - bulls: 추측에서 올바른 위치에 있는 숫자의 수
> - cows: 비밀 번호에 있지만 잘못된 위치에 있는 추측된 숫자

[299. Bulls and Cows](https://leetcode.com/problems/bulls-and-cows/)

```java
class Solution {
    public String getHint(String secret, String guess) {
        int bulls = 0;
        int cows = 0;
        
        // secret and guess consist of digits only.
        // For cows maintain an array that stores count of the number appearances in secret and in guess. 
        int[] numbers = new int[10];
        
        for (int i = 0; i < secret.length(); i++) {
            if (secret.charAt(i) == guess.charAt(i)) {
                bulls++;
            } else {
                // Increment cows when either number from secret was already seen in guest or vice versa.
                if (numbers[secret.charAt(i)-'0']++ < 0) cows++; // 비밀번호의 인덱스방의 값이 0보다 작으면 추측된 번호가 존재한다.
                if (numbers[guess.charAt(i)-'0']-- > 0) cows++;  // 추즉번호의 인덱스방의 값이 0보다 크면 비밀번호가 존재한다.
                System.out.println(secret.charAt(i) + ":" + numbers[secret.charAt(i) - '0']);
            }
        }
        
        return bulls + "A" + cows + "B";
    }
}
```