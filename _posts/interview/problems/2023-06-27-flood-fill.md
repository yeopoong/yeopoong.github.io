---
layout: post
published: true
title: "733. Flood Fill"
categories: interview
tags: easy dfs
---

> 플러드 필을 수행한 후 수정된 이미지를 반환

[733. Flood Fill](https://leetcode.com/problems/flood-fill/)

![](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

```java
class Solution {
    //Time Complexity: O(N), where N is the number of pixels in the image. We might process every pixel.
    //Space Complexity: O(N), the size of the implicit call stack when calling dfs.
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        int color = image[sr][sc];
        // The new Color have to be different from the already present color.
        if (color != newColor) {
            dfs(image, sr, sc, color, newColor);
        }
        
        return image;
    }
    
    // recursive function that paints the pixel
    public void dfs(int[][] image, int r, int c, int color, int newColor) {
        // 각 행열의 시작,끝 지점과 동일한 색상의 컬러인지 체크한다.
        if (r < 0 || r == image.length || c < 0 || c == image[0].length || image[r][c] != color) {
            return;
        }
        
        image[r][c] = newColor;
        
        // 상하좌우 처리한다.
        dfs(image, r+1, c, color, newColor);
        dfs(image, r-1, c, color, newColor);
        dfs(image, r, c-1, color, newColor);
        dfs(image, r, c+1, color, newColor);
    }
}
```