---
layout: post
title: Algorithm - breadth first search
subtitle:
tags: algorithm breadth-first-search
---

Leetcode:
* medium, [1926. Nearest Exit from Entrance in Maze](https://leetcode.com/problems/nearest-exit-from-entrance-in-maze/)

```java
int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
public int nearestExit(char[][] maze, int[] entrance) {
    int rows = maze.length, cols = maze[0].length;
    Queue<int[]> queue = new LinkedList<>();
    maze[entrance[0]][entrance[1]] = '+';
    queue.offer(new int[]{entrance[0],entrance[1]});
    int moves = 1;
    while(!queue.isEmpty()) {
        int size = queue.size();
        Queue<int[]> next = new LinkedList<>();
        for(int k = 0; k < size; k++) {
            int[] p = queue.poll();

            for(int[] dir: dirs) {
                int x = p[0] + dir[0];
                int y = p[1] + dir[1];
                if(x < 0 ||x >= rows || y < 0 || y >= cols || maze[x][y] == '+')
                    continue;
                if(x == 0 || x == rows-1 || y == 0 || y == cols-1)
                    return moves;
                maze[x][y] = '+';
                next.offer(new int[]{x,y});
            }
        }
        moves++;
        queue = next;
    }
    return -1;
}
```

