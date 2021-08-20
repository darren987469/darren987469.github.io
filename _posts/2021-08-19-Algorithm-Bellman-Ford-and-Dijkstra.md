---
layout: post
title: Algorithm - Bellman Ford and Dijkstra
subtitle:
tags: Bellman-Ford, Dijkstra
---

Leetcode:
* medium, [1514. Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/)

### Bellman Ford

Time complexity: `O(n*E)`
Space complexity: `O(n+E)`
E = edges.length

```java
public double maxProbability(int n, int[][] edges, double[] succProb, int start, int end) {
    Map<Integer, List<int[]>> graph = new HashMap<>();
    for(int i = 0; i < edges.length; i++) {
        int a = edges[i][0], b = edges[i][1];
        graph.computeIfAbsent(a, key -> new ArrayList<>()).add(new int[]{b,i});
        graph.computeIfAbsent(b, key -> new ArrayList<>()).add(new int[]{a,i});
    }
    double[] prob = new double[n];
    prob[start] = 1d;
    Queue<Integer> queue = new LinkedList<>(Arrays.asList(start));
    while(!queue.isEmpty()) {
        int cur = queue.poll();
        for(int[] a : graph.getOrDefault(cur, Collections.emptyList())) {
            int neighbor = a[0], index = a[1];
            if(prob[cur] * succProb[index] > prob[neighbor]) {
                prob[neighbor] = prob[cur] * succProb[index];
                queue.offer(neighbor);
            }
        }
    }
    return prob[end];
}
```

* medium [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

```java
public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
    int edges = k+1;
    // dp[i][j] = distance to reach j with at most i edges from src
    int[][] dp = new int[edges+1][n];
    for(int i = 0; i <= edges; i++) {
        Arrays.fill(dp[i], Integer.MAX_VALUE);
        dp[i][src] = 0; // distance to reach src is 0
    }
    for(int i = 1; i <= edges; i++) {
        for(int[] flight : flights) {
            int u = flight[0], v = flight[1], w = flight[2];
            if(dp[i-1][u] != Integer.MAX_VALUE)
                dp[i][v] = Math.min(dp[i][v], dp[i-1][u] + w);
        }
    }
    int distance = dp[edges][dst];
    return distance == Integer.MAX_VALUE ? -1 : distance;
}
```
Time complexity: `O(kn)`, k is the stops.
Space complexity: `O(kn)`.

### Dijkstra

Time complexity: `O(n*Elogn)`
Space complexity: `O(n+E)`

```java
public double maxProbability(int n, int[][] edges, double[] succProb, int start, int end) {
    Map<Integer, List<int[]>> graph = new HashMap<>();
    for(int i = 0; i < edges.length; i++) {
        int a = edges[i][0], b = edges[i][1];
        graph.computeIfAbsent(a, key -> new ArrayList<>()).add(new int[]{b,i});
        graph.computeIfAbsent(b, key -> new ArrayList<>()).add(new int[]{a,i});
    }
    double[] prob = new double[n];
    prob[start] = 1d;
    PriorityQueue<Integer> pq = new PriorityQueue<>(Comparator.comparingDouble(i -> -prob[i]));
    pq.offer(start);
    while(!pq.isEmpty()) {
        int cur = pq.poll();
        if(cur == end) return prob[end];
        for(int[] a : graph.getOrDefault(cur, Collections.emptyList())) {
            int neighbor = a[0], index = a[1];
            if(prob[cur] * succProb[index] > prob[neighbor]) {
                prob[neighbor] = prob[cur] * succProb[index];
                pq.offer(neighbor);
            }
        }
    }
    return prob[end];
}
```

Similar problems:

* hard 407. Trapping Rain Water II
* medium [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/submissions/)
* medium [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
* medium [1631. Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/)
