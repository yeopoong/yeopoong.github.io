---
layout: post
published: true
title: "33. Search in Rotated Sorted Array"
categories: interview
tags: binary-search array
---

> 회전 된 오름차순으로 정렬된 배열에서 주어진 정수값의 인덱스를 찾는 문제

- [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

```java
class Solution {
    
    // 회전된 정렬 배열에서 검색
    // O(log n)
    public int search(int[] nums, int target) {

        int left = 0, right = nums.length - 1;
        
        // 1. 시작지점을 찾는다.
        int start = findStart(nums);
        //System.out.format("start=%d", start);

        // 2. 타겟이 오른쪽값보다 작으면 오른쪽 부분에서 찾아야 한다. 
        if (target <= nums[right]) {
            left = start;
        } else {
            right = start;
        }

        // 3. 이진검색으로 값 찾기 
        return binarySearch(nums, left, right, target);
    }
    
    // 시작지점 찾기
    public int findStart(int[] nums) {
        int left = 0, right = nums.length - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            // 중간값이 가장 오른쪽 값보다 크면 회전구간이 존재하므로 시작점은 더 오른쪽에 있다. 
            if (nums[mid] > nums[right]) {
                left = mid + 1;
            // 중간값이 가장 오른쪽 값보다 작으면 시작점은 더 왼쪽에 있다.
            } else {
                right = mid;
            }
        }
        
        return left;
    }
    
    // 이진검색
    public int binarySearch(int[] nums, int left, int right, int target) {
        int mid ;

        // 원소가 홀수 일 경우 때문에 = 조건이 포함되야 한다.
        while (left <= right) {
            mid = left + (right - left) / 2;
            if (nums[mid] < target) left = mid + 1;
            else if (nums[mid] > target) right = mid - 1;
            else return mid; 
        }

        return -1;
    }
}
```