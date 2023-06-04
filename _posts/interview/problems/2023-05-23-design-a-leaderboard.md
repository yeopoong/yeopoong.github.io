---
layout: post
published: true
title: "1244. Design A Leaderboard"
categories: interview
tags: design hashmap
---

> 3가지 기능이 있는 Leaderboard 클래스를 설계
> - addScore(playerId, score): 주어진 플레이어의 점수에 점수를 추가하여 순위표를 업데이트  
> - top(K): 상위 K 플레이어의 점수 합계를 반환  
> - reset(playerId): 주어진 ID를 가진 플레이어의 점수를 0으로 재설정(즉, 리더보드에서 삭제)  

- [1244. Design A Leaderboard](https://leetcode.com/problems/design-a-leaderboard/)

```java
class Leaderboard {
    
    Map<Integer, Integer> scores;
    TreeMap<Integer, Integer> sortedScores;
    
    public Leaderboard() {
        this.scores = new HashMap<Integer, Integer>();
        this.sortedScores = new TreeMap<>(Collections.reverseOrder());
    }
    
    public void addScore(int playerId, int score) {
        
        // The scores dictionary simply contains the mapping from the playerId to their score. 
        // The sortedScores contain a BST with key as the score and value as the number of players that have that score.        
        if (!scores.containsKey(playerId)) {
            scores.put(playerId, score);
            sortedScores.put(score, sortedScores.getOrDefault(score, 0) + 1);
        } else {
            
            // Since the current player's score is changing, we need to
            // update the sortedScores map to reduce count for the old
            // score.
            int preScore = scores.get(playerId);
            int playerCount = sortedScores.get(preScore);
            
            
            // If no player has score, remov it from the tree.
            if (playerCount == 1) {
                sortedScores.remove(preScore);
            } else {
                sortedScores.put(preScore, playerCount - 1);
            }
            
            // Updated score
            int newScore = preScore + score;
            scores.put(playerId, newScore);
            sortedScores.put(newScore, sortedScores.getOrDefault(newScore, 0) + 1);
        }
    }
    
    public int top(int K) {
        
        int count = 0;
        int sum = 0;
        
        // In-order traversal over the scores in the TreeMap
        for (Map.Entry<Integer, Integer> entry: sortedScores.entrySet()) {
            
            // Number of players that have this score.
            int times = entry.getValue();
            int key = entry.getKey();
            
            for (int i = 0; i < times; i++) {
                sum += key;
                count++;
                
                // Found top-K scores, break.
                if (count == K) {
                    break;
                }
            }
            
            // Found top-K scores, break.
            if (count == K) {
                break;
            }
        }
        
        return sum;
    }
    
    public void reset(int playerId) {
        int preScore = scores.get(playerId);
        sortedScores.put(preScore, sortedScores.get(preScore) - 1);
        if (sortedScores.get(preScore) == 0) {
            sortedScores.remove(preScore);
        }
        
        scores.remove(playerId);
    }
}

/**
 * Your Leaderboard object will be instantiated and called as such:
 * Leaderboard obj = new Leaderboard();
 * obj.addScore(playerId,score);
 * int param_2 = obj.top(K);
 * obj.reset(playerId);
 */
```