---
layout: post
title: Algorithm - breadth first search, depth first search
subtitle:
tags: algorithm breadth-first-search depth-first-search
---

Leetcode:
* medium, [542. 01 Matrix](https://leetcode.com/problems/01-matrix/)`
* medium, [133. Clone Graph](https://leetcode.com/problems/clone-graph/)
* medium, [785. Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)
* medium, [1306. Jump Game III](https://leetcode.com/problems/jump-game-iii/)
* medium, [1926. Nearest Exit from Entrance in Maze](https://leetcode.com/problems/nearest-exit-from-entrance-in-maze/)
* hard, [847. Shortest Path Visiting All Nodes](https://leetcode.com/problems/shortest-path-visiting-all-nodes/)
* hard, [1192. Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/)

```java
public int nearestExit(char[][] maze, int[] entrance) {
    int[][] dirs = new int[][]{ {1,0}, {-1,0}, {0,1}, {0,-1} };
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
