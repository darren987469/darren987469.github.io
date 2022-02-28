---
layout: post
title: Data structure - Heap
subtitle:
tags: heap
---

Video: [Heap - Heap Sort - Heapify - Priority Queues](https://www.youtube.com/watch?v=HqPJF2L5h9U)
create a heap: `O(nlogn)`
heapify: `O(n)`
insertion: `O(logn)`
deletion: `O(logn)`

Leetcode:
* medium, [373. Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/)

Concepts like merge sorted linked lists.
nums1 = [1,7,11]
nums2 = [2,4,6]

list1: (1,2) -> (1,4) -> (1,6)
list2: (7,2) -> (7,4) -> (7,6)
list3: (11,2) -> (11,4) -> (11,6)


```java
public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
    PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(o -> o[0] + o[1]));
    List<List<Integer>> ans = new ArrayList<>();
    for(int i = 0; i < k && i < nums1.length; i++) {
        pq.offer(new int[]{ nums1[i], nums2[0], 0 });
        if(pq.size() > k) pq.poll();
    }
    while(k-- > 0 && !pq.isEmpty()) {
        int[] cur = pq.poll();
        ans.add(Arrays.asList(cur[0], cur[1]));
        if(cur[2] == nums2.length -1) continue;
        int nums2Index = cur[2]+1;
        pq.offer(new int[]{ cur[0], nums2[nums2Index], nums2Index });
    }
    return ans;
}

// time complexity: O(kLog(k))
// space complexity: O(k)
```


More:
* hard, [1439. Find the Kth Smallest Sum of a Matrix With Sorted Rows](https://leetcode.com/problems/find-the-kth-smallest-sum-of-a-matrix-with-sorted-rows/)
