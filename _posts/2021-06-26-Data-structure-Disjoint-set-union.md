---
layout: post
title: Data structure - Disjoint set union
subtitle:
tags: disjoint-set-union
---

### Disjoint set union

Leetcode:
* medium, [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/)
* medium, [1202. Smallest String With Swaps](https://leetcode.com/problems/smallest-string-with-swaps/)

```java
class DSU {
    int[] parent;
    int[] rank;

    public DSU(int size) {
        parent = new int[size];
        for(int i = 0; i < size; i++) parent[i] = i;
        rank = new int[size];
    }

    public int find(int x) {
        if(parent[x] != x) parent[x] = find(parent[x]);
        return parent[x];
    }

    public boolean union(int x, int y) {
        int xr = find(x), yr = find(y);
        if(xr == yr) {
            return false;
        } else if(rank[xr] < rank[yr]) {
            parent[xr] = yr;
        } else if(rank[xr] > rank[yr]) {
            parent[yr] = xr;
        } else {
            parent[yr] = xr;
            rank[xr]++;
        }
        return true;
    }
}
```
