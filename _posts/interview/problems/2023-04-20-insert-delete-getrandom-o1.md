---
layout: post
published: true
title: "380. Insert Delete GetRandom O(1)"
categories: interview
tags: problems hashmap design
---

> RandomizedSet 클래스를 구현: 각 함수가 평균 O(1) 시간 복잡도에서 작동하도록 클래스의 함수를 구현 

- [380. Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/)

```java
class RandomizedSet {
    
    Random random = new Random();

    // 중복체크 및 삭제 연산 최적화를 위해서 인덱스 저장
    HashMap<Integer, Integer> map;
    // 인덱스로 데이터 접근
    ArrayList<Integer> list;
    
    public RandomizedSet() {
        list = new ArrayList<>();
        map = new HashMap<>();
    }
    
    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        
        //key: val, value:index
        map.put(val, list.size());
        list.add(val);
        
        return true;
    }
    
    // 리스트에서 삭제 연산에 대한 최적화: 마지막 데이터를 삭제 위치로 옮긴다.
    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        
        // 마지막과 삭제위치
        int last = list.size() - 1;
        int curr = map.get(val);
        
        // 삭제 아이템이 마지막이 아니면 마지막 아이템으로 갱신한다.
        if (curr < last) {
            int temp = list.get(last);
            list.set(curr, temp);
            map.put(temp, curr);
        }
        
        map.remove(val);
        list.remove(last);
        
        return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        return list.get(random.nextInt(list.size()));
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```