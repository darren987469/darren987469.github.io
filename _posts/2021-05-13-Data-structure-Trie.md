---
layout: post
title: Data structure - Trie
subtitle:
tags: trie
---

Leetcode:
medium, https://leetcode.com/problems/implement-trie-prefix-tree/

```java
class Trie {
    TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node = root;
        for(char c : word.toCharArray()) {
            int i = c - 'a';
            if(node.children[i] == null)
                node.children[i] = new TrieNode();
            node = node.children[i];
        }
        node.word = word;
    }
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode node = root;
        for(char c : word.toCharArray()) {
            int i = c - 'a';
            if(node.children[i] == null)
                return false;
            node = node.children[i];
        }
        return node.word != null;
    }
    class TrieNode {
        String word;
        TrieNode[] children = new TrieNode[26];
    }
}
```

More:
medium, https://leetcode.com/problems/design-add-and-search-words-data-structure/
hard,   https://leetcode.com/problems/word-search-ii/
