---
layout: post
published: true
title: "77. Combinations"
categories: interview
tags: medium backtracking
---

> 두 개의 정수 n과 k가 주어지면 [1, n] 범위에서 선택한 k 숫자의 가능한 모든 조합을 반환합니다.

[77. Combinations](https://leetcode.com/problems/combinations)

![](https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg)

```java
class Solution {
	List<List<Integer>> list = new ArrayList<>();
	List<Integer> temp = new ArrayList<>();
    
    // 조합: n개의 숫자 중에서 k개의 수를 순서 없이 뽑는 경우
    public List<List<Integer>> combine(int n, int k) {
		backtrack(n, k, 1);
        
		return list;
	}
    
    // k: 현재까지 전체 개수를 의미한다.
	public void backtrack(int n, int k, int start) {
		if (k == 0) {
			list.add(new ArrayList<>(temp));
			return;
		}
        
        // 순서를 고려하지 않으므로 다음 숫자부터 처리해야 한다.
		for (int i = start; i <= n; i++) {
			temp.add(i);
			backtrack(n, k - 1, i + 1);
			temp.remove(temp.size() - 1);
		}
	}
}
```