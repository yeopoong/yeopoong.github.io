---
layout: post
published: true
title: "71. Simplify Path"
categories: interview
tags: medium string stack
---

> Unix 스타일 파일 시스템의 파일 또는 디렉터리에 대한 절대 경로(슬래시 '/'로 시작)인 문자열 경로가 주어지면 이를 단순화된 표준 경로로 변환

- [71. Simplify Path](https://leetcode.com/problems/simplify-path/)

The canonical path should have the following format:

- The path starts with a single slash '/'.
- Any two directories are separated by a single slash '/'.
- The path does not end with a trailing '/'.
- The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period '.' or double period '..')

```java
class Solution {
    
    public String simplifyPath(String path) {

        // Initialize a stack
        Stack<String> stack = new Stack<String>();
        String[] components = path.split("/");

        // Split the input string on "/" as the delimiter
        // and process each portion one by one
        for (String directory : components) {

            // A no-op for a "." or an empty string
            if (directory.equals(".") || directory.isEmpty()) {
                continue;
            } else if (directory.equals("..")) {
                // If the current component is a "..", then
                // we pop an entry from the stack if it's non-empty
                if (!stack.isEmpty()) {
                    stack.pop();
                }
            } else {
                // Finally, a legitimate directory name, so we add it to our stack
                stack.add(directory);
            }
        }

        // Stich together all the directory names together
        StringBuilder result = new StringBuilder();
        for (String dir : stack) {
            result.append("/");
            result.append(dir);
        }

        return result.length() > 0 ? result.toString() : "/" ;
    }
}
```