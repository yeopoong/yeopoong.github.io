---
layout: post
published: true
title: "1603. Design Parking System"
categories: interview
tags: problems design
---

> 결과 배열에 1만 포함된 비어 있지 않은 가장 긴 하위 배열의 크기를 반환

- [1603. Design Parking System](https://leetcode.com/problems/design-parking-system/)

```java
class ParkingSystem {

    int[] count;
    
    // 디자인 주차 시스템
    public ParkingSystem(int big, int medium, int small) {
        count = new int[]{big, medium, small};
    }

    // T: O(n)
    public boolean addCar(int carType) {
        return count[carType - 1]-- > 0;
    }
}

/**
 * Your ParkingSystem object will be instantiated and called as such:
 * ParkingSystem obj = new ParkingSystem(big, medium, small);
 * boolean param_1 = obj.addCar(carType);
 */
```
